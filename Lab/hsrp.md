> ## Basic HSRP  
```
R1#sh ip int brief

R1#conf t
R1(config)#int g0/1
R1(config-if)#ip address 10.10.10.2 255.255.255.0
R1(config-if)#no shut
R1(config-if)#standby 1 ip 10.10.10.1

R2#conf t
R2(config)#int g0/1
R2(config-if)#ip address 10.10.10.3 255.255.255.0
R2(config-if)#no shut
R2(config-if)#standby 1 ip 10.10.10.1

R1#sh standby

C:\>ping 10.10.10.1

C:\>ping 203.0.113.1
```
>## Priority and pre-emption  
```
R1(config)#int g0/1
R1(config-if)#standby 1 priority 110
R1(config-if)#do sh standby

R1(config-if)#int g0/1
R1(config-if)#standby 1 preempt 
```
