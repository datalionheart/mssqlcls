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

![](./pictures/prepare-windows-vm-master-template-20.png)
![](./pictures/prepare-windows-vm-master-template-21.png)
![](./pictures/prepare-windows-vm-master-template-22.png)
![](./pictures/prepare-windows-vm-master-template-23.png)
![](./pictures/prepare-windows-vm-master-template-24.png)

## Generate New VM by Master Template