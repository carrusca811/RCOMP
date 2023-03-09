RCOMP 2021-2022 Project - Sprint 3 - Eduardo Rocha 121550
===========================================

# Edifício 3#

## DNS Databases Records ##

![1190967_DNS_Table](./images/dns.PNG)

---

## IPv4 Networks Relativas ao Edifício 1 e Campus Backbone ##

![IPv4Networks](./imgs/1190967_IPv4Networks.png)

| VLAN Location|  VLAN ID   |     Network IP    | Default Gateway |
| ------------ | ---------- | ----------------- | --------------- |
|   First Floor    |    291     | 172.17.37.0| 172.17.37.1  |
|   Second floor    |    292     | 172.17.37.64   | 172.17.37.65   |
|   Wi-fi     |    293    | 172.17.37.128  | 172.17.37.129   |
|   DMZ	       |    294     | 172.17.37.192   | 172.17.37.193  |
|   VoIP       |    295     | 172.17.37.224 | 172.17.37.225  |


## Configurations & Commands

#### OSPF (Open Shortest Path First)

  - **Router(config)#** router ospf 3
  - **Router(config)#** network 172.17.32.0 0.0.0.127 area 0
  - **Router(config)#** network 172.17.37.0 0.0.0.255 area 3


-------------------------------------------------------------------

#### HTTP Server



![HTML.PNG](./images/html-page.PNG)



-------------------------------------------------------------------

#### DHCPv4 Service

* Floor 0:
    - **Router(config)#** ip dhcp pool 3FIRST
    - **Router(config)#** network 172.17.37.0 255.255.255.192
    - **Router(config)#** default-router 172.17.37.1
    - **Router(config)#** dns-server 172.17.37.194
    - **Router(config)#** domain-name rcomp-21-22-df-g4
* Floor 1:
    - **Router(config)#** ip dhcp pool 3SECOND
    - **Router(config)#** network 172.17.37.64 255.255.255.192
    - **Router(config)#** default-router 172.17.37.65
    - **Router(config)#** dns-server 172.17.37.194
    - **Router(config)#** domain-name rcomp-21-22-df-g4
* WiFi:
    - **Router(config)#** ip dhcp pool 3Wifi
    - **Router(config)#** network 172.17.37.128 255.255.255.224
    - **Router(config)#** default-router 172.17.37.129
    - **Router(config)#** dns-server 172.17.37.194
    - **Router(config)#** domain-name rcomp-21-22-df-g4
* VoIP:
    - **Router(config)#** ip dhcp pool 3VoIP
    - **Router(config)#** network 172.17.37.224 255.255.255.224
    - **Router(config)#** default-router 172.17.37.225
    - **Router(config)#** option 150 ip 172.17.37.225
    - **Router(config)#** dns-server 172.17.37.194
    - **Router(config)#** domain-name rcomp-21-22-df-g4

![DHCP.PNG](./imgs/DHCP.PNG)

-------------------------------------------------------------------

* Foi garantido que os gateway adresses foram excluidos da pool:
    - **Router(config)#** ip dhcp excluded-address 172.17.37.1
    - **Router(config)#** ip dhcp excluded-address 172.17.37.65
    - **Router(config)#** ip dhcp excluded-address 172.17.37.129
    - **Router(config)#** ip dhcp excluded-address 10.124.229.1
    - **Router(config)#** ip dhcp excluded-address 172.17.37.193

-------------------------------------------------------------------

#### VoIP Service

- Os VoIP phones foram adicionados à network e podem comunicar um com o outro.
    - **Router(config)#** telephony-service
    - **BC-Router(config-telephony)#** ip source-address 10.124.229.193 port 3000
    - **BC-Router(config-telephony)#** max-ephones 20
    - **BC-Router(config-telephony)#** max-dn 20
    - **BC-Router(config-telephony)#** exit
    - **BC-Router(config)#** ephone-dn 11
    - **BC-Router(config-ephone-dn)#** number 3001
    - **BC-Router(config-ephone-dn)#** exit
    - **BC-Router(config)#** ephone-dn 12
    - **BC-Router(config-ephone-dn)#** number 3002
    - **BC-Router(config-ephone-dn)#** exit


