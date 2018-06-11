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
> Must be install windows cluster roles and features on all of nodes<br/>
> If want on one node install all of nodes features, Need configure Server Manager -> All Servers

![](./pictures/install-cluster-feature-01.png)
> Search DEMO.COM below all servers and select you want add to group

![](./pictures/install-cluster-feature-02.png)
> Then you can see all server information on this node dashboard

![](./pictures/install-cluster-feature-03.png)
> Select Server Manager -> Manage -> Add Roles and Features<br/>
Role-based or feature-based installation to install

![](./pictures/install-cluster-feature-04.png)
> Select a server from the server pool -> Node Name to add some roles or features to the node

![](./pictures/install-cluster-feature-05.png)
> Do nothing, Next

![](./pictures/install-cluster-feature-06.png)
> Clicked Features -> Failover Clustering and add include management tools

![](./pictures/install-cluster-feature-07.png)
> Review the summary, then click install to process

![](./pictures/install-cluster-feature-08.png)
> You can on Server Manager check all node installation progress

![](./pictures/install-cluster-feature-09.png)
### (Option)Prepare and Test current Cluster Environment
> Only need to execute once on any node<br/>
> Select Server Manager -> Tools -> Failover Cluster Manager

![](./pictures/create-cluster-01.png)
> Click Validate Configuration

![](./pictures/create-cluster-02.png)
> Startup Validate a Configuration Wizard

![](./pictures/create-cluster-03.png)
> Select and add this cluster include all nodes

![](./pictures/create-cluster-04.png)
> Run all tests (If you know some test items configure install laster, you can skip the items)

![](./pictures/create-cluster-05.png)
> Review summary, then next

![](./pictures/create-cluster-06.png)
> Run test items, maybe need a few minutes

![](./pictures/create-cluster-07.png)
> All test complete, you can check required items, then clicked the Create the cluster now using the validated nodes to create cluster

![](./pictures/create-cluster-08.png)
### Create the Cluster
> Startup Create Cluster Wizard

![](./pictures/create-cluster-09.png)
> Input Cluster Name, Choose Cluster Network (192.168.0.0/24), give them a IP Address and Make sure other subnet been clean

![](./pictures/create-cluster-10.png)
> Review summary, Then Next

![](./pictures/create-cluster-11.png)
> Create Cluster, maybe need a few minutes

![](./pictures/create-cluster-12.png)
> Click install log

![](./pictures/create-cluster-13.png)
> Now, you can operate the cluster

![](./pictures/create-cluster-14.png)
### Check and fix Network Resource for the Cluster
> Select Failover Cluster Manager -> Networks

![](./pictures/check-cluster-network-01.png)
> Rename Network Resource Name
>
| ID | Name | Item | Subitem | Role ID |
| --- | --- | --- | --- | --- |
| 1 | Domain | Allow cluster network communication on this network | Allow clients to connect through this network | 3 |
| 2 | Heartbeat | Allow cluster network communication on this network | - | 1 |
| 3 | Storage | - | - | 0 |

![](./pictures/check-cluster-network-02.png)
![](./pictures/check-cluster-network-03.png)
![](./pictures/check-cluster-network-04.png)
> Complete

![](./pictures/check-cluster-network-05.png)
### Add Storage Resource to the Cluster
> Add Storage Resource to Cluster

![](./pictures/mount-iscsi-storage-to-file-system-22.png)
> Rename Resource

![](./pictures/mount-iscsi-storage-to-file-system-23.png)
### Configure Quorum for the Cluster

### Create MSDTC Application on the Cluster