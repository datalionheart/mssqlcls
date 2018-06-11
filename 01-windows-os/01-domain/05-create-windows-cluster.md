# Create Windows Cluster
## Initialize all of Node Servers
### Create Node Virtual Machine
> Reference：[Create a New Windows Server](./03-create-domain-controller.md)

![](./pictures/create-nodes-01.png)
### Configure Node Virtual Machine
Example：Node01
| ID | Item | Parameter | Remark |
| --- | --- | --- | --- |
| 1 | Network - Domain | IP:192.168.0.1<br/>Masks:255.255.255.0<br/>Gateway:192.168.0.254<br/>DNS:192.168.0.253 | |
| 2 | Network - Heartbeat | IP:172.168.0.1<br/>Masks:255.255.0.0<br/>Gateway:172.168.0.254 | |
| 3 | Network - Storage | IP:192.168.100.1<br/>Masks:255.255.255.0<br/>Gateway:192.168.100.254 | |
| 4 | Computer Name | SQLN01 | |
![](./pictures/configure-node-01.png)
### Add Node Server Join to Domain
Example：Node01
> Use a Domain User to complete for join domain

![](./pictures/node-join-to-domain-01.png)
> Show welcome information

![](./pictures/node-join-to-domain-02.png)
> Must be restart node computer for finish join domain task

![](./pictures/node-join-to-domain-03.png)
> Login Node Use Domain Admin Account, For Create Cluster<br/>
By default login is local account, so you need choose login by other user and input domain\domainUser to login

![](./pictures/node-join-to-domain-04.png)
## Create Windows Cluster
### Installation Windows Cluster Roles and Features

### (Option)Prepare and Test current Cluster Environment
### Create the Cluster
### Check and fix Network Resource for the Cluster
### Add Storage Resource to the Cluster
### Configure Quorum for the Cluster
### Create MSDTC Application on the Cluster