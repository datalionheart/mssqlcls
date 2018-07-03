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