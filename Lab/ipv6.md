> ## IPv6 Configuration 
```
R1(config)#int f0/1
R1(config-if)#ipv6 address 2001:db8::1/64
R1(config-if)#no shut
R1(config-if)#int f0/0
R1(config-if)#ipv6 address 2001:db8:0:1::1/64
R1(config-if)#no shut 

R2(config)#int f0/0
R2(config-if)#ipv6 address 2001:db8:0:1::2/64
R2(config-if)#no shut
R2(config-if)#int f0/1
R2(config-if)#ipv6 address 2001:db8:0:2::2/64
R2(config-if)#no shut

R3(config)#int f0/0
R3(config-if)#ipv6 address 2001:db8:0:1::2/64
R3(config-if)#no shut
R3(config-if)#int f0/1
R3(config-if)#ipv6 address 2001:db8:0:3::1/64
R3(config-if)#no shut

PC1(config)#int f0/0
PC1(config-if)#ipv6 address 2001:db8::/64 eui-64
PC1(config-if)#no shut

PC2(config)#int f0/0
PC2(config-if)#ipv6 address 2001:db8:0:3::/64 eui-64
PC2(config-if)#no shut

R1(config-if)#int f0/0
R1(config-if)#ipv6 address fe80::1 link-local
R1(config-if)#int f0/1
R1(config-if)#ipv6 address fe80::1 link-local

R2(config-if)#int f0/0
R2(config-if)#ipv6 address fe80::2 link-local
R2(config-if)#int f0/1
R2(config-if)#ipv6 address fe80::2 link-local

R3(config-if)#int f0/0
R3(config-if)#ipv6 address fe80::3 link-local
R3(config-if)#int f0/1
R3(config-if)#ipv6 address fe80::3 link-local

R2#ping fe80::3
Output Interface: FastEthernet0/1

R2#sh ipv6 neighbors
``` 
> ## Static Route
```
PC1(config)#ipv6 route ::/0 2001:db8::1
PC2(config)#ipv6 route ::/0 2001:db8:0:3::1

R2(config)#ipv6 route 2001:db::/64 2001:db8:0:1::1

R1(config)#ipv6 unicast-routing 
R2(config)#ipv6 unicast-routing 
R3(config)#ipv6 unicast-routing 

R1(config)#ipv6 route 2001:db8:0:2::/64 2001:db8:0:1::2
R1(config)#ipv6 route 2001:db8:0:3::/64 2001:db8:0:1::2

R2(config)#ipv6 route 2001:db8::/64 2001:db8:0:1::1
R2(config)#ipv6 route 2001:db8:0:3::/64 2001:db8:0:2::1

ipv6 route 2001:db8:0:1::/64 2001:db8:0:2::2
ipv6 route 2001:db8::/64 2001:db8:0:2::2
```
