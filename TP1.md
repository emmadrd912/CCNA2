
# TP1 : Back to basics #


## I. Gather informations ##


- Récupérer la liste des cartes réseaux avec leur nom, leur IP et leur adresse MAC :

	```
	[emmadrd912@localhost ~]$ ip a

	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000

	link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

	inet 127.0.0.1/8 scope host lo

	valid_lft forever preferred_lft forever

	inet6 ::1/128 scope host

	valid_lft forever preferred_lft forever

	2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

	link/ether 08:00:27:25:12:53 brd ff:ff:ff:ff:ff:ff

	inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3

	valid_lft 85413sec preferred_lft 85413sec

	inet6 fe80::ed40:af4e:b1e5:101a/64 scope link noprefixroute

	valid_lft forever preferred_lft forever

	3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

	link/ether 08:00:27:df:08:e4 brd ff:ff:ff:ff:ff:ff

	inet 192.168.115.15/24 brd 192.168.115.255 scope global noprefixroute enp0s8

	valid_lft forever preferred_lft forever

	inet6 fe80::a00:27ff:fedf:8e4/64 scope link

	valid_lft forever preferred_lft forever

	```
- Déterminer si les cartes réseaux ont récupéré une IP en DHCP ou non :

	- La carte enp0s3 a pris une IP avec DHCP avec bail DHCP :

		```

		DHCP4.OPTION[1]: domain_name = auvence.co

		DHCP4.OPTION[2]: domain_name_servers = 10.33.10.20 10.33.10.2 8.8.>

		DHCP4.OPTION[3]: expiry = 1569568876

		DHCP4.OPTION[4]: ip_address = 10.0.2.15

		```

- Afficher la table de routage de la machine et sa table ARP :

	- Table de routage :

		```

		[emmadrd912@localhost etc]$ ip route

		default via 10.0.2.2 dev enp0s3 proto dhcp metric 100

		10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100

		192.168.115.0/24 dev enp0s8 proto kernel scope link src 192.168.115.15 metric 101

		```

		- cette route est celle de la carte enp0s3, elle est utilisée pour une connexion externe, la passerelle de cette route est à l'IP 10.0.2.0

		- cette route est celle de la carte enp0s8, elle est utilisée pour une connexion locale, la passerelle de cette route est à l'IP 192.168.115.0

	- Table ARP :

		```

		10.0.2.2 dev enp0s3 lladdr 52:54:00:12:35:02 STALE

		192.168.115.1 dev enp0s8 lladdr 0a:00:27:00:00:03 DELAY

		```

		- cette route est celle de la carte enp0s3, elle est utilisée pour une connexion locale, la passerelle de cette route est à l'IP 10.0.2.2

		- cette route est celle de la carte enp0s8, elle est utilisée pour une connexion externe, la passerelle de cette route est à l'IP 192.168.115.0

- Récupérer la liste des ports en écoute (listening) sur la machine (TCP et UDP) :

	```

	[emmadrd912@localhost etc]$ ss -lntu

	Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port

	udp UNCONN 0 0 127.0.0.1:323 0.0.0.0:*

	udp UNCONN 0 0 10.0.2.15%enp0s3:68 0.0.0.0:*

	udp UNCONN 0 0 [::1]:323 [::]:*

	tcp LISTEN 0 128 0.0.0.0:22 0.0.0.0:*

	tcp LISTEN 0 128 [::]:22 [::]:*

	```

- Récupérer la liste des DNS utilisés par la machine :

	```

	[emmadrd912@localhost etc]$ dig

	; <<>> DiG 9.11.4-P2-RedHat-9.11.4-17.P2.el8_0.1 <<>>

	;; global options: +cmd

	;; Got answer:

	;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 25765

	;; flags: qr rd ra ad; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 1

	  

	;; OPT PSEUDOSECTION:

	; EDNS: version: 0, flags:; udp: 4096

	;; QUESTION SECTION:

	;. IN NS

	  

	;; ANSWER SECTION:

	. 13741 IN NS m.root-servers.net.

	. 13741 IN NS b.root-servers.net.

	. 13741 IN NS f.root-servers.net.

	. 13741 IN NS a.root-servers.net.

	. 13741 IN NS h.root-servers.net.

	. 13741 IN NS j.root-servers.net.

	. 13741 IN NS g.root-servers.net.

	. 13741 IN NS e.root-servers.net.

	. 13741 IN NS i.root-servers.net.

	. 13741 IN NS k.root-servers.net.

	. 13741 IN NS l.root-servers.net.

	. 13741 IN NS d.root-servers.net.

	. 13741 IN NS c.root-servers.net.

	  

	;; Query time: 2 msec

	;; SERVER: 10.33.10.20#53(10.33.10.20)

	;; WHEN: Thu Sep 26 04:33:05 EDT 2019

	;; MSG SIZE rcvd: 239

	```

