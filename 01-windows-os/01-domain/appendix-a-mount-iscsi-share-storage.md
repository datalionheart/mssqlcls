# Appendix A: Mount iSCSI Share Storage to Node
## Mount iSCSI Share Storage
> Open Server Manager -> iSCSI Initiator

![](./pictures/mount-iscsi-storage-to-file-system-01.png)
> Select Yes for automatic found storage provider by each restart nodes

![](./pictures/mount-iscsi-storage-to-file-system-02.png)
> Select Discovery card -> Open Discover Portal -> Input Storage Provider IP or DNS name<br/>
By default keep port is 3260

![](./pictures/mount-iscsi-storage-to-file-system-03.png)
> Select Targets, Now you can see target storage status is inactive<br/>
We need connect to it, by each target

![](./pictures/mount-iscsi-storage-to-file-system-04.png)
> Now, iSCSI Storage been mounted to current server node

![](./pictures/mount-iscsi-storage-to-file-system-05.png)
## Create Volume
> Open Server Manager -> Tools -> Computer Management

![](./pictures/mount-iscsi-storage-to-file-system-06.png)
> Select Disk Management -> Select each disk -> make each disk online

![](./pictures/mount-iscsi-storage-to-file-system-07.png)
> Initialize Disk, Click any one disk initalize

![](./pictures/mount-iscsi-storage-to-file-system-08.png)
> System can be found each status been online but not initalize disk<br/>
Now, You can Initialize all of disk<br/>
By default is MBR

![](./pictures/mount-iscsi-storage-to-file-system-09.png)
> Now, You can create volume, If not special requirements, just create simple volume be fine

![](./pictures/mount-iscsi-storage-to-file-system-10.png)
> Startup New Simple Volume Wizard

![](./pictures/mount-iscsi-storage-to-file-system-11.png)
> By default, All remaining space for the current disk will be assigned to the volume

![](./pictures/mount-iscsi-storage-to-file-system-12.png)
> Assign Driver Letter:<br/>
Typically: Quorum Disk Assign Q; MSDTC Disk Assign M

![](./pictures/mount-iscsi-storage-to-file-system-13.png)
> We need format current disk for frist time, keep this setting be ok

![](./pictures/mount-iscsi-storage-to-file-system-14.png)
> Review Summary, Finish

![](./pictures/mount-iscsi-storage-to-file-system-15.png)
> All disks need to repeat this operation<br/>
Now, this is complete stauts

![](./pictures/mount-iscsi-storage-to-file-system-16.png)
## Other Node operational has some differences
> Let disk status to online

![](./pictures/mount-iscsi-storage-to-file-system-17.png)
> Maybe you need rescan all disk status<br/>
You can see All Disk been initalized and has been automatic assigned driver letter<br/>
But the driver letter maybe wrong, If wrong you need reassign driver letter<br/>
Must be let all of node share disk has same driver letter<br/>
Right click volume, Select Change Drive Letter and Paths to Change Driver letter

![](./pictures/mount-iscsi-storage-to-file-system-18.png)
> Click Change, Set correct driver letter assign to current volume

![](./pictures/mount-iscsi-storage-to-file-system-19.png)
> This is just warning, click Yes be ok

![](./pictures/mount-iscsi-storage-to-file-system-20.png)
> Now, All of node share disk been mounted, correct assign driver letter and all volume been usable.

![](./pictures/mount-iscsi-storage-to-file-system-21.png)