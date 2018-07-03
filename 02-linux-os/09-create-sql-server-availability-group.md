# Create SQL Server Availability Group
## Install SQL Server High Availability Component on each nodes
```bash
yum install /opt/mssql-packages/mssql-server-ha-14.0.3029.16-1.x86_64.rpm -y

result:
Loaded plugins: fastestmirror
Examining /opt/mssql-packages/mssql-server-ha-14.0.3029.16-1.x86_64.rpm: mssql-server-ha-14.0.3029.16-1.x86_64
Marking /opt/mssql-packages/mssql-server-ha-14.0.3029.16-1.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package mssql-server-ha.x86_64 0:14.0.3029.16-1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================================================================================================================
 Package                             Arch                       Version                             Repository                                                  Size
=====================================================================================================================================================================
Installing:
 mssql-server-ha                     x86_64                     14.0.3029.16-1                      /mssql-server-ha-14.0.3029.16-1.x86_64                      12 M

Transaction Summary
=====================================================================================================================================================================
Install  1 Package

Total size: 12 M
Installed size: 12 M
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : mssql-server-ha-14.0.3029.16-1.x86_64                                                                                                             1/1
  Verifying  : mssql-server-ha-14.0.3029.16-1.x86_64                                                                                                             1/1

Installed:
  mssql-server-ha.x86_64 0:14.0.3029.16-1

Complete!
```
## Create SQL Certficate/ SQL Login and SQL User for Endpoint
> Linux can't join to active directory, so we need create certficate for each nodes endpoint authorization

