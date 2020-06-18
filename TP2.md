## TP2 : Network low-level, Switching ##

### I. Simplest setup ###

- 🌞 mettre en place la topologie : Topologie effectué
  - [Topologie1](https://github.com/emmadrd912/CCNA2/blob/master/lien/tp2-topologie1.PNG)
- 🌞 faire communiquer les deux PCs et 🌞 récapituler toutes les étapes (dans le compte-rendu, à l'écrit) quand PC1 exécute ping PC2 pour la première fois
	 - Ping effectué et réussi entre les deux machines :  

```
PC-2> ping 10.2.1.1
84 bytes from 10.2.1.1 icmp_seq=1 ttl=64 time=0.154 ms
84 bytes from 10.2.1.1 icmp_seq=2 ttl=64 time=0.206 ms
84 bytes from 10.2.1.1 icmp_seq=3 ttl=64 time=0.218 ms
84 bytes from 10.2.1.1 icmp_seq=4 ttl=64 time=0.347 ms
84 bytes from 10.2.1.1 icmp_seq=5 ttl=64 time=0.280 ms
```

  - Le protocole utilisé pour le ping est le ICMP. La capture suivante a été executé sur le PC1 qui faisait un ping sur le PC2.
    - [Wireshark_ICMP](https://github.com/emmadrd912/CCNA2/blob/master/lien/gns3-ping-tp2.PNG)
  - Affichage de la table ARP :  

```
PC-1> show arp
  00:50:79:66:68:01  10.2.1.2 expires in 106 seconds
```
```
PC-2> show arp
  00:50:79:66:68:00  10.2.1.1 expires in 43 seconds
```  

- 🌞 expliquer...
  - Le switch n'a pas besoin d'une IP car il est comme une multriprise il passe juste l'information.
  - Les machines ont besoin d'une IP pour pouvoir se ping car elles ont besoin de s'identifier.

### II. More switches ###

- 🌞 mettre en place la topologie ci-dessus : Topologie effectué
  - [Topologie2](https://github.com/emmadrd912/CCNA2/blob/master/lien/tp2-topologie2.PNG)
- 🌞 faire communiquer les trois PCs
  - ping du PC1 vers PC2 et PC3 :  

```  
PC-1> ping 10.2.2.2
84 bytes from 10.2.2.2 icmp_seq=1 ttl=64 time=0.232 ms
84 bytes from 10.2.2.2 icmp_seq=2 ttl=64 time=0.298 ms
84 bytes from 10.2.2.2 icmp_seq=3 ttl=64 time=0.315 ms
84 bytes from 10.2.2.2 icmp_seq=4 ttl=64 time=0.290 ms
84 bytes from 10.2.2.2 icmp_seq=5 ttl=64 time=0.317 ms

PC-1> ping 10.2.2.3
84 bytes from 10.2.2.3 icmp_seq=1 ttl=64 time=0.873 ms
84 bytes from 10.2.2.3 icmp_seq=2 ttl=64 time=0.409 ms
84 bytes from 10.2.2.3 icmp_seq=3 ttl=64 time=0.555 ms
84 bytes from 10.2.2.3 icmp_seq=4 ttl=64 time=0.352 ms
84 bytes from 10.2.2.3 icmp_seq=5 ttl=64 time=0.523 ms
```  

  - ping du PC2 vers PC1 et PC3 :  

```
PC-2> ping 10.2.2.1
84 bytes from 10.2.2.1 icmp_seq=1 ttl=64 time=0.365 ms
84 bytes from 10.2.2.1 icmp_seq=2 ttl=64 time=0.314 ms
84 bytes from 10.2.2.1 icmp_seq=3 ttl=64 time=0.319 ms
84 bytes from 10.2.2.1 icmp_seq=4 ttl=64 time=0.314 ms
84 bytes from 10.2.2.1 icmp_seq=5 ttl=64 time=0.305 ms

PC-2> ping 10.2.2.3
84 bytes from 10.2.2.3 icmp_seq=1 ttl=64 time=0.184 ms
84 bytes from 10.2.2.3 icmp_seq=2 ttl=64 time=0.310 ms
84 bytes from 10.2.2.3 icmp_seq=3 ttl=64 time=0.313 ms
84 bytes from 10.2.2.3 icmp_seq=4 ttl=64 time=0.331 ms
84 bytes from 10.2.2.3 icmp_seq=5 ttl=64 time=0.316 ms
```  

  - ping du PC3 vers PC1 et PC2 :  

```
PC-3> ping 10.2.2.1
84 bytes from 10.2.2.1 icmp_seq=1 ttl=64 time=0.495 ms
84 bytes from 10.2.2.1 icmp_seq=2 ttl=64 time=0.393 ms
84 bytes from 10.2.2.1 icmp_seq=3 ttl=64 time=0.407 ms
84 bytes from 10.2.2.1 icmp_seq=4 ttl=64 time=0.387 ms
84 bytes from 10.2.2.1 icmp_seq=5 ttl=64 time=0.316 ms

PC-3> ping 10.2.2.2
84 bytes from 10.2.2.2 icmp_seq=1 ttl=64 time=0.317 ms
84 bytes from 10.2.2.2 icmp_seq=2 ttl=64 time=0.309 ms
84 bytes from 10.2.2.2 icmp_seq=3 ttl=64 time=0.298 ms
84 bytes from 10.2.2.2 icmp_seq=4 ttl=64 time=0.315 ms
84 bytes from 10.2.2.2 icmp_seq=5 ttl=64 time=0.327 ms
```  

- 🌞 analyser la table MAC d'un switch :  

```
IOU19#show mac address-table
        Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0050.7966.6800    DYNAMIC     Et0/0
   1    0050.7966.6801    DYNAMIC     Et0/1
   1    0050.7966.6802    DYNAMIC     Et0/2
   1    aabb.cc00.0110    DYNAMIC     Et0/0
   1    aabb.cc00.0300    DYNAMIC     Et0/2
Total Mac Addresses for this criterion: 5
```  

  - La première adresse mac appartient au PC1 et communique par le port Et0/0
  - La deuxième adresse mac appartient au PC2 et communique par le port Et0/1
  - La troisième adresse mac appartient au PC3 et communique par le port Et0/2
  - Les deux dernières lignes affiche les adresses mac des autres switches avec les ports dont il communique.

- 🐙 en lançant Wireshark sur les liens des switches, il y a des trames CDP qui circulent. Quoi qu'est-ce ?
  - [Wireshak_CDP](https://github.com/emmadrd912/CCNA2/blob/master/lien/CPD-TP2.PNG)
  - Le CDP permet de voir les autres péripherique connectés, sur la capture wireshark, on peut voir l'adresse mac et le port avec le voisin qui communique avec lui.

#### Mise en évidence du Spanning Tree Protocol ####

- 🌞 déterminer les informations STP
  - Pour determiner les informations STP, on execute différentes commande qui permettent de voir les port ou voir qui est le root bridge.
  - Exemple sur le switch 3 (IOU20) :  

```
IOU20#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: none
Extended system ID                      is enabled
Portfast Default                        is disabled
Portfast Edge BPDU Guard Default        is disabled
Portfast Edge BPDU Filter Default       is disabled
Loopguard Default                       is disabled
PVST Simulation Default                 is enabled but inactive in rapid-pvst mode
Bridge Assurance                        is enabled
EtherChannel misconfig guard            is enabled
Configured Pathcost method used is short
UplinkFast                              is disabled
BackboneFast                            is disabled

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0001                     1         0        0         15         16
---------------------- -------- --------- -------- ---------- ----------
1 vlan                       1         0        0         15         16
IOU20#show spanning-tree

VLAN0001
Spanning tree enabled protocol rstp
Root ID    Priority    32769
           Address     aabb.cc00.0100
           Cost        100
           Port        3 (Ethernet0/2)
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
           Address     aabb.cc00.0300
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
           Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Altn BLK 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
Et1/0               Desg FWD 100       128.5    Shr
Et1/1               Desg FWD 100       128.6    Shr
Et1/2               Desg FWD 100       128.7    Shr
Et1/3               Desg FWD 100       128.8    Shr
Et2/0               Desg FWD 100       128.9    Shr
Et2/1               Desg FWD 100       128.10   Shr
Et2/2               Desg FWD 100       128.11   Shr
Et2/3               Desg FWD 100       128.12   Shr
Et3/0               Desg FWD 100       128.13   Shr
Et3/1               Desg FWD 100       128.14   Shr
Et3/2               Desg FWD 100       128.15   Shr
Et3/3               Desg FWD 100       128.16   Shr
```
  - Le root bridge est le switch 1(IOU18) et le port bloquer est le eth0/0  (ALT BLK).

```
IOU20#show spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.0100
             Cost        100
             Port        3 (Ethernet0/2)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.0300
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Altn BLK 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
Et1/0               Desg FWD 100       128.5    Shr
Et1/1               Desg FWD 100       128.6    Shr
Et1/2               Desg FWD 100       128.7    Shr
Et1/3               Desg FWD 100       128.8    Shr
Et2/0               Desg FWD 100       128.9    Shr
Et2/1               Desg FWD 100       128.10   Shr
Et2/2               Desg FWD 100       128.11   Shr
Et2/3               Desg FWD 100       128.12   Shr
Et3/0               Desg FWD 100       128.13   Shr
Et3/1               Desg FWD 100       128.14   Shr
Et3/2               Desg FWD 100       128.15   Shr
Et3/3               Desg FWD 100       128.16   Shr
```  

- 🌞 faire un schéma en représentant les informations STP
  - Le root bridge est le switch 1 (IOU18) sur la VLAN 1 :  

```
IOU18#show spanning-tree bridge                                                 Hello  Max  Fwd
Vlan                         Bridge ID              Time  Age  Dly  Protocol
---------------- --------------------------------- -----  ---  ---  --------
VLAN0001         32769 (32768,   1) aabb.cc00.0100    2    20   15  rstp
IOU18#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0001                         is disabled
```  

  - Le role des ports varient selon les ports :  

```
IOU18#show spanning-tree

VLAN0001
Spanning tree enabled protocol rstp
Root ID    Priority    32769
           Address     aabb.cc00.0100
           This bridge is the root
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
           Address     aabb.cc00.0100
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
           Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Desg FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
Et1/0               Desg FWD 100       128.5    Shr
Et1/1               Desg FWD 100       128.6    Shr
Et1/2               Desg FWD 100       128.7    Shr
Et1/3               Desg FWD 100       128.8    Shr
Et2/0               Desg FWD 100       128.9    Shr
Et2/1               Desg FWD 100       128.10   Shr
Et2/2               Desg FWD 100       128.11   Shr
Et2/3               Desg FWD 100       128.12   Shr
Et3/0               Desg FWD 100       128.13   Shr
Et3/1               Desg FWD 100       128.14   Shr
Et3/2               Desg FWD 100       128.15   Shr
Et3/3               Desg FWD 100       128.16   Shr
```  

  - Le role 'desg' est le port qui transmet les trames.

- 🌞 confirmer les informations STP
  - Les ping s'effectuent bien, le rapport entre le switch 2 et 3 est bloqué, desactivé donc cela passe.

- 🌞 faire un schéma qui explique le trajet d'une requête ARP lorsque PC1 ping PC3
  - pas trop compris comment faire un schema, ni réussi la capture wireshark

#### Reconfigurer STP ####

- 🌞 changer la priorité d'un switch qui n'est pas le root bridge et 🌞 vérifier les changements
  - Une fois la propriété du switch modfié, on peut voir que le switch 1 (IOU18) n'est plus le root bridge. Maintenant après ma configuration, le switch 2 (IOU19) est passé root bridge.  

```
IOU18#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: none
Extended system ID                      is enabled
Portfast Default       
```
```
IOU19#show spanning-tree summary
*Oct  8 17:54:30.487: %SYS-5-CONFIG_I: Configured from console by console
IOU19#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0001
```  

#### 🐙 STP & Perfs ####

- Mise en place fortfast et bpduguard :
  - L'interface ethernet 0/1 a bien été placé en port edge :  

```
IOU20#show spanning-tree vlan 1
VLAN0001
Spanning tree enabled protocol rstp
Root ID    Priority    4097
           Address     aabb.cc00.0100
           Cost        100
           Port        3 (Ethernet0/2)
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

Bridge ID  Priority    4097   (priority 4096 sys-id-ext 1)
           Address     aabb.cc00.0300
           Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
           Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Altn BLK 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr Edge
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
```  

- 🐙 ToDo :
  - bpduguard et Portfast déjà mis en place au dessus.
  - Désactivation de l'envoi de trames CDP fait

### III. Isolation ###

- 🌞 mettre en place la topologie ci-dessus avec des VLANs (IP aussi configurée) :  
   [Topologie3](https://github.com/emmadrd912/CCNA2/blob/master/lien/tp2-topologie3.PNG)

```
IOU19#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client-network                   active    Et0/0
20   client-network20                 active    Et0/1, Et0/2
```  

- 🌞 faire communiquer les PCs deux à deux :
  - vérifier que PC2 ne peut joindre que PC3 : (Il ne ping que PC3)  

```
PC-2> ping 10.2.3.3
84 bytes from 10.2.3.3 icmp_seq=1 ttl=64 time=0.111 ms
84 bytes from 10.2.3.3 icmp_seq=2 ttl=64 time=0.194 ms
84 bytes from 10.2.3.3 icmp_seq=3 ttl=64 time=0.186 ms
84 bytes from 10.2.3.3 icmp_seq=4 ttl=64 time=0.192 ms
84 bytes from 10.2.3.3 icmp_seq=5 ttl=64 time=0.196 ms

PC-2> ping 10.2.3.1
host (10.2.3.1) not reachable
```  

  - vérifier que PC1 ne peut joindre personne alors qu'il est dans le même réseau (sad)
    - Il ne peut communiquer avec personne  

```
PC-1> ping 10.2.3.2
host (10.2.3.2) not reachable

PC-1> ping 10.2.3.3
host (10.2.3.3) not reachable
```

#### 2. Avec trunk ####

- 🌞 mettre en place la topologie ci-dessus :
  [Topologie4](https://github.com/emmadrd912/CCNA2/blob/master/lien/tp2-topologie4.PNG)
  - Configuration du switch1 avec la VLAN 10 et VLAN 20 :  

```
SW1#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/1, Et0/3, Et1/0, Et1/1
                                                Et1/2, Et1/3, Et2/0, Et2/1
                                                Et2/2, Et2/3, Et3/0, Et3/1
                                                Et3/2, Et3/3
10   client-network10                 active    Et0/0
20   client-network20                 active    Et0/2
```  

  - Configuration du switch2 avec la VLAN 10 et VLAN 20 :  

```
SW2#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/3, Et1/0, Et1/1, Et1/2
                                                Et1/3, Et2/0, Et2/1, Et2/2
                                                Et2/3, Et3/0, Et3/1, Et3/2
                                                Et3/3
10   client-network10                 active    Et0/1
20   client-network20                 active    Et0/2
```  

- 🌞 faire communiquer les PCs deux à deux
  - vérifier que PC1 ne peut joindre que PC3 (PC1 peut joindre que la vlan 10)  

```
PC-1> ping 10.2.10.2
84 bytes from 10.2.10.2 icmp_seq=1 ttl=64 time=0.203 ms
84 bytes from 10.2.10.2 icmp_seq=2 ttl=64 time=0.349 ms
84 bytes from 10.2.10.2 icmp_seq=3 ttl=64 time=0.316 ms
84 bytes from 10.2.10.2 icmp_seq=4 ttl=64 time=0.332 ms
84 bytes from 10.2.10.2 icmp_seq=5 ttl=64 time=0.342 ms

PC-1> ping 10.2.20.1
No gateway found

PC-1> ping 10.2.20.2
No gateway found
```  

  - vérifier que PC4 ne peut joindre que PC2 (PC4 peut joindre que la vlan 20)  

```
PC-4> ping 10.2.20.1
84 bytes from 10.2.20.1 icmp_seq=1 ttl=64 time=0.193 ms
84 bytes from 10.2.20.1 icmp_seq=2 ttl=64 time=0.312 ms
84 bytes from 10.2.20.1 icmp_seq=3 ttl=64 time=0.388 ms
84 bytes from 10.2.20.1 icmp_seq=4 ttl=64 time=0.335 ms
84 bytes from 10.2.20.1 icmp_seq=5 ttl=64 time=0.354 ms

PC-4> ping 10.2.10.1
No gateway found

PC-4> ping 10.2.10.2
No gateway found
```  

### IV. Need Perfs ###

- 🌞 mettre en place la topologie ci-dessus
  [Topologie5](https://github.com/emmadrd912/CCNA2/blob/master/lien/tp2-topologie5.PNG)
  - configurer LACP entre SW1 et SW2  

```
SW1#show etherchannel
                Channel-group listing:
                ----------------------

Group: 1
----------
Group state = L2
Ports: 1   Maxports = 4
Port-channels: 1 Max Port-channels = 4
Protocol:   LACP
Minimum Links: 0
```
```

SW2#show etherchannel
                Channel-group listing:
                ----------------------

Group: 1
----------
Group state = L2
Ports: 1   Maxports = 4
Port-channels: 1 Max Port-channels = 4
Protocol:   LACP
Minimum Links: 0
```  

    - Ping qui marche pour les PC qui sont dans la même VLAN.
  - vérifier avec un show ip interface po1 que la bande passante a bien été doublée

```
SW1#show ip int po1
Port-channel1 is up, line protocol is up
Inbound  access list is not set
Outgoing access list is not set
```

    - Mon LACP doit être mal configuré avec cette réponse, triste
