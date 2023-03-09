RCOMP 2021-2022 Project - Sprint 3 - Member 1200882 folder
===========================================
(This folder is to be created/edited by the team member 1200882 only)

# Edifício 2#

## DNS Databases Records ##

![1200882_DNS_Table](dns_table_building2.PNG)


### IP Subnetting

 As decisões de IP Subnetting podem ser consultadas no README.md file do Sprint2.

-------------------------------------------------------------------

| VLAN ID |	VLAN Name| Network in CIDR Notation 	|	Network’s First Valid Node Address |	Network’s Last Valid Node Address |	Network Mask |	Broadcast Address |
|---|---|---|---|---|---|---|
|220 |		BB		|	10.124.224.0/25		|	10.124.224.1			|	10.124.224.126			|255.255.255.128	| 10.124.224.127	|
|286 |		2Ground	|	172.17.36.128/27		|	172.17.36.129			|	172.17.36.159			|255.255.255.224	|	172.17.36.160	|
|287 |		2First	|	172.17.36.192/26	|	172.17.36.193			|	172.17.36.239			|255.255.255.192	|	172.17.36.240	|
|288 |		2Wifi	|	172.17.36.0/25		|	172.17.36.1			|	172.17.36.11		|255.255.255.128	|	172.17.36.120	|
|289 |		2DMZ	|	172.17.36.160/28	|	172.17.36.161			|	172.17.36.175			|255.255.255.240	|	172.17.36.176	|
|290 |		2VoIP	|	172.117.36.176/28	|	172.17.36.177			|	172.17.36.191			|255.255.255.240	|	172.17.36.192	|

-------------------------------------------------------------------

## Configurations & Commands

#### OSPF (Open Shortest Path First)

-
    - router ospf 2
    - network 172.17.32.0 0.0.0.127 area 0
    - network 172.17.36.0 0.0.1.255 area 2
	

-------------------------------------------------------------------

#### HTTP Server

- Um novo servidoror foi adicionado ao piso 1 (datacenter) como server de HTTP server para a network. Foi adicionado à DMZ network. O HTML foi criado para ter o seguinte aspeto: 

![HTML.PNG](html.PNG)


-------------------------------------------------------------------

#### DHCPv4 Service

- DHCP  foi adicionado a todos os local networks, mudando os defenidos estaticamente.
* Floor 0
	- **Router(config)#** ip dhcp pool 2Ground
	- **Router(config)#** network 172.17.36.128 255.255.255.224
	- **Router(config)#** default-router 172.17.36.129
	- **Router(config)#** dns-server 172.17.36.162
	- **Router(config)#** domain-name building-2.rcomp-21-22-df-g4
* Floor 1:
	- **Router(config)#** ip dhcp pool 2First
    - **Router(config)#** network 172.17.36.192 255.255.255.192
    - **Router(config)#** default-router 172.17.36.193
    - **Router(config)#** dns-server 172.17.36.162
    - **Router(config)#** domain-name building-2.rcomp-21-22-df-g4
* WiFi:
	 - **Router(config)#** ip dhcp pool 2Wifi
     - **Router(config)#** network 172.17.36.0 255.255.255.128
    - **Router(config)#** default-router 172.17.36.1
    - **Router(config)#** dns-server 172.17.36.162
    - **Router(config)#** domain-name building-2.rcomp-21-22-df-g4
* VoIP:
	- **Router(config)#** ip dhcp pool 2VoIP
	- **Router(config)#** network 172.17.36.176 255.255.255.240
	- **Router(config)#** default-router 172.17.36.177
	- **Router(config)#** option 150 ip 172.17.36.177
	- **Router(config)#** dns-server 172.17.36.177
	- **Router(config)#** domain-name building-2.rcomp-21-22-df-g4

![DHCP.PNG](dhcp.PNG)
-------------------------------------------------------------------

#### VoIP Service

