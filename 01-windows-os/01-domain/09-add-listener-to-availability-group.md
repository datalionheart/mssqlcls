# Add Listener to Availability Group
## (Option)Create Listener By GUI
> Use SSMS GUI, Add Listener in Availability Group

![](./pictures/create-lsr-01.png)
> Open Listener GUI Wizard, Choose Network Mode to Static IP

![](./pictures/create-lsr-02.png)
> Give to them a listener name and port, and add static IP<br/>
Select Subnet 192.168.0.0/24, fill static IP to create

![](./pictures/create-lsr-03.png)
> Review Availability Group/ Availability Group Listener Cluster Resource in Failover Cluster Manager

![](./pictures/create-lsr-04.png)
## (Option)Create Listener By T-SQL
```sql
USE [master]
GO
ALTER AVAILABILITY GROUP [AGDEMO]
ADD LISTENER N'LSRDEMO' (
WITH IP
((N'192.168.0.12', N'255.255.255.0')
)
, PORT=1521);
GO
```