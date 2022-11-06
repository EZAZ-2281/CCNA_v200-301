> # Cisco DHCP Client  
```
R1
int f0/0
ip address dhcp
no shut
!
sh ip int brief
!
sh dhcp lease
!
```
> # Cisco DHCP Server    
```
R1
ip dhcp excluded-address 10.10.10.1 10.10.10.10 
ip dhcp pool Dhaka
default-router 10.10.10.1
dns-server 10.10.20.10
network 10.10.10.0 255.255.255.0
!
PC1
ipconfig /all
ping dnsserver
!
R1
sh ip dhcp binding
!
R1
no ip dhcp excluded-address 10.10.10.1 10.10.10.10
no ip dhcp pool Dhaka
!
PC1
ipconfig /release
ipconfig /renew
```
> # External DHCP Server  
```
R1
int f0/1
ip helper-address 10.10.20.10
!
PC1
ipconfig /all
!
```
