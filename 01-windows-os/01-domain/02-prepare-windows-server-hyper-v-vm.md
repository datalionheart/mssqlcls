# Prepare Windows Server Hyper-V VM
## Prepare Windows Server Hyper-V VM Master Template
### Create Empty Disk File
> Choose Hyper-V Manager -> New -> Hard Disk

![](./pictures/prepare-windows-vm-master-template-01.png)
> Open -> New Virual Hard Disk Wizard

![](./pictures/prepare-windows-vm-master-template-02.png)
> Choose Disk Format -> VHDX

![](./pictures/prepare-windows-vm-master-template-03.png)
> Dynamically expanding

![](./pictures/prepare-windows-vm-master-template-04.png)
> Input New Disk Name and store path

![](./pictures/prepare-windows-vm-master-template-05.png)
> Set Vistual Hard Disk Size: 256GB

![](./pictures/prepare-windows-vm-master-template-06.png)
> Review the summary and create

![](./pictures/prepare-windows-vm-master-template-07.png)
### Create New VM
> Choose Hyper-V Manager -> New -> Vistual Machine<br/>
Open -> New Virtual Machine Wizard

![](./pictures/prepare-windows-vm-master-template-08.png)
> Input New Virtual Machine Name and store path

![](./pictures/prepare-windows-vm-master-template-09.png)
> Choose Generation 1

![](./pictures/prepare-windows-vm-master-template-10.png)
> Set Memory Size<br/>
Clear Use Dynamic Memory for this virtual machine clickbox<br/>
Input Startup memory size: 4096MB

![](./pictures/prepare-windows-vm-master-template-11.png)
> Set Network configure(Option)

![](./pictures/prepare-windows-vm-master-template-12.png)
> Choose virtual hard disk

![](./pictures/prepare-windows-vm-master-template-13.png)
> Review the summary and create

![](./pictures/prepare-windows-vm-master-template-14.png)
### Configre Vistual Machine Parameters
> Set:<br/>
Processor: 8Cores<br/>
DVD Drive: Windows Server Install Image File Path<br/>
Checkpoints: Clear Use automatic checkpoints chickbox

![](./pictures/prepare-windows-vm-master-template-15.png)
> Start up Vistual Machine

![](./pictures/prepare-windows-vm-master-template-16.png)
> Set Time and currency format: Chinese (Simplified, China)<br/>
P.S. Recommendations:
>> Install English Edition Windows Server<br/>
>> Choose Local languages and formats [The SQL Server installation process automatically selects the appropriate collation and character set]

![](./pictures/prepare-windows-vm-master-template-17.png)
> Install Now

![](./pictures/prepare-windows-vm-master-template-18.png)
> Skip Windows Activation

![](./pictures/prepare-windows-vm-master-template-19.png)
> Choose Windows Server 2016 Standard (Desktop Experience)

![](./pictures/prepare-windows-vm-master-template-20.png)
> Accept the license agreement

![](./pictures/prepare-windows-vm-master-template-21.png)
> Choose Custom: Install Windows only (Advanced)

![](./pictures/prepare-windows-vm-master-template-22.png)
> Choose Disk do not partition

![](./pictures/prepare-windows-vm-master-template-23.png)
> Begin install process and waiting for complete

![](./pictures/prepare-windows-vm-master-template-24.png)
### Templating Vistual Machine
> Set administrator password for new vistual machine

![](./pictures/prepare-windows-vm-master-template-25.png)
> Login new visual machine

![](./pictures/prepare-windows-vm-master-template-26.png)
> Install features:
>> Install .NET Framework 3.5<br/>
>> Install Telnet Client

> GUI
> Open -> Add Roles and Features Wizard

![](./pictures/prepare-windows-vm-master-template-27.png)
> Choose -> Role-based or feature-based installation

![](./pictures/prepare-windows-vm-master-template-28.png)
> Choose -> Select a server from the server pool

![](./pictures/prepare-windows-vm-master-template-29.png)
> Select server roles - do not choose

![](./pictures/prepare-windows-vm-master-template-30.png)
> Choose -> .NET Framework 3.5 Features
Choose -> Telnet Client

![](./pictures/prepare-windows-vm-master-template-31.png)
> Sumrry -> Specify am alternate source path -> For .NET Framework 3.5 Features

![](./pictures/prepare-windows-vm-master-template-32.png)
> Specify Installation Image X:\Sources\Sxs

![](./pictures/prepare-windows-vm-master-template-33.png)
> Install choosed features

![](./pictures/prepare-windows-vm-master-template-34.png)
> Command Line
```command
DISM /Online /Enable-Feature /FeatureName:NetFx3 /All /LimitAccess /Source:X:\sources\sxs
```
> Powershell
```powershell
Install-WindowsFeature Net-Framework-Core -Source X:\sources\sxs
```
> Set features:
>> Disable Firewall

> GUI
> Open -> Windows Firewall with Advanced Security

![](./pictures/prepare-windows-vm-master-template-35.png)
> Open -> Windows Firewall Profile

![](./pictures/prepare-windows-vm-master-template-36.png)
> Set Domain Profile/ Private Profile/ Public Profile Firewall state: Off

![](./pictures/prepare-windows-vm-master-template-37.png)
> Command Line
```command
netsh advfirewall set allprofiles state off
```
> Powershell
```powershell
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False
```

### Generate Master Template
> Use sysprep tool to generate master template

![](./pictures/prepare-windows-vm-master-template-38.png)