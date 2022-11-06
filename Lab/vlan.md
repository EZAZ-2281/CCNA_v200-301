```
sh vlan brief
!
sh int g0/1 switchport
!
```
```
sw1
int g0/1
switchport mode trunk
!
sw2
int g0/1
switchport trunk encap dot1q
switchport mode trunk
int g0/2
switchport trunk encap dot1q
switchport mode trunk
!
sw3
int g0/2
switchport mode trunk 
!
sw1
vtp domain dhaka
vtp mode server
!
sw2
vtp mode transparent
!
sw3
vtp mode client
vtp domain dhaka
!
```
```
sw1
vlan 10
name Eng
vlan 20
name Sales
vlan 199
name Native
!
sw2
vlan 10
name Eng
vlan 20
name Sales
vlan 199
name Native
!
sw1
int g0/1
switchport trunk native vlan 199
sw2
int g0/1
switchport trunk native vlan 199
int g0/2
switchport trunk native vlan 199
sw3
int g0/2
switchport trunk native vlan 199
!
sw1
int range f0/1 - 2
switchport mode access
switchport access vlan 10
int f0/3
switchport mode access
switchport access vlan 20
!
sw3
int range f0/1 - 2
switchport mode access
switchport access vlan 20
int f0/3
switchport mode access
switchport access vlan 10
!
```
> # Option-1: Separate Interfaces on Router  
```
R1
int f0/0
ip address 10.10.10.1 255.255.255.0
no shut
int f0/1
ip address 10.10.20.1 255.255.255.0 
no shut 
!
sw2
int f0/1
switchport mode access
switchport access vlan 10
int f0/2
switchport mode access 
switchport access vlan 20
!
R1
int f0/1
shut
!
```
> # Option-2: Router on a Stick  
```
R1
int f0/0
no ip address
no shut
!
int f0/0.10
encapsulation dot1q 10
ip address 10.10.10.1 255.255.255.0
no shut
!
int f0/0.20
encapsulation dot1q 20
ip address 10.10.20.1 255.255.255.0
no shut
!
sw2
int f0/1
switchport trunk encapsulation dot1q
switchport mode trunk 
!
R1
int f0/0
shut
!
```
> # Option-3: Layer 3 switch
```
sw2
ip routing
int vlan 10
ip address 10.10.10.1 255.255.255.0
no shut
int vlan 20
ip address 10.10.20.1 255.255.255.0
no shut
!
```
