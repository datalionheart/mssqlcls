# Create Database and Join to Existed Availability Group
## Create same directory in each nodes
```powershell
Invoke-Command -ComputerName SQLN01, SQLN02, SQLN03, SQLN04, SQLN05, SQLN06, SQLN07, SQLN08, SQLN09 -ScriptBlock {mkdir C:\Databases}
```
## Create Database and Join to availability group
```sql
-- :CONNECT SQLN01 Only Execute in SQLN01 Once
-- Create User Database in specify directory
CREATE DATABASE DEMODB
ON PRIMARY
	(NAME = DEMODB_DATA,
	  FILENAME = N'C:\Databases\DEMODB_DATA.mdf',
          SIZE = 8MB,
          FILEGROWTH = 0)
LOG ON
	( NAME = DEMODB_LOG,
	  FILENAME = N'C:\Databases\DEMODB_LOG.ldf',
          SIZE = 16MB,
          FILEGROWTH = 128MB)
GO

-- Full backup the user database, for enable restore start point, then you can delete the backup file
BACKUP DATABASE DEMODB TO DISK = 'C:\Databases\DEMODB.bak'
GO

-- Add the user database to specify availability group
ALTER AVAILABILITY GROUP [AGDEMO] ADD DATABASE [DEMODB]
GO
```