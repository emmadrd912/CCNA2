## TP2 : Network low-level, Switching ##

### I. Router-on-a-stick ###

- Setup this shit : fait
- 🌞 Prove me that your setup is actually working
  - Net1 ne peut joindre personne :

```
PC-1> ping 1.3.20.2
*10.3.10.254 icmp_seq=1 ttl=255 time=9.655 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=2 ttl=255 time=5.741 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=3 ttl=255 time=5.541 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=4 ttl=255 time=5.403 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=5 ttl=255 time=5.338 ms (ICMP type:3, code:1, Destination host unreachable)

PC-1> ping 1.3.20.3
*10.3.10.254 icmp_seq=1 ttl=255 time=9.847 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=2 ttl=255 time=5.379 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=3 ttl=255 time=5.841 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=4 ttl=255 time=5.762 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=5 ttl=255 time=7.357 ms (ICMP type:3, code:1, Destination host unreachable)

PC-1> ping 1.3.30.4
*10.3.10.254 icmp_seq=1 ttl=255 time=5.724 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=2 ttl=255 time=6.280 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=3 ttl=255 time=5.486 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=4 ttl=255 time=6.817 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=5 ttl=255 time=5.489 ms (ICMP type:3, code:1, Destination host unreachable)

PC-1> ping 1.3.40.1
*10.3.10.254 icmp_seq=1 ttl=255 time=6.989 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=2 ttl=255 time=7.314 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=3 ttl=255 time=5.625 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=4 ttl=255 time=5.901 ms (ICMP type:3, code:1, Destination host unreachable)
*10.3.10.254 icmp_seq=5 ttl=255 time=5.590 ms (ICMP type:3, code:1, Destination host unreachable)
```

  - Net2 peut joindre net2, net3 et netp :

```
PC-2> ping 10.3.20.3
84 bytes from 10.3.20.3 icmp_seq=1 ttl=64 time=0.208 ms
84 bytes from 10.3.20.3 icmp_seq=2 ttl=64 time=0.294 ms
84 bytes from 10.3.20.3 icmp_seq=3 ttl=64 time=0.296 ms
84 bytes from 10.3.20.3 icmp_seq=4 ttl=64 time=0.317 ms
84 bytes from 10.3.20.3 icmp_seq=5 ttl=64 time=0.300 ms

PC-2> ping 10.3.30.4
10.3.30.4 icmp_seq=1 timeout
84 bytes from 10.3.30.4 icmp_seq=2 ttl=63 time=11.338 ms
84 bytes from 10.3.30.4 icmp_seq=3 ttl=63 time=19.462 ms
84 bytes from 10.3.30.4 icmp_seq=4 ttl=63 time=11.301 ms
84 bytes from 10.3.30.4 icmp_seq=5 ttl=63 time=15.971 ms

PC-2> ping 10.3.40.1
10.3.40.1 icmp_seq=1 timeout
84 bytes from 10.3.40.1 icmp_seq=2 ttl=63 time=16.003 ms
84 bytes from 10.3.40.1 icmp_seq=3 ttl=63 time=17.277 ms
84 bytes from 10.3.40.1 icmp_seq=4 ttl=63 time=19.873 ms
84 bytes from 10.3.40.1 icmp_seq=5 ttl=63 time=11.771 ms
```

  - Net3 peut joindre net2, net3 et netp :

```
PC-4> ping 10.3.20.2
10.3.20.2 icmp_seq=1 timeout
10.3.20.2 icmp_seq=2 timeout
84 bytes from 10.3.20.2 icmp_seq=3 ttl=63 time=14.013 ms
84 bytes from 10.3.20.2 icmp_seq=4 ttl=63 time=15.954 ms
84 bytes from 10.3.20.2 icmp_seq=5 ttl=63 time=16.417 ms

PC-4> ping 10.3.20.3
10.3.20.3 icmp_seq=1 timeout
10.3.20.3 icmp_seq=2 timeout
84 bytes from 10.3.20.3 icmp_seq=3 ttl=63 time=18.866 ms
84 bytes from 10.3.20.3 icmp_seq=4 ttl=63 time=15.848 ms
84 bytes from 10.3.20.3 icmp_seq=5 ttl=63 time=16.364 ms

PC-4> ping 10.3.40.1
10.3.40.1 icmp_seq=1 timeout
10.3.40.1 icmp_seq=2 timeout
84 bytes from 10.3.40.1 icmp_seq=3 ttl=63 time=16.250 ms
84 bytes from 10.3.40.1 icmp_seq=4 ttl=63 time=15.296 ms
84 bytes from 10.3.40.1 icmp_seq=5 ttl=63 time=13.277 ms
```

  - NetP peut joindre net2, net3 et netp :