- Requête DNS de reddit :

	```

	[emmadrd912@localhost etc]$ dig www.reddit.com

	  

	; <<>> DiG 9.11.4-P2-RedHat-9.11.4-17.P2.el8_0.1 <<>> www.reddit.com

	;; global options: +cmd

	;; Got answer:

	;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63780

	;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 13, ADDITIONAL: 27

	  

	;; OPT PSEUDOSECTION:

	; EDNS: version: 0, flags:; udp: 4096

	;; QUESTION SECTION:

	;www.reddit.com. IN A

	  

	;; ANSWER SECTION:

	www.reddit.com. 5 IN CNAME reddit.map.fastly.net.

	reddit.map.fastly.net. 13 IN A 151.101.129.140

	reddit.map.fastly.net. 13 IN A 151.101.65.140

	reddit.map.fastly.net. 13 IN A 151.101.1.140

	reddit.map.fastly.net. 13 IN A 151.101.193.140

	  

	;; AUTHORITY SECTION:

	net. 172101 IN NS h.gtld-servers.net.

	net. 172101 IN NS l.gtld-servers.net.

	net. 172101 IN NS g.gtld-servers.net.

	net. 172101 IN NS a.gtld-servers.net.

	net. 172101 IN NS b.gtld-servers.net.

	net. 172101 IN NS f.gtld-servers.net.

	net. 172101 IN NS m.gtld-servers.net.

	net. 172101 IN NS i.gtld-servers.net.

	net. 172101 IN NS e.gtld-servers.net.

	net. 172101 IN NS c.gtld-servers.net.

	net. 172101 IN NS d.gtld-servers.net.

	net. 172101 IN NS j.gtld-servers.net.

	net. 172101 IN NS k.gtld-servers.net.

	  

	;; ADDITIONAL SECTION:

	a.gtld-servers.net. 172089 IN A 192.5.6.30

	a.gtld-servers.net. 172089 IN AAAA 2001:503:a83e::2:30

	m.gtld-servers.net. 172089 IN A 192.55.83.30

	m.gtld-servers.net. 172089 IN AAAA 2001:501:b1f9::30

	j.gtld-servers.net. 172089 IN A 192.48.79.30

	j.gtld-servers.net. 172089 IN AAAA 2001:502:7094::30

	k.gtld-servers.net. 172089 IN A 192.52.178.30

	k.gtld-servers.net. 172089 IN AAAA 2001:503:d2d::30

	f.gtld-servers.net. 172089 IN A 192.35.51.30

	f.gtld-servers.net. 172089 IN AAAA 2001:503:d414::30

	c.gtld-servers.net. 172089 IN A 192.26.92.30

	c.gtld-servers.net. 172089 IN AAAA 2001:503:83eb::30

	g.gtld-servers.net. 172089 IN A 192.42.93.30

	g.gtld-servers.net. 172089 IN AAAA 2001:503:eea3::30

	l.gtld-servers.net. 172089 IN A 192.41.162.30

	l.gtld-servers.net. 172089 IN AAAA 2001:500:d937::30

	b.gtld-servers.net. 172089 IN A 192.33.14.30

	b.gtld-servers.net. 172089 IN AAAA 2001:503:231d::2:30

	i.gtld-servers.net. 172089 IN A 192.43.172.30

	i.gtld-servers.net. 172089 IN AAAA 2001:503:39c1::30

	h.gtld-servers.net. 172089 IN A 192.54.112.30

	h.gtld-servers.net. 172089 IN AAAA 2001:502:8cc::30

	e.gtld-servers.net. 172089 IN A 192.12.94.30

	e.gtld-servers.net. 172089 IN AAAA 2001:502:1ca1::30

	d.gtld-servers.net. 172089 IN A 192.31.80.30

	d.gtld-servers.net. 172089 IN AAAA 2001:500:856e::30

	  

	;; Query time: 5 msec

	;; SERVER: 10.33.10.20#53(10.33.10.20)

	;; WHEN: Thu Sep 26 04:37:42 EDT 2019

	;; MSG SIZE rcvd: 935

	```

- Afficher l'état actuel du firewall :

	- Le firewall filtre les deux cartes réseaux :

	```

	[emmadrd912@localhost /]$ sudo firewall-cmd --list-all

	[sudo] password for emmadrd912:

	public (active)

	target: default

	icmp-block-inversion: no

	interfaces: enp0s3 enp0s8

	sources:

	services: cockpit dhcpv6-client ssh

	```

	- On peut voir que le firewall est actif sur les services. Les services ont des ports ouverts, donc les ports actif sur le firewall sont 9090 (cockpit),	22 (ssh), et 546 (dhcpv6-client).

## II. Edit configuration ##

  

### 1. Configuration cartes réseau ###

  

- Commande effectuée

- Changement de la carte réseau privée en IP statique sur enp0s8 :

```

[emmadrd912@localhost network-scripts]$ cat ifcfg-enp0s8

BOOTPROTO=static

IPADDR=192.168.115.15

NETMASK=255.255.255.0

NAME=enp0s8

DEVICE=enp0s8

ONBOOT=yes

```

  

