# Single Subnet HA Solution
## Software requirements
| ID | Item | Limited | Remark |
| --- | --- | --- | --- |
| 1 | Windows Server 2016 Standard Edition | Must be match SQL Server Install Image Language | Required |
| 2 | SQL Server 2017 Enterprise Edition | Must be match Windows Server Install Image Language | Required |
| 3 | SQL Server Management Studio | Must be match Windows Server Install Image Language | Option |
## Node and Hardware requirements
| ID | Item | Limited | Remark |
| --- | --- | --- | --- |
| 1 | Domain Controller | CPU 2Cores; MEM 2GB; Disk Size 32GB | Min 1 Node |
| 2 | SQL Server Node | CPU 8Cores; MEM 2GB; Disk Size 64GB | Max 9 Nodes |
| 3 | iSCIS Server Node | CPU 2Cores; MEM 2GB; Disk Size 64GB | Min 1 Nodes; 2 Disks：1 Quorum 1GB/ 1 MSDTC 4GB |
## Architecture
![](./pictures/domain-single-subnet-ha.png)