```
P1> ping 10.3.20.2
10.3.20.2 icmp_seq=1 timeout
10.3.20.2 icmp_seq=2 timeout
84 bytes from 10.3.20.2 icmp_seq=3 ttl=63 time=19.414 ms
84 bytes from 10.3.20.2 icmp_seq=4 ttl=63 time=17.372 ms
84 bytes from 10.3.20.2 icmp_seq=5 ttl=63 time=16.122 ms

P1> ping 10.3.20.3
10.3.20.3 icmp_seq=1 timeout
10.3.20.3 icmp_seq=2 timeout
84 bytes from 10.3.20.3 icmp_seq=3 ttl=63 time=16.487 ms
84 bytes from 10.3.20.3 icmp_seq=4 ttl=63 time=15.343 ms
84 bytes from 10.3.20.3 icmp_seq=5 ttl=63 time=16.161 ms

P1> ping 10.3.30.4
10.3.30.4 icmp_seq=1 timeout
10.3.30.4 icmp_seq=2 timeout
84 bytes from 10.3.30.4 icmp_seq=3 ttl=63 time=12.426 ms
84 bytes from 10.3.30.4 icmp_seq=4 ttl=63 time=15.667 ms
84 bytes from 10.3.30.4 icmp_seq=5 ttl=63 time=16.216 ms
```

### II. Cas concret ###

- SETUP this in GNS3 :
  [Setup-Infra](https://github.com/emmadrd912/CCNA2/blob/master/lien/TP3-infrasolo.PNG)

- Toutes les configurations sont [ICI](https://github.com/emmadrd912/CCNA2/blob/master/confCisco/confCiscoTP3.md)

- Tableau d'adressage :

| Nom          | Vlan10  | Vlan20 | Vlan30 |  Vlan40 |  Vlan50 | Vlan60 |  
| ---------------  |:-------------------:| :-----:| :-----:| :-----:|:-----:| :-----:|
| U1 à U16     | 10.3.10.1 à 10.3.10.16 | x | x | x | x | x |
| S1 à S8      | x   | 10.3.20.1 à 10.3.20.8 | x | x | x | x | x |
| P1 à P5      | x | x | 10.3.30.1 à 10.3.30.5 | x | x | x |
| A1 à A3      | x | x | x | 10.3.40.1 à 10.3.40.3 | x | x |
| SRV2 à SRV5 | x  | x | x | x | 10.3.50.2 à 10.3.50.5 | x |
| SRV1 et SRV6 | x  | x | x | x | x | 10.3.60.1 et 10.3.60.6|

- Toutes les réseaux sont en /24, c'est énorme mais si plus tard on veut ajouter de nouvelles machines, on pourra. L'infra que j'ai proposé est composé de 6 switchs, un pour chaque salle et un central permattant de les relier entre eux et lié à un routeur. Les swicths sont composés de 16 adapteurs ce qui assure l'ajout de machine si on veut en rajouter. Le routeur est composé de 2 ports, un pour le NAT et un pour le switch central. L'infra est composé de 6 VLAN, chaque vlan est répartie par catégorie (admin, stagiaires, user ...) sauf pour les serveurs où il y a deux vlans, une pour les serveurs normaux et une pour les serveurs sensibles par sécurité.

- Pour que chaque vlan de chaque salle communique entre elles, il suffisait de faire des trunks pour permettre les vlans de passer, mais cela faisait que chaque vlan pouvait ping que sa propre vlan et non les autres. Pour pouvoir faire cela, il suffit de configurer le routeur avec des sous interfaces, cela permet de ping tout le monde, n'importe quelle vlan mais grâce au VLAN access-list, on peut définir qui communique avec qui et donc bloquer certaines communication.

- Pour le cablage, il y aura en tout 46 câbles.
  - 39 câbles moyens (chaque users, stagiares ... relié à son switch)
  - 6 câbles long (reliant les switchs entre eux)
  - 1 câble court (reliant le NAT au routeur)

- Afficher quelque ping pour montrer que ça marche en montrant qui a accès a qui.
  - Pour l'instant, je ping toutes les vlans malgrès les restrictions du VLAN access-list.  

```
U1> ping 10.3.40.1
84 bytes from 10.3.40.1 icmp_seq=1 ttl=63 time=32.737 ms
84 bytes from 10.3.40.1 icmp_seq=2 ttl=63 time=19.458 ms
84 bytes from 10.3.40.1 icmp_seq=3 ttl=63 time=21.077 ms
84 bytes from 10.3.40.1 icmp_seq=4 ttl=63 time=12.848 ms
84 bytes from 10.3.40.1 icmp_seq=5 ttl=63 time=20.350 ms

U1> ping 10.3.50.1
10.3.50.1 icmp_seq=1 timeout
10.3.50.1 icmp_seq=2 timeout
10.3.50.1 icmp_seq=3 timeout
10.3.50.1 icmp_seq=4 timeout
10.3.50.1 icmp_seq=5 timeout

U1> ping 10.3.60.1
84 bytes from 10.3.60.1 icmp_seq=1 ttl=63 time=31.651 ms
84 bytes from 10.3.60.1 icmp_seq=2 ttl=63 time=16.133 ms
84 bytes from 10.3.60.1 icmp_seq=3 ttl=63 time=11.864 ms
84 bytes from 10.3.60.1 icmp_seq=4 ttl=63 time=20.479 ms
84 bytes from 10.3.60.1 icmp_seq=5 ttl=63 time=16.057 ms

U1> ping 10.3.50.2
84 bytes from 10.3.50.2 icmp_seq=1 ttl=63 time=31.253 ms
84 bytes from 10.3.50.2 icmp_seq=2 ttl=63 time=19.853 ms
84 bytes from 10.3.50.2 icmp_seq=3 ttl=63 time=19.857 ms
84 bytes from 10.3.50.2 icmp_seq=4 ttl=63 time=16.443 ms
84 bytes from 10.3.50.2 icmp_seq=5 ttl=63 time=17.085 ms
```
