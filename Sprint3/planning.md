RCOMP 2021-2022 Project - Sprint 3 planning
===========================================
### Sprint master: 1201550 Eduardo Rocha ###
(This file is to be created/edited by the sprint master only)
# 1. Sprint's backlog #
T.3.1 Update the building1.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 1.  
T.3.2 Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 2. Final integration of each member’s Packet Tracer simulation into a single simulation.  
T.3.3 Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 3.  
T.3.4 Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 4.    
T.3.5 Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 5.

# 2. Technical decisions and coordination #

During the sprint planning meeting, the team established:

* The OSPF area ids to be used on each building:

| Building | OSPF Area ID |
| :------: | :----------: |
| Building 1 |1|
| Building 2 |2|
| Building 3 |3|
| Building 4 |4|
| Backbone   |0|

* VoIP phone numbers and prefix digits schema

| Building | Prefix Digits Schema |
| :------: | :----------: |
| Building 1 |2...|
| Building 2 |9...|
| Building 3 |3...|
| Building 4 |4...|
| Building 5 |7...|



* DNS Domain Names

| Building | DNS Domain Name |
| :------: | :----------: |
| Building 1 |rcomp-21-22-df-g4|
| Building 2 |building-2.rcomp-21-22-df-g4|
| Building 3 |building-3.rcomp-21-22-df-g4|
| Building 4 |building-4.rcomp-21-22-df-g4|
| Building 5 |building-5.rcomp-21-22-df-g4|

* NS (Name Server) records

| Building | DNS Name Server |
| :------: | :----------: |
| Building 1 |ns.rcomp-20-21-di-g3|
| Building 2 |ns.building-2.rcomp-21-22-df-g4|
| Building 3 |ns.building-3.rcomp-21-22-df-g4|
| Building 4 |ns.building-4.rcomp-21-22-df-g4|
| Building 5 |ns.building-5.rcomp-21-22-df-g4|

* The IPv4 node address of the DNS name server of each DNS domain

| Building | IPv4 node address |
| :------: | :----------: |
| Building 1 |172.17.33.2|
| Building 2 |172.17.36.162|
| Building 3 |172.17.37.194|
| Building 4 |172.17.38.130|
| Building 5 |172.17.39.131|

IPv4 node address of the DNS name server per building

| Network | DHCP Pool name |
|:---:|:---:|
| BuildingX_GF | XFIRST/XGROUND |
| BuildingX_FF | XSECOND | 
| BuildingX_WIFI | XWIFI |
| BuildingX_VOIP | XVoIP |  

where X represents the building number