- Nouvelle carte réseau ajoutée avec IP statique :

```

[emmadrd912@localhost network-scripts]$ cat ifcfg-enp0s9

BOOTPROTO=static

IPADDR=192.168.73.5

NETMASK=255.255.255.0

NAME=enp0s9

ONBOOT=yes

DEVICE=enp0s9

```

  
### 2. Serveur SSH ###

  

- Modification du serveur sur le port 2222 :

  

```

[emmadrd912@localhost network-scripts]$ sudo firewall-cmd --list-all

[sudo] password for emmadrd912:

public (active)

target: default

icmp-block-inversion: no

interfaces: enp0s10 enp0s3 enp0s8 enp0s9

sources:

services: cockpit dhcpv6-client ssh

ports: 2222/tcp

protocols:

masquerade: no

forward-ports:

source-ports:

icmp-blocks:

rich rules:

```

- Le port tourne maintenant sur le port 2222.
- Capture wireshark sur la connexion ssh du client au serveur :

[Wireshark capture ici](http://git.ynov-bordeaux.com/emmadrd912/CCNA/blob/master/lien/capture_ssh_client_serveur.pcapng)


## III. Routage simple ##

  

-            +-------+
                   |Outside|
                   | world |
                   +---+---+
                       |
                       |
+-------+         +----+---+         +-------+
|       |   net1  |        |   net2  |       |
|  VM1  +---------+ Router +---------+  VM2  |
|       |         |        |         |       |
+-------+         +--------+         +-------+


  

- Tableau récapitulatif des IP :

| routeur 1 | 192.168.115.254 | 192.168.215.254 |

|    vm 1   | 192.168.115.15  |        x        |

|    vm 2   |        x        | 192.168.215.15  |

  

- Configuration de VM1 :


```

[emmadrd912@localhost ~]$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000

link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

inet 127.0.0.1/8 scope host lo

valid_lft forever preferred_lft forever

inet6 ::1/128 scope host

valid_lft forever preferred_lft forever

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 08:00:27:25:12:53 brd ff:ff:ff:ff:ff:ff

inet 192.168.115.15/24 brd 192.168.115.255 scope global dynamic noprefixroute enp0s3

valid_lft 85413sec preferred_lft 85413sec

inet6 fe80::ed40:af4e:b1e5:101a/64 scope link noprefixroute

valid_lft forever preferred_lft forever

```

```

[emmadrd912@localhost network-scripts]$ cat ifcfg-enp0s3

BOOTPROTO=static

IPADDR=192.168.115.15

NETMASK=255.255.255.0

NAME=enp0s3

ONBOOT=yes

DEVICE=enp0s3

```

```

[emmadrd912@localhost network-scripts]$ ip route

default via 192.168.115.254 dev enp0s3 proto static metric 100

192.168.215.0/24 via 192.168.115.254 dev enp0s3 proto static metric 100

192.168.115.0/24 dev enp0s3 proto kernel scope link src 192.168.115.15 metric 100

```

  

- Configuration de VM2 :

  

```

[emmadrd912@localhost ~]$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000

link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

inet 127.0.0.1/8 scope host lo

valid_lft forever preferred_lft forever

inet6 ::1/128 scope host

valid_lft forever preferred_lft forever

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 08:00:27:25:12:53 brd ff:ff:ff:ff:ff:ff

inet 192.168.215.15/24 brd 192.168.215.255 scope global dynamic noprefixroute enp0s3

valid_lft 85413sec preferred_lft 85413sec

inet6 fe80::ed40:af4e:b1e5:101a/64 scope link noprefixroute

valid_lft forever preferred_lft forever

```

  

```

[emmadrd912@localhost network-scripts]$ cat ifcfg-enp0s3

BOOTPROTO=static

IPADDR=192.168.215.15

NETMASK=255.255.255.0

NAME=enp0s3

ONBOOT=yes

DEVICE=enp0s3

```

  

```

[emmadrd912@localhost network-scripts]$ ip route

default via 192.168.215.254 dev enp0s3 proto static metric 100

192.168.215.0/24 dev enp0s3 proto kernel scope link src 192.168.215.15 metric 100

192.168.115.0/24 via 192.168.215.254 dev enp0s3 proto static metric 100

```

  

## IV. Autres applications et métrologie ##

  

## 1. Commandes ##

  

- La commande iftop permet d'afficher la liste des connexions réseaux sous forme de bande passante (on voit leur débit).

  

## 2. Cockpit ##

  

- Après l'installation, on vérifie le port sur lequel écoute cockpit et on l'ajoute au pare-feu :

```

LISTEN 0 128 *:9090 *:* users:(("cockpit-ws",pid=6642,fd=3),("systemd",pid=1,fd=85))

```

```

[emmadrd912@localhost ]$ firewall-cmd --permanent --add-port=9090/tcp

```

  

### 3. Netdata ###