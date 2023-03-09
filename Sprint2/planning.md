#RCOMP 2021-2022 Project 2DF_04 - Sprint 2 planning
### Sprint master: 1200882
# 1. Sprint's backlog
| Tasks | Task description                          | Student assignation |
|-------|-------------------------------------------|---------------------|
| T.2.1 | Development of the network of building 1. | 1201549             |
| T.2.2 | Development of the network of building 2. | 1200882             |
| T.2.3 | Development of the network of building 3. | 1201550             |
| T.2.4 | Development of the network of building 4. | 1201021             |
| T.2.5 | Development of the network of building 5. | 1201183             |
# 2. Building/Name of devices
* Ex. (4Laptop0)
* Laptop0
* Desktop0
* Access Point 0
* Server 0
* HCGroundFloor
* IC
* Router
* IP Phone 0
* Consolidation Point 0
* Laptop1
* Desktop1
* Access Point 1
* Server 1
* HC1Floor
* IP Phone 1
* Consolidation Point 1

# 3. BUILDING 1
* VLANID-VLAN_NAME-IPv4-MASK
* 280 - BackBone - 172.17.32.0 - 255.255.255.128
* 281 - Floor Zero - 172.17.34.0 - 255.255.255.192
* 282 - Floor one - 172.17.32.128 - 255.255.255.128
* 283 - WIFI - 172.17.33.128 - 255.255.255.128
* 284 - DMZ - 173.17.33.0 - 255.255.255.128
* 285 - VoIP - 172.17.34.64 - 255.255.255.192
# 4. BUILDING 2
* VLANID-VLAN_NAME-IPv4-MASK
* 286 - GroundFloor - 172.17.36.129 - 255.255.255.224
* 287 - FirstFloor - 172.17.36.193 - 255.255.255.192
* 288 - WIFIVLAN - 172.17.36.1 - 255.255.255.128
* 289 - DMZVLAN - 172.17.36.161 - 255.255.255.240
* 290 - IPVLAN - 172.17.36.177 - 255.255.255.240
# 5. BUILDING 3
* VLANID-VLAN_NAME-IPv4-MASK
* 291 - FIRST_FLOOR - 172.17.37.1 - 255.255.255.192
* 292 - SECOND_FLOOR - 172.17.37.65 - 255.255.255.192
* 293 - WIFI - 172.17.37.129 - 255.255.255.192
* 294 - DMZ - 172.17.37.193 - 255.255.255.224
* 295 - VoIP - 172.17.37.225 - 255.255.255.224
# 6. BUILDING 4
* VLANID-VLAN_NAME-IPv4-MASK
* 296 - GroundFloor - 172.17.38.161 - 255.255.255.224
* 297 - FirstFloor - 172.17.38.193 - 255.255.255.192
* 298 - Wifi - 172.17.38.1 - 255.255.255.128
* 299 - DMZ - 172.17.38.129 - 255.255.255.240
* 300 - VoIP - 172.17.38.145 - 255.255.255.240
# 7. BUILDING 5
* VLANID-VLAN_NAME-IPv4-MASK
* 301 - 5WIFI - 172.17.39.193 - 255.255.255.192
* 302 - 5FirstFloor - 172.17.39.1 - 255.255.255.192
* 303 - 5VOIP - 172.17.39.161 - 255.255.255.224
* 304 - 5GroundFloor - 172.17.39.65 - 255.255.255.192
* 305 - 5DMZ - 172.17.39.129 - 255.255.255.224

# 8. VTP Domain Name
- rc22dfg4

# 9. ISP router IPv4
* IP - 15.203.47.125
* Mask - 255.255.255.252