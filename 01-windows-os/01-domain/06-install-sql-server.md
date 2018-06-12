# Install SQL Server to each node
## Prepare Installation
> Recommended: Use Domain User to Install SQL Server

![](./pictures/install-sql-server-01.png)
> Select Hyper-V Client -> Media -> DVD Drive -> Insert Disk -> Found SQL Server ISO Image

![](./pictures/install-sql-server-02.png)
## Install SQL Server by SQL Server Installation Center
> SQL Server Availability Group need standalone install SQL Server, Not like install SQL Cluster

![](./pictures/install-sql-server-03.png)
> You have two choose<br/>
1. Specify a free edition, Include developer edition/ Evaluation edition/ Express edition<br/>
2. Enter the product key, SQL Server use this key for identify editions

![](./pictures/install-sql-server-04.png)
> Accept license

![](./pictures/install-sql-server-05.png)
> Because current is internal network, so clean this checkbox

![](./pictures/install-sql-server-06.png)
> Because current is internal network, so we can access internet, so this error is normal

![](./pictures/install-sql-server-07.png)
> Do nothing, waiting for install support files

![](./pictures/install-sql-server-08.png)
> Choose need SQL Server features

| ID | Type | Item |
| --- | --- | --- |
| 1 | Instance Feature | Database Engine Service |
| 2 | Share Tools | Client Tools Connectivity |
| 3 | Share Tools | Integration Services |
| 4 | Share Tools | Client Tools Backwards Compatibility |
| 5 | Share Tools | Client Tools SDK |
| 6 | Share Tools | SQL Client Cnnectivity SDK |

![](./pictures/install-sql-server-09.png)
![](./pictures/install-sql-server-10.png)
> Choose default instance or named instance, Current Handbook just use default instance

![](./pictures/install-sql-server-11.png)
> 1. Give each service a account, Recommended: Domain User<br/>
2. SQL Server Browser: From Disabled to Automatic Start<br/>
3. Grant Perform Volume Maintenance Task privilege to SQL Server Database Engine Service<br/>
P.S. Must be Manual of setting [local security policy](./pictures/install-sql-server-24.png) by each node

![](./pictures/install-sql-server-12.png)
> SQL Server automatic choose collation by System Language, User NOT need do anything

![](./pictures/install-sql-server-13.png)
> Mixed Mode, Input SQL user: sa Password<br/>
Add Windows authentication users or groups

![](./pictures/install-sql-server-14.png)
> Review summary, begin install process

![](./pictures/install-sql-server-15.png)
> Waiting for complete

![](./pictures/install-sql-server-16.png)
> Review complete status report

![](./pictures/install-sql-server-17.png)
## Install SQL Server Patch to each nodes
> Accept license

![](./pictures/install-sql-server-18.png)
> Select need patch instance or instances

![](./pictures/install-sql-server-19.png)
> Installation Wizard automatic upgrade environment

![](./pictures/install-sql-server-20.png)
> Review summary, Update

![](./pictures/install-sql-server-21.png)
> Waiting for complete

![](./pictures/install-sql-server-22.png)
> Review complete status report

![](./pictures/install-sql-server-23.png)