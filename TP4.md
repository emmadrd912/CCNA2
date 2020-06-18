
## TP4 : TP4 : Buffet à volonté ##

### I. Sujet global - Topologie ###

- Voici la configuration des 3 switchs :

```
client-sw1 :
!
interface Ethernet0/0
 switchport access vlan 10
 switchport mode access
!
interface Ethernet0/1
 switchport access vlan 20
 switchport mode access
!
interface Ethernet1/1
  switchport trunk encapsulation dot1q
  switchport mode trunk
!
```

```
client-sw2  :
!
interface Ethernet0/0
 switchport access vlan 10
 switchport mode access
!
interface Ethernet0/1
 switchport access vlan 20
 switchport mode access
!
interface Ethernet1/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet1/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet1/3
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
```

```
client-sw3 :
!
interface Ethernet0/0
 switchport access vlan 10
 switchport mode access
!
interface Ethernet0/1
 switchport access vlan 20
 switchport mode access
!
interface Ethernet0/2
 switchport access vlan 20
 switchport mode access
!
!
interface Ethernet1/3
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
!
```

- Configuration de l'infra-sw1 :

```
!
interface Ethernet1/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet0/0
 switchport access vlan 30
 switchport mode access
!
interface Ethernet0/1
 switchport access vlan 30
 switchport mode access
!
```

- Configuration du routeur :

```
!
interface Ethernet1/0.30
 encapsulation dot1Q 30
 ip address 10.5.30.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
interface Ethernet1/2.10
 encapsulation dot1Q 10
 ip address 10.5.10.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
interface Ethernet1/2.20
 encapsulation dot1Q 20
 ip address 10.5.20.254 255.255.255.0
 ip nat inside
 ip virtual-reassembly
!
```

- Ping de admin1 à admin2 :

```
admin1> ping 10.5.10.12
84 bytes from 10.5.10.12 icmp_seq=1 ttl=64 time=0.779 ms
84 bytes from 10.5.10.12 icmp_seq=2 ttl=64 time=0.821 ms
84 bytes from 10.5.10.12 icmp_seq=3 ttl=64 time=0.969 ms
84 bytes from 10.5.10.12 icmp_seq=4 ttl=64 time=1.089 ms
```

- Pour la mise en place du DHCP et du DNS, j'ai récupéré tes exemples de conf.
  - Voici un exemple de ping de guest1 à guest2 (dns) :

```
guest1> ping guest2
guest2.tp4.b2 resolved to 10.5.20.11
84 bytes from 10.5.20.11 icmp_seq=1 ttl=64 time=0.739 ms
84 bytes from 10.5.20.11 icmp_seq=2 ttl=64 time=0.639 ms
84 bytes from 10.5.20.11 icmp_seq=3 ttl=64 time=0.838 ms
84 bytes from 10.5.20.11 icmp_seq=4 ttl=64 time=0.737 ms
```

### II. Anonymat en ligne ###

#### Proxy HTTP ####

- 🌞 Lancez Wireshark et observez le trafic émis lors d'un trafic utilisant un proxy HTTP, puis un proxy HTTPS.
  - Pour une connexion en site HTTP ou HTTPS, on peut remarquer que l'adresse de destination devient l'adresse du proxy.
  - La seule différence que j'ai remarqué est que lorsque on lance une requête HTTP, le protocole utilisé est HTTP et firefox va retourner un succes pour cette requête avec les informations de la requête (une section en plus lorsque qu'on clique sur la trame). Alors qu'en HTTPS, le protocole utilisé est le TCP est il n'y pas autant d'informations donnéés que lorsque une requête HTTP.

  - [Firefoxsuccess](https://github.com/emmadrd912/CCNA2/blob/master/lien/httpsuccess.png)

#### Tor Browser ####

- 🌞 Lancez Wireshark et observez le trafic émis lors d'un trafic utilisant le Tor Browser, comparé à une connexion classique.
  - Par rapport à une connexion classique, on remarque que l'adresse IP de destination est l'adresse IP de l'entry relay (de mon circuit). Le mien est situé en Allemagne.


#### Hidden service Tor ####

- 🌞 Lancez tcpdump sur la VM
  - On remarque que l'ip de destination n'est pas l'adresse Ip de notre machine.

#### DoH/DoT ####

- 🌞 Utilisez Wireshark pour déterminer la différence entre DNS classique et DoH.
  - J'ai configuré mon navigateur (firefox) pour utiliser le Doh avec cloudflare (par défaut sur firefox).
  - Avec DoH, une requête DNS vers mozilla.cloudflare.com vient s'ajouter à la suite de la première requête TCP.

#### Bilan ####

🌞 Faites un comparatif entre :

  - proxy HTTP
  - Tor
  - Tor hidden servie
  - DoH
  - VPN (vu l'année passée)


|              |Proxy    |Tor   |Hidden tor  |Doh  |VPN                      |
|--------------|---------|------|--------|-----|----|
|Confidentialité ?|Aucune|Oui|Oui|Oui|Oui
|Messages ? |Protocole HTTP - Traffic non chiffré|Protocole TLS/TCP - Traffic chiffré | Traffic chiffré - HTTPS| Protocole DNS - Traffic chiffré | Traffic chiffré
|Anonymat client |Aucune, l'ip du client devient celle du proxy|Oui, plusieurs connexion avec l'ip qui change (circuit)| Oui, on ne connait pas l'ip du client | Oui, l'ip client deviens celle des resolvers DNS | Oui, l'ip client devient celle du VPN (server)
|Anonymat server |Aucune|Aucune|Oui, on ne connait pas l'ip du server | Aucune | Aucune
