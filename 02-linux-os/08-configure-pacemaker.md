# Configure Pacemaker Cluster
## Set Password by User hacluster on each nodes
```bash
passwd hacluster
# Password: P@ssW0rd

result:
Changing password for user hacluster.
New password:
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password:
passwd: all authentication tokens updated successfully.
```
> P.S. Must be make sure each node user hacluster has same password
## Configure Pacemaker Service on each nodes
```bash
systemctl enable pcsd

result:
Created symlink from /etc/systemd/system/multi-user.target.wants/pcsd.service to /usr/lib/systemd/system/pcsd.service.

systemctl start pcsd

systemctl enable pacemaker

result:
Created symlink from /etc/systemd/system/multi-user.target.wants/pacemaker.service to /usr/lib/systemd/system/pacemaker.service.
```
## Authoritarian and Startup Pacemaker Cluster on any node
```bash
pcs cluster auth sqll01 sqll02 sqll03 sqll04 sqll05 sqll06 sqll07 sqll08 sqll09 -u hacluster -p 'P@ssW0rd'

result:
sqll06: Authorized
sqll07: Authorized
sqll04: Authorized
sqll05: Authorized
sqll02: Authorized
sqll03: Authorized
sqll01: Authorized
sqll08: Authorized
sqll09: Authorized

pcs cluster setup --name hacluster sqll01 sqll02 sqll03 sqll04 sqll05 sqll06 sqll07 sqll08 sqll09

result:
Destroying cluster on nodes: sqll01, sqll02, sqll03, sqll04, sqll05, sqll06, sqll07, sqll08, sqll09...
sqll01: Stopping Cluster (pacemaker)...
sqll09: Stopping Cluster (pacemaker)...
sqll02: Stopping Cluster (pacemaker)...
sqll08: Stopping Cluster (pacemaker)...
sqll06: Stopping Cluster (pacemaker)...
sqll05: Stopping Cluster (pacemaker)...
sqll03: Stopping Cluster (pacemaker)...
sqll04: Stopping Cluster (pacemaker)...
sqll07: Stopping Cluster (pacemaker)...
sqll04: Successfully destroyed cluster
sqll06: Successfully destroyed cluster
sqll05: Successfully destroyed cluster
sqll07: Successfully destroyed cluster
sqll02: Successfully destroyed cluster
sqll09: Successfully destroyed cluster
sqll03: Successfully destroyed cluster
sqll01: Successfully destroyed cluster
sqll08: Successfully destroyed cluster

Sending 'pacemaker_remote authkey' to 'sqll01', 'sqll02', 'sqll03', 'sqll04', 'sqll05', 'sqll06', 'sqll07', 'sqll08', 'sqll09'
sqll01: successful distribution of the file 'pacemaker_remote authkey'
sqll02: successful distribution of the file 'pacemaker_remote authkey'
sqll03: successful distribution of the file 'pacemaker_remote authkey'
sqll04: successful distribution of the file 'pacemaker_remote authkey'
sqll05: successful distribution of the file 'pacemaker_remote authkey'
sqll07: successful distribution of the file 'pacemaker_remote authkey'
sqll08: successful distribution of the file 'pacemaker_remote authkey'
sqll09: successful distribution of the file 'pacemaker_remote authkey'
sqll06: successful distribution of the file 'pacemaker_remote authkey'
Sending cluster config files to the nodes...
sqll01: Succeeded
sqll02: Succeeded
sqll03: Succeeded
sqll04: Succeeded
sqll05: Succeeded
sqll06: Succeeded
sqll07: Succeeded
sqll08: Succeeded
sqll09: Succeeded

Synchronizing pcsd certificates on nodes sqll01, sqll02, sqll03, sqll04, sqll05, sqll06, sqll07, sqll08, sqll09...
sqll06: Success
sqll07: Success
sqll04: Success
sqll05: Success
sqll02: Success
sqll03: Success
sqll01: Success
sqll08: Success
sqll09: Success
Restarting pcsd on the nodes in order to reload the certificates...
sqll09: Success
sqll06: Success
sqll07: Success
sqll04: Success
sqll05: Success
sqll02: Success
sqll03: Success
sqll01: Success
sqll08: Success

pcs cluster start --all

result:
sqll01: Starting Cluster...
sqll04: Starting Cluster...
sqll08: Starting Cluster...
sqll03: Starting Cluster...
sqll06: Starting Cluster...
sqll09: Starting Cluster...
sqll05: Starting Cluster...
sqll02: Starting Cluster...
sqll07: Starting Cluster...

pcs cluster status --all

result:
Cluster Status:
 Stack: corosync
 Current DC: sqll05 (version 1.1.18-11.el7-2b07d5c5a9) - partition with quorum
 Last updated: Tue Jul  3 18:09:40 2018
 Last change: Tue Jul  3 18:09:37 2018 by hacluster via crmd on sqll05
 9 nodes configured
 0 resources configured

PCSD Status:
  sqll09: Online
  sqll03: Online
  sqll02: Online
  sqll07: Online
  sqll01: Online
  sqll08: Online
  sqll04: Online
  sqll06: Online
  sqll05: Online
```