```sql
-- Just execute on primary node, once time
USE master
GO

CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'P@ssW0rd'
GO

CREATE CERTIFICATE dbm_ep_cert WITH SUBJECT = 'dbm'
GO

BACKUP CERTIFICATE dbm_ep_cert
	TO FILE = '/var/opt/mssql/data/dbm_ep_cert.cer'
	WITH PRIVATE KEY (
		FILE = '/var/opt/mssql/data/dbm_ep_cert.pvk',
		ENCRYPTION BY PASSWORD = 'P@ssW0rd'
	)
GO

CREATE LOGIN dbm_ep_login WITH PASSWORD = 'P@ssW0rd'
GO

CREATE USER dbm_ep_user FOR LOGIN dbm_ep_login
GO
```
> Copy Master Certificate to Other each nodes
```bash
# dbm_ep_cert.* certificates on 192.168.0.21 in /var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.22:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.23:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.24:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.25:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.26:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.27:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.28:/var/opt/mssql/data/
scp dbm_ep_cert.* root@192.168.0.29:/var/opt/mssql/data/

result:
dbm_ep_cert.cer                                                                                                                    100%  667   653.3KB/s   00:00
dbm_ep_cert.pvk                                                                                                                    100% 1212   669.5KB/s   00:00

# Allow Microsoft SQL Server Database Engine Service Access the files, By default SQL Server Database Engine Service User and Group named is mssql
chown mssql:mssql /var/opt/mssql/data/dbm_ep_cert.*
```
> Create and import master certificate to other each nodes
```sql
-- Just create/ store/ use in instance level, so not need from primary node export hash password and sid for create sql login on other nodes
USE master
GO

CREATE LOGIN dbm_ep_login WITH PASSWORD = 'P@ssW0rd'
GO

CREATE USER dbm_ep_user FOR LOGIN dbm_ep_login
GO

-- Import master certificate to instance
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'P@ssW0rd'
GO

CREATE CERTIFICATE dbm_ep_cert
	AUTHORIZATION dbm_ep_user
		FROM FILE = '/var/opt/mssql/data/dbm_ep_cert.cer'
	WITH PRIVATE KEY (
		FILE = '/var/opt/mssql/data/dbm_ep_cert.pvk',
		DECRYPTION BY PASSWORD = 'P@ssW0rd'
	)
GO
```
## Start AlwaysOn XEvent and Endpoint Service on all of nodes
```sql
ALTER EVENT SESSION AlwaysOn_health ON SERVER WITH (STARTUP_STATE = ON)
GO

CREATE ENDPOINT Hadr_endpoint
	AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
	FOR DATA_MIRRORING (
		ROLE = ALL,
		AUTHENTICATION = CERTIFICATE dbm_ep_cert,
		ENCRYPTION = REQUIRED ALGORITHM AES
		)
GO

ALTER ENDPOINT Hadr_endpoint STATE = STARTED
GO

GRANT CONNECT ON ENDPOINT::Hadr_endpoint TO dbm_ep_login
GO
```
## Create SQL Server Availability Group
```sql
-- Just execute on primary node, once time
USE [master]
GO

CREATE AVAILABILITY GROUP [AGDEMO]
WITH (AUTOMATED_BACKUP_PREFERENCE = SECONDARY,
DB_FAILOVER = ON,
-- DTC_SUPPORT = PER_DB,
-- SQL 2017 CU8 NO SUPPORT DTC
CLUSTER_TYPE = EXTERNAL,
-- Linux HA is Pacemaker-Based is EXTERNAL
-- Windows HA is WSFC-Based is WSFC
-- Linux / Windows NON-HA is NONE
REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 0)
FOR
	-- DATABASE [DEMODB] 
    -- create availability group frist, then create database and add to the availability group
    -- create availability group frist without user database(s)
REPLICA ON 
N'sqll01' 
	WITH (ENDPOINT_URL = N'TCP://sqll01:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL
		, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll02' 
	WITH (ENDPOINT_URL = N'TCP://sqll02:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL
		, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll03' 
	WITH (ENDPOINT_URL = N'TCP://sqll03:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL
		, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll04' 
	WITH (ENDPOINT_URL = N'TCP://sqll04:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll05' 
	WITH (ENDPOINT_URL = N'TCP://sqll05:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll06' 
	WITH (ENDPOINT_URL = N'TCP://sqll06:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll07' 
	WITH (ENDPOINT_URL = N'TCP://sqll07:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll08' 
	WITH (ENDPOINT_URL = N'TCP://sqll08:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY)),
N'sqll09' 
	WITH (ENDPOINT_URL = N'TCP://sqll09:5022'
		, FAILOVER_MODE = EXTERNAL                        -- EXTERNAL, NO SUPPORT MANUAL OPTION KEYWORD
		, AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT
		, BACKUP_PRIORITY = 50
		, SEEDING_MODE = AUTOMATIC
		, SECONDARY_ROLE(ALLOW_CONNECTIONS = READ_ONLY));
GO
```
## Join other nodes to this Availability Group
```sql
ALTER AVAILABILITY GROUP [AGDEMO] JOIN WITH (CLUSTER_TYPE = EXTERNAL)
GO
```
## High Availability Managed to Pacemaker
> Create SQL Managed Account to all of nodes
```sql
-- Execute on all of nodes
USE master
GO

-- Create HA Managed SQL Access Login Account
CREATE LOGIN [pcs_login] WITH PASSWORD = 'P@ssW0rd'
GO

-- Grant some instance permissions to Managed SQL Account
ALTER SERVER ROLE [sysadmin] ADD MEMBER [pcs_login]
GO

GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP :: [AGDEMO] TO [pcs_login]
GO

GRANT VIEW SERVER STATE TO [pcs_login]
GO
```
> Save SQL Managed Account to file, Execute on all of nodes
```bash
echo 'pcs_login' >> ~/pacemaker-passwd
echo 'P@ssW0rd' >> ~/pacemaker-passwd
mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
chown root:root /var/opt/mssql/secrets/passwd
# Only readable by root, For protect SQL Managed account and password
chmod 400 /var/opt/mssql/secrets/passwd
```
## Create Pacemaker High Availability Resource
> In primary node execute once
```bash
# Must be execute this command
pcs property set start-failure-is-fatal=true 

# Create pacemaker cluster resource, must be match SQL Server exist Availability Group Name
pcs resource create ag_resource ocf:mssql:ag ag_name=AGDEMO meta failure-timeout=30s master notify=true
# Create pacemaker heartbeat IP
pcs resource create ip_resource ocf:heartbeat:IPaddr2 ip=192.168.0.32
# Binding resources constraint relationships
pcs constraint colocation add ip_resource ag_resource-master INFINITY with-rsc-role=Master

## If need, can be Manual promote instance
pcs constraint order promote ag_resource-master then start ip_resource
```
## Pacemaker Maintenance
> Pacemaker Cluster Status
```bash
pcs cluster status --all

result:
Cluster Status:
 Stack: corosync
 Current DC: sqll07 (version 1.1.18-11.el7-2b07d5c5a9) - partition with quorum
 Last updated: Tue Jul  3 22:00:32 2018
 Last change: Tue Jul  3 21:52:38 2018 by root via cibadmin on sqll01
 9 nodes configured
 10 resources configured

PCSD Status:
  sqll06: Online
  sqll03: Online
  sqll01: Online
  sqll02: Online
  sqll04: Online
  sqll08: Online
  sqll07: Online
  sqll05: Online
  sqll09: Online
```
> Pacemaker Resource status
```bash
pcs status

result:
Cluster name: hacluster
Stack: corosync
Current DC: sqll07 (version 1.1.18-11.el7-2b07d5c5a9) - partition with quorum
Last updated: Tue Jul  3 22:01:43 2018
Last change: Tue Jul  3 21:52:38 2018 by root via cibadmin on sqll01

9 nodes configured
10 resources configured

Online: [ sqll01 sqll02 sqll03 sqll04 sqll05 sqll06 sqll07 sqll08 sqll09 ]

Full list of resources:

 Master/Slave Set: ag_resource-master [ag_resource]
     Masters: [ sqll01 ]
     Slaves: [ sqll02 sqll03 sqll04 sqll05 sqll06 sqll07 sqll08 sqll09 ]
 ip_resource    (ocf::heartbeat:IPaddr2):       Started sqll01

Daemon Status:
  corosync: active/disabled
  pacemaker: active/disabled
  pcsd: active/enabled
```
> Pacemaker Resource Remove
```bash
pcs resource delete resource_id(ip_resource/ag_resource/other)
```