-------------------------------------------------------------------

- A imagem a baixo mostra o telemovel direito a comunicar com o telefone esquerdo.

![VOIP.PNG](./images/VOIP.PNG)

-------------------------------------------------------------------

#### NAT

- **Router(config)#** ip nat inside source static tcp 172.17.37.195 80 172.17.32.3 80
- **Router(config)#** ip nat inside source static tcp 172.17.37.195 443 172.17.32.3 443
- **Router(config)#** ip nat inside source static tcp 172.17.37.194 53 172.17.32.3 53
- **Router(config)#** ip nat inside source static udp 172.17.37.194 53 172.17.32.3 53


-------------------------------------------------------------------

#### Firewall

- Firewall Commands:
- **Router(config)#** ip access-list extended anti-spoof
- **Router(config)#** deny ip 10.0.0.0 0.255.255.255 any
- **Router(config)#** deny ip 172.16.0.0 0.15.255.255 any
- **Router(config)#** deny ip 192.168.0.0 0.0.255.255 any
- **Router(config)#**  deny ip 224.0.0.0 31.255.255.255 any
- **Router(config)#**  deny ip 127.0.0.0 0.255.255.255 any
- **Router(config)#**  deny ip 169.254.0.0 0.0.255.255 any
- **Router(config)#**  deny ip 172.17.37.0 0.0.0.255 any
- **Router(config)#**  permit ip any any
- **Router(config)#**  ip access-list extended BUILDING3_PCS
- **Router(config)#**  permit icmp 172.17.37.0 0.0.0.255 any echo
- **Router(config)#**  permit icmp 172.17.37.0 0.0.0.255 any echo-reply
- **Router(config)#**  permit ip 172.17.37.0 0.0.0.255 any
- **Router(config)#**  permit udp any any eq bootps
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.195 eq www
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.195 eq 443
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.194 eq domain
- **Router(config)#**  permit udp 172.17.37.0 0.0.0.255 host 172.17.37.194 eq domain
- **Router(config)#**  deny ip any 172.17.37.0 0.0.0.255
- **Router(config)#**  ip access-list extended INTERNET
- **Router(config)#**  deny ip 172.17.37.0 0.0.0.255 any
- **Router(config)#**  permit icmp any 172.17.37.0 0.0.0.255 echo
- **Router(config)#**  permit icmp any 172.17.37.0 0.0.0.255 echo-reply
- **Router(config)#**  deny ip any 172.17.37.0 0.0.0.255
- **Router(config)#**  permit tcp any host 172.17.37.195 eq www
- **Router(config)#**  permit tcp any host 172.17.37.195 eq 443
- **Router(config)#**  permit tcp any host 172.17.37.194 eq domain
- **Router(config)#**  permit udp any host 172.17.37.194 eq domain
- **Router(config)#**  permit ip any any
- **Router(config)#**  ip access-list extended BUILDING3_VOIP
- **Router(config)#**  permit icmp 172.17.37.0 0.0.0.255 any echo
- **Router(config)#**  permit icmp 172.17.37.0 0.0.0.255 any echo-reply
- **Router(config)#**  permit ip 172.17.37.0 0.0.0.255 any
- **Router(config)#**  permit udp any any eq bootps
- **Router(config)#**  permit udp any any eq tftp
- **Router(config)#**  permit tcp any host 172.17.37.225 eq 3000
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.195 eq www
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.195 eq 443
- **Router(config)#**  permit tcp 172.17.37.0 0.0.0.255 host 172.17.37.194 eq domain
- **Router(config)#**  permit udp 172.17.37.0 0.0.0.255 host 172.17.37.194 eq domain
- **Router(config)#**  deny ip any 172.17.37.0 0.0.0.255


-------------------------------------------------------------------

