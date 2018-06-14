# Appendix B: Configure Virtual Switch
## Create Virtual Switch
> In Hyper-V Manager -> Actions -> Virtual Switch Manager<br/>
New virtual network switch -> Create virtual switch<br/>
-> Internal<br/>
Create 4 virtual network switch:
> * Domain
> * Heartbeat
> * Storage
> * Application

![](./pictures/create-virtual-switch-01.png)
> Configure Virtual Machine Default Gateway -> In Host Server Network Connections -> Select Virtual Ethernet -> Input IP Address and Marks<br/>
The IP Address is Virtual Machine Default Gateway<br/>
If You Configure same subnet IP, You can let virtual machine access Host Server, and Host Server can be access virtual machine 

![](./pictures/create-virtual-switch-02.png)