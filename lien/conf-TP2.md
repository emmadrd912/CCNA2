- 🌞 conf du switch 1 : trunk effectué et vlan autorisé sur chaque port correspondant :

```
SW1#show interfaces trunk

Port        Mode             Encapsulation  Status        Native vlan
Et0/0       on               802.1q         trunking      1
Et0/3       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Et0/0       10,20,30,40
Et0/3       10,20,30,40

Port        Vlans allowed and active in management domain
Et0/0       10,20,30,40
Et0/3       10,20,30,40

Port        Vlans in spanning tree forwarding state and not pruned
Et0/0       10,20,30,40
Et0/3       10,20,30,40
```

```
SW1#show vlan
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et1/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                              Et3/0, Et3/1, Et3/2, Et3/3
10   vlan10-client                    active    Et0/1
20   vlan20-client                    active    Et0/2
30   vlan30-client                    active
40   vlan40-client                    active
```

- 🌞 conf du switch 2 :

```
SW2#show interfaces trunk

Port        Mode             Encapsulation  Status        Native vlan
Et0/0       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Et0/0       10,20,30,40

Port        Vlans allowed and active in management domain
Et0/0       10,20,30,40

Port        Vlans in spanning tree forwarding state and not pruned
Et0/0       10,20,30,40
```

```
SW2#show vlan
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et1/0, Et1/1, Et1/2, Et1/3
                                                Et2/0, Et2/1, Et2/2, Et2/3
                                                Et3/0, Et3/1, Et3/2, Et3/3
10   vlan10-client                    active
20   vlan20-client                    active    Et0/1
30   vlan30-client                    active    Et0/3
40   vlan40-client                    active    Et0/2
```

- 🌞 conf du switch router R1 :
