RCOMP 2021-2022 Project - Sprint 3 - João Oliveira 1201183
===========================================

# Edifício 5#

## DNS Databases Records ##

![dns_table](dns_table.PNG)

---

## IPv4 Networks Relativas ao Edifício 1 e Campus Backbone ##


| VLAN Location|  VLAN ID   |     Network IP    | Default Gateway |
| ------------ | ---------- | ----------------- | --------------- |
|   Ground Floor    |    304     | 172.17.39.64| 172.17.39.65  |
|   First floor    |    302     | 172.17.39.0   | 172.17.39.1   |
|   Wi-fi     |    301    | 172.17.39.192  | 172.17.39.193   |
|   DMZ	       |    305     | 172.17.39.128   | 172.17.39.129  |
|   VoIP       |    303     | 172.17.39.160 | 172.17.39.161  |


## Configurations & Commands

#### OSPF (Open Shortest Path First)

- As rotas estaticas foram apagadas da routing table e o OSPF foi feito para o router do edificio 5.
  - **Router(config)#** router ospf 5
  - **Router(config)#** network 172.17.32.0 0.0.0.127 area 0
  - **Router(config)#** network 172.17.39.128 0.0.0.1 area 5
  
  
-------------------------------------------------------------------

#### HTTP Server



![html](html.PNG)



-------------------------------------------------------------------

#### DHCPv4 Service

* Wifi:

 ip dhcp pool 5WIFI
 network 172.17.39.192 255.255.255.192
 default-router 172.17.39.193
 dns-server 172.17.39.131
 domain-name building-5.rcomp-21-22-df-g4

* Floor 1:
 ip dhcp pool 5FirstFloor
 network 172.17.39.0 255.255.255.192
 default-router 172.17.39.1
 dns-server 172.17.39.131
 domain-name building-5.rcomp-21-22-df-g4


* VOIP:
 ip dhcp pool 5VOIP
 network 172.17.39.160 255.255.255.224
 default-router 172.17.39.161
 dns-server 172.17.39.131
 domain-name building-5.rcomp-21-22-df-g4
* Floor 0:
 ip dhcp pool 5GroundFloor
 network 172.17.39.64 255.255.255.192
 default-router 172.17.39.65
 dns-server 172.17.39.131
 domain-name building-5.rcomp-21-22-df-g4


-------------------------------------------------------------------

* Foi garantido que os gateway adresses foram excluidos da pool:
    - ip dhcp excluded-address 172.17.39.65
    -  ip dhcp excluded-address 172.17.39.1
    -  ip dhcp excluded-address 172.17.39.193
    -  ip dhcp excluded-address 172.17.39.129
    -  ip dhcp excluded-address 172.17.39.161
-------------------------------------------------------------------

#### VoIP Service

- Os VoIP phones foram adicionados à network e podem comunicar um com o outro.
    - telephony-service
       max-ephones 20
       max-dn 20
       ip source-address 172.17.39.162 port 2000
       auto assign 11 to 12
      !
      ephone-dn 11
       number 7001
      !
      ephone-dn 12
       number 7002
      !
      ephone 5
       device-security-mode none
       mac-address 0001.9734.0435
       type 7960
       button 1:11
      !
      ephone 3
       device-security-mode none
       mac-address 0001.637E.2DA1
       type 7960
       button 1:12

Aqui esta demonstrada a ligação entre os telemoveis com estas imagens
![phone_who_calls](phone_who_calls.PNG)
![phone_who_receives](phone_who_receives.PNG)


*
-------------------------------------------------------------------



-------------------------------------------------------------------

#### NAT

- ip nat inside source static tcp 172.17.39.132 80 172.17.32.5 80 
- ip nat inside source static tcp 172.17.39.132 443 172.17.32.5 443 
-  ip nat inside source static tcp 172.17.39.131 53 172.17.32.5 53 
-  ip nat inside source static udp 172.17.39.131 53 172.17.32.5 53 


-------------------------------------------------------------------

#### Firewall

ip access-list extended anti-spoof
 deny ip 10.0.0.0 0.255.255.255 any
 deny ip 172.16.0.0 0.15.255.255 any
 deny ip 192.168.0.0 0.0.255.255 any
 deny ip 224.0.0.0 31.255.255.255 any
 deny ip 127.0.0.0 0.255.255.255 any
 deny ip 169.254.0.0 0.0.255.255 any
 deny ip 172.17.39.128 0.0.0.1 any
 permit ip any any
ip access-list extended BUILDING5_PCS
 permit icmp 172.17.39.0 0.0.0.1 any echo
 permit icmp 172.17.39.0 0.0.0.1 any echo-reply
 permit ip 172.17.39.0 0.0.0.1 any
 permit udp any any eq bootps
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.132 eq www
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.132 eq 443
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.131 eq domain
 permit udp 172.17.39.0 0.0.0.1 host 172.17.39.131 eq domain
 deny ip any 172.17.39.0 0.0.0.255
ip access-list extended INTERNET
 deny ip 172.17.39.0 0.0.1.255 any
 permit icmp any 172.17.39.0 0.0.0.1 echo
 permit icmp any 172.17.39.0 0.0.0.1 echo-reply
 deny ip any 172.17.39.0 0.0.0.1
 permit tcp any host 172.17.39.132 eq www
 permit tcp any host 172.17.39.132 eq 443
 permit tcp any host 172.17.39.131 eq domain
 permit udp any host 172.17.39.131 eq domain
 permit ip any any
ip access-list extended BUILDING5_VOIP
 permit icmp 172.17.39.0 0.0.0.1 any echo
 permit icmp 172.17.39.0 0.0.0.1 any echo-reply
 permit ip 172.17.39.0 0.0.0.1 any
 permit udp any any eq bootps
 permit udp any any eq tftp
 permit tcp any host 172.17.39.161 eq 2000
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.132 eq www
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.132 eq 443
 permit tcp 172.17.39.0 0.0.0.1 host 172.17.39.131 eq domain
 permit udp 172.17.39.0 0.0.0.1 host 172.17.39.131 eq domain
 deny ip any 172.17.39.0 0.0.0.255

-------------------------------------------------------------------

