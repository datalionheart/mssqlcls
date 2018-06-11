# Create Storage Server
## Create a New Windows Server
> Reference：[Create a New Windows Server](./03-create-domain-controller.md)
### Create Storage Server Disk
> Reference：[Create a New Windows Server](./03-create-domain-controller.md)
### Create Storage Server Virtual Machine
> Reference：[Create a New Windows Server](./03-create-domain-controller.md)
### Set Storage Server VM Parameters
> Reference：[Create a New Windows Server](./03-create-domain-controller.md)
### Startup VM
### Set System Parameters
| ID | Item | Parameter |
| --- | --- | --- |
| 1 | Computer Name | SS |
| 2 | Network | IP: 192.168.100.253<br/>Masks: 255.255.255.0<br/>Gateway: 192.168.100.254 |
## Add Storage Roles
### Install Storage Roles
> Open Server Manager -><br/>
Open Add Roles and Features Wizard -><br/>
Select Role-based or feature-based installation

![](./pictures/add-iscsi-role-01.png)
> Select a server from the server pool

![](./pictures/add-iscsi-role-02.png)
> Choose some feature:<br/>
File and Storage Services<br/>
>> File and iSCSI Services<br/>
>>> File Server<br/>
>>> iSCSI Target Server<br/>
>>> iSCSI Target Storage Provider

![](./pictures/add-iscsi-role-03.png)
> Do nothing, Next

![](./pictures/add-iscsi-role-04.png)
> Summary，Do nothing, Install

![](./pictures/add-iscsi-role-05.png)
> Done. Server Manager -> File and Storage Services -> Show below contents

![](./pictures/add-iscsi-role-06.png)
## Configure iSCSI Storage
| ID | Item | Size | Type |
| --- | --- | --- | --- |
| 1 | Quorum Disk | 1GB | Share Disk |
| 2 | MSDTC Disk | 2GB | Share Disk |

Example(Create Quorum Disk, Same step for create other share disk): 
> Create frist iSCSI disk

![](./pictures/create-share-disk-01.png)
> Open New iSCSI Virtual Disk Wizard<br/>
Choose custom path for store the virtual disk file

![](./pictures/create-share-disk-02.png)
> Give the new virtual disk a name

![](./pictures/create-share-disk-03.png)
> Set the new virtual disk size

![](./pictures/create-share-disk-04.png)
> We need other server can be access the share disk, so need configre new iSCSI target for discover by network

![](./pictures/create-share-disk-05.png)
> Give the new iSCSI target a name

![](./pictures/create-share-disk-06.png)
> Input need access the storage server IPs

![](./pictures/create-share-disk-07.png)
> Summary, Next

![](./pictures/create-share-disk-08.png)
> Do nothing, Next

![](./pictures/create-share-disk-09.png)
> Summary, Create

![](./pictures/create-share-disk-10.png)
> Waiting for finish

![](./pictures/create-share-disk-11.png)
> Continue for New MSDTC Disk and iSCSI Target

![](./pictures/create-share-disk-12.png)
> Create iSCSI for each disk group

![](./pictures/create-share-disk-13.png)
> Summary, Create

![](./pictures/create-share-disk-14.png)
> Completed, Look like the below

![](./pictures/create-share-disk-15.png)