- Os VoIP phones foram adicionados à network e podem comunicar um com o outro,todos os comandos encontram-se em baixo:
	- **Router(config)#** telephony-service
	- **Router(config)#** max-ephones 20
    - **Router(config)#** max-20
	- **BC-Router(config-telephony)#** ip source-address 172.17.36.177 port 2000
	- **BC-Router(config-telephony)#** auto assign 11 to 12
	- **BC-Router(config-telephony)#** exit
	- **BC-Router(config)#** ephone-dn 11
	- **BC-Router(config-ephone-dn)#** number 9998
	- **BC-Router(config-ephone-dn)#** exit
	- **BC-Router(config)#** ephone-dn 12
	- **BC-Router(config-ephone-dn)#** number 9999
	- **BC-Router(config-ephone-dn)#** exit
	- **BC-Router(config)#** ephone 5
	- **BC-Router(config-ephone-dn)#** mac-address 0090.0C4C.A84D
	- **BC-Router(config-ephone-dn)#** type 7960
	- **BC-Router(config-ephone-dn)#** button 1:11
	- **BC-Router(config-ephone-dn)#** exit
	- **BC-Router(config)#** ephone 3
	- **BC-Router(config-ephone-dn)#** mac-address 0006.2A4D.2C73
	- **BC-Router(config-ephone-dn)#** type 7960
	- **BC-Router(config-ephone-dn)#** button 1:12
	- **BC-Router(config-ephone-dn)#** exit	
	
	
-------------------------------------------------------------------

- A imagem a baixo mostra o telemovel esquerdo a comunicar com o telefone direito.Como indicado pela seta vermelha, o telefone esquerdo esta a receber uma chamada do **9999**.O telefone direito esta a fazer uma chamada do **9998**. 

![VOIP.PNG](voip.PNG)

-------------------------------------------------------------------

#### NAT

- Static NAT was used to redirect traffic, and the commands below were used for this purpose:
	- **Router(config)#** ip nat inside source static tcp 172.17.36.163 80 172.17.32.2 80
	- **Router(config)#** ip nat inside source static tcp 172.17.36.163 443 172.17.32.2 443
	- **Router(config)#** ip nat inside source static tcp 172.17.36.162 53 172.17.32.2 53
	- **Router(config)#** ip nat inside source static udp 172.17.36.162 53 172.17.32.2 53

-------------------------------------------------------------------
#### FIREWALL
- ip access-list extended anti-spoof
- deny ip 10.0.0.0 0.255.255.255 any
- deny ip 172.16.0.0 0.15.255.255 any
- deny ip 192.168.0.0 0.0.255.255 any
- deny ip 224.0.0.0 31.255.255.255 any
- deny ip 127.0.0.0 0.255.255.255 any
- deny ip 169.254.0.0 0.0.255.255 any
- deny ip 172.17.36.0 0.0.1.255 any
- permit ip any any
- ip access-list extended BUILDING2_PCS
- permit icmp 172.17.36.0 0.0.1.255 any echo
- permit icmp 172.17.36.0 0.0.1.255 any echo-reply
- permit ip 172.17.36.0 0.0.0.255 any
- permit udp any any eq bootps
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.163 eq www
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.163 eq 443
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.162 eq domain
- permit udp 172.17.36.0 0.0.1.255 host 172.17.36.162 eq domain
- deny ip any 172.17.36.0 0.0.0.255
- ip access-list extended INTERNET
- deny ip 172.17.36.0 0.0.1.255 any
- permit icmp any 172.17.36.0 0.0.1.255 echo
- permit icmp any 172.17.36.0 0.0.1.255 echo-reply
- deny ip any 172.17.36.0 0.0.0.255
- permit tcp any host 172.17.36.163 eq www
- permit tcp any host 172.17.36.163 eq 443
- permit tcp any host 172.17.36.162 eq domain
- permit udp any host 172.17.36.162 eq domain
- permit ip any any
- ip access-list extended BUILDING2_VOIP
- permit icmp 172.17.36.0 0.0.1.255 any echo
- permit icmp 172.17.36.0 0.0.1.255 any echo-reply
- permit ip 172.17.36.0 0.0.0.255 any
- permit udp any any eq bootps
- permit udp any any eq tftp
- permit tcp any host 172.17.36.177 eq 2000
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.163 eq www
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.163 eq 443
- permit tcp 172.17.36.0 0.0.1.255 host 172.17.36.162 eq domain
- permit udp 172.17.36.0 0.0.1.255 host 172.17.36.162 eq domain
- deny ip any 172.17.36.0 0.0.0.255
