# Based-VM Template Create Domain Controller Server
## Create a New Windows Server
### Create Domain Controller Server Disk
> Choose -> File Format VHDX

![](./pictures/create-dc-01.png)
> Choose -> Differncing

![](./pictures/create-dc-02.png)
> Input DC Hard Disk Name and Choose Store Path

![](./pictures/create-dc-03.png)
> Choose template file

![](./pictures/create-dc-04.png)
> Summary Ready to Create

![](./pictures/create-dc-05.png)
### Create Domain Controller Server Virtual Machine
> Input VM Name and choose store path

![](./pictures/create-dc-06.png)
> Choose -> Generation 1

![](./pictures/create-dc-07.png)
> Set Startup Memory 2048MB

![](./pictures/create-dc-08.png)
> Choose Domain Subnet

![](./pictures/create-dc-09.png)
> Choose Domain Controller Server Hard Disk

![](./pictures/create-dc-10.png)
> Summary Ready to Create

![](./pictures/create-dc-11.png)
### Set Domain Controller Server VM Parameters
> Parameters:
>> Processor: 8 Cores
>> Checkpoint: Clear Use automatic checkpoints

![](./pictures/create-dc-12.png)
### Startup VM
![](./pictures/create-dc-13.png)
> Waiting for Init

![](./pictures/create-dc-14.png)
## Configure for prepare setup domain controller
### Set System Parameters
> Country/Region Language Keyboard

![](./pictures/create-dc-15.png)
> Skip Windows Activation

![](./pictures/create-dc-16.png)
> Accept the license

![](./pictures/create-dc-17.png)
> Set Windows Administrator Password

![](./pictures/create-dc-18.png)
## Add Domain Controller Roles
### Install Domain Controller Roles
> Server Manager -> Add Roles and Features

![](./pictures/add-dc-roles-01.png)
> Choose -> Role-based or feature-based installation

![](./pictures/add-dc-roles-02.png)
> Select a server from the server pool -> Choose DCS

![](./pictures/add-dc-roles-03.png)
> Clicked Roles -> Active Directory Domain Services<br/>
Include management tools

![](./pictures/add-dc-roles-04.png)
> Do nothing -> Next

![](./pictures/add-dc-roles-05.png)
> Do nothing -> Next

![](./pictures/add-dc-roles-06.png)
> Install Roles and Features

![](./pictures/add-dc-roles-07.png)
## Configure Domain Controller
### Create Domain Controller
> Choose Promote this server to a domain controller

![](./pictures/configure-dc-01.png)
> Add a new forest<br/>
Input New Domain Name

![](./pictures/configure-dc-02.png)
> Input DSRM Password

![](./pictures/configure-dc-03.png)
> Do nothing -> Next (Need New a DNS Service)

![](./pictures/configure-dc-04.png)
> Do nothing -> Show default NetBIOS Name

![](./pictures/configure-dc-05.png)
> Do nothing -> Next

![](./pictures/configure-dc-06.png)
> Summary for AD DC Configure

![](./pictures/configure-dc-07.png)
> Review Checklist

![](./pictures/configure-dc-08.png)
> Install DC by configures

![](./pictures/configure-dc-09.png)
> The Installation process need to automatic restart this computer

![](./pictures/configure-dc-10.png)
## Configure Domain Controller Before Installed
> Sign to this computer
Now you can see defalut login name change to Domain Administrator

![](./pictures/configure-dc-11.png)
> Open -> Active Directory Users and Computers

![](./pictures/configure-dc-12.png)
> Create a OU for management SQL Server Service Account

![](./pictures/configure-dc-13.png)
> OU Named: SQLServices and click protect model

![](./pictures/configure-dc-14.png)
> Create Domian Users in SQLService OU

![](./pictures/configure-dc-15.png)
> Input UserName LoginName

![](./pictures/configure-dc-16.png)
> Input Login Password and must be clicked Password never expires

![](./pictures/configure-dc-17.png)
> Show the summary

![](./pictures/configure-dc-18.png)
> Create Domain Users for SQL Services
>> SQLEngine: SQL Database Engine<br/>
>> SQLAgent: SQL Agent<br/>
>> SQLReport: SQL Reporting Service<br/>
>> SQLAnalysis: SQL Analysis Service

![](./pictures/configure-dc-19.png)