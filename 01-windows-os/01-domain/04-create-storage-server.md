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
| ID | Item | Parameter | Remark |
| --- | --- | --- | --- |
| 1 | Computer Name | SS | |
| 2 | Network | 192.168.100.253/24 | |
## Add Storage Roles
### Install Storage Roles

## Configure iSCSI Storage
| ID | Item | Size | Type |
| --- | --- | --- | --- |
| 1 | Quorum Disk | 1GB | Share Disk |
| 2 | MSDTC Disk | 2GB | Share Disk |
Example(Create Quorum Disk, Same step for create other share disk): 
