## Conf TP3 partie 2 ##

- SW1

```
conf t
interface ethernet 0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,30,40,50,60
exit
interface ethernet 0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50
exit
interface ethernet 0/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50
exit
interface ethernet 0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
interface ethernet 1/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
interface ethernet 1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
exit
```

- SW2

```
conf t
vlan 50
name server
exit
vlan 60
name server-ss
exit
interface ethernet 0/1
switchport mode access
switchport access vlan 60
exit
interface ethernet 0/2
switchport mode access
switchport access vlan 50
exit
interface ethernet 0/3
switchport mode access
switchport access vlan 50
exit
interface ethernet 1/0
switchport mode access
switchport access vlan 50
exit
interface ethernet 1/2
switchport mode access
switchport access vlan 60
exit
interface ethernet 1/1
switchport mode access
switchport access vlan 50
exit
interface ethernet 0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,30,40,50,60
exit
exit
```

- SW3

```
conf t
vlan 10
name users
exit
vlan 20
name stagiaires
exit
vlan 30
name imprimantes
exit
interface ethernet 0/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 0/2
switchport mode access
switchport access vlan 10
exit
interface ethernet 0/3
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/1
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/2
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/3
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/0
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/1
switchport mode access
switchport access vlan 30
exit
interface ethernet 0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50
exit
exit
```

- SW4

```
conf t
vlan 10
name users
exit
vlan 20
name stagiaires
exit
vlan 30
name imprimantes
exit
vlan 40
name admin
exit
interface ethernet 0/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 0/1
switchport mode access
switchport access vlan 20
exit
interface ethernet 0/3
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/1
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/2
switchport mode access
switchport access vlan 40
exit
interface ethernet 1/3
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/0
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/1
switchport mode access
switchport access vlan 30
exit
interface ethernet 0/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50
exit
exit
```

- SW5

```
conf t
vlan 10
name users
exit
vlan 20
name stagiaires
exit
vlan 30
name imprimantes
exit
vlan 40
name admin
exit
interface ethernet 0/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 0/1
switchport mode access
switchport access vlan 40
exit
interface ethernet 0/2
switchport mode access
switchport access vlan 30
exit
interface ethernet 1/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/1
switchport mode access
switchport access vlan 20
exit
interface ethernet 1/2
switchport mode access
switchport access vlan 10
exit
interface ethernet 1/3
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 2/1
switchport mode access
switchport access vlan 20
exit
interface ethernet 2/2
switchport mode access
switchport access vlan 10
exit
interface ethernet 2/3
switchport mode access
switchport access vlan 30
exit
interface ethernet 3/0
switchport mode access
switchport access vlan 10
exit
interface ethernet 0/3
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
exit
```

- SW6

```
conf t
vlan 30
name imprimantes
exit
vlan 40
name admin
exit
interface ethernet 0/0
switchport mode access
switchport access vlan 30
exit
interface ethernet 0/1
switchport mode access
switchport access vlan 40
exit
interface ethernet 1/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60
exit
exit
```

- R1

```
conf t
interface ethernet 1/3.10
encapsulation dot1q 10
ip address 10.3.10.254 255.255.255.0
exit
interface ethernet 1/3.20
encapsulation dot1q 20
ip address 10.3.20.254 255.255.255.0
exit
interface ethernet 1/3.30
encapsulation dot1q 30
ip address 10.3.30.254 255.255.255.0
exit
interface ethernet 1/3.40
encapsulation dot1q 40
ip address 10.3.40.254 255.255.255.0
exit
interface ethernet 1/3.50
encapsulation dot1q 50
ip address 10.3.50.254 255.255.255.0
exit
interface ethernet 1/3.60
encapsulation dot1q 60
ip address 10.3.60.254 255.255.255.0
exit
interface ethernet 1/3
no shut
exit
exit
```

```
conf t
access-list 100 permit ip 10.3.10.0 0.0.0.255 any
access-list 100 permit ip 10.3.20.0 0.0.0.255 any
access-list 100 permit ip 10.3.40.0 0.0.0.255 any
access-list 100 permit ip 10.3.50.0 0.0.0.255 any
access-list 100 permit ip 10.3.60.0 0.0.0.255 any
interface ethernet 1/3
ip access-group 100 in
exit
exit
```
