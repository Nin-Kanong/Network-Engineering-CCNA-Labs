<h1 align="center"> LAB: 4.3.8 - Cinfigure Layer3 Switching And Inter VLAN Routing </h1>


---


## Lab Guide




---


## Addressing Table


| Device | Interface | IP Address / Prefix |
| :--- | :--- | :--- |
| **MLS** | VLAN 10 | `192.168.10.254 /24` |
| **MLS** | VLAN 10 | `2001:db8:acad:10::1/64` |
| **MLS** | VLAN 20 | `192.168.20.254 /24` |
| **MLS** | VLAN 20 | `2001:db8:acad:20::1/64` |
| **MLS** | VLAN 30 | `192.168.30.254/24` |
| **MLS** | VLAN 30 | `2001:db8:acad:30::1/64` |
| **MLS** | VLAN 99 | `192.168.99.254/24` |
| **MLS** | G0/2 | `209.165.200.225` |
| **MLS** | G0/2 | `2001:db8:acad:a::1/64` |
| **PC0** | NIC | `192.168.10.1` |
| **PC1** | NIC | `192.168.20.1` |
| **PC2** | NIC | `192.168.30.1` |
| **PC3** | NIC | `192.168.10.2/24` |
| **PC3** | NIC | `2001:db8:acad:10::2/64` |
| **PC4** | NIC | `192.168.20.2/24` |
| **PC4** | NIC | `2001:db8:acad:20::2/64` |
| **PC5** | NIC | `192.168.30.2` |
| **PC5** | NIC | `2001:db8:acad:30::2/64` |
| **S1** | VLAN 99 | `192.168.99.1` |
| **S2** | VLAN 99 | `192.168.99.2` |
| **S3** | VLAN 99 | `192.168.99.3` |


---



## Lab Walkkthrough


<img width="1107" height="618" alt="image" src="https://github.com/user-attachments/assets/baf8b7f9-531f-44d2-95bd-fa5e1dd106a8" />




---



### Part 1: Configure Layer 3 Switching

In this part, we will configure MLS ``G0/2`` as a routed port and test connectivity to the Cloud.

Click on **MLS** -> **CLI**, press **Enter**.


**Enter privileged EXEC mode:**
````
MLS> enable
MLS# configure terminal
````


#### Configure G0/2 as a routed port:

A multilayer switch normally uses switchports for Layer 2 switching. The ``no switchport`` command converts ``G0/2`` into a Layer 3 routed interface.

````
MLS(config)# interface gigabitEthernet 0/2
MLS(config-if)# no switchport
MLS(config-if)# ip address 209.165.200.225 255.255.255.252
MLS(config-if)# no shutdown
MLS(config-if)# exit
MLS(config)# end
````


| Command | Purpose |
| :--- | :--- |
| `no switchport` | Converts the port into a Layer 3 routed interface |
| `ip address` | Assigns the IPv4 address |
| `no shutdown` | Enables the interface |

---


#### Verify the routed interface
````
MLS# show ip interface brief
````

<img width="657" height="455" alt="image" src="https://github.com/user-attachments/assets/5591ff31-4306-44b7-a956-951b8d3328be" />


Now it show `up`.


#### Test connectivity to cloud
On **MLS**, run:
````
ping 209.165.200.226
````

**Output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 209.165.200.226, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms
````

> Now **MLS** can communicate with the Cloud through its directly connected network.

---



### Part 2: Configure Inter-VLAN Routing


#### Step 1: Add VLANs.
In this we will add **VLANs** on **MLS**.


Open **MLS** -> **CLI**, then enter:
````
MLS> enable
MLS# configure terminal
````


##### Create VLAN 10
````
MLS(config)# vlan 10
MLS(config-vlan)# name staff
MLS(config-vlan)# exit
````

##### Create VLAN 20
````
MLS(config)# vlan 20
MLS(config-vlan)# name Student
MLS(config-vlan)# exit
````

##### Create VLAN 30
````
MLS(config)# vlan 30
MLS(config-vlan)# name Faculty
MLS(config-vlan)# exit
````


##### Create VLAN 99
````
MLS(config)# vlan 99
MLS(config-vlan)# name Management
MLS(config-vlan)# exit
````


##### Verify:
````
MLS(config)# end
MLS# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1
10   staff                            active    
20   Student                          active    
30   Faculty                          active    
99   Management                       active    
999  VLAN0999                         active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
````

Now we see all our VLAN that we was created.


---



#### Configure SVIs on MLS

An **SVI (Switched Virtual Interface)** gives a VLAN its own Layer 3 IP address.


````
MLS> enable
MLS# configure terminal
````

##### Configure VLAN 10

````
MLS(config)# interface vlan 10
MLS(config-if)# ip address 192.168.10.254 255.255.255.0
MLS(config-if)# no shutdown
MLS(config-if)# exit
````

##### Configure VLAN 20
````
MLS(config)# interface vlan 20
MLS(config-if)# ip address 192.168.20.254 255.255.255.0
MLS(config-if)# no shutdown
MLS(config-if)# exit
````


##### Configure VLAN 30

````
MLS(config)# interface vlan 30
MLS(config-if)# ip address 192.168.30.254 255.255.255.0
MLS(config-if)# no shutdown
MLS(config-if)# exit
````




##### Configure VLAN 99

````
MLS(config)# interface vlan 99
MLS(config-if)# ip address 192.168.99.254 255.255.255.0
MLS(config-if)# no shutdown
MLS(config-if)# exit
````


##### Exit and Verify
````
MLS(config)# end
MLS# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES unset  down                  down 
FastEthernet0/2        unassigned      YES unset  down                  down 
FastEthernet0/3        unassigned      YES unset  down                  down 
FastEthernet0/4        unassigned      YES unset  down                  down 
FastEthernet0/5        unassigned      YES unset  down                  down 
FastEthernet0/6        unassigned      YES unset  down                  down 
FastEthernet0/7        unassigned      YES unset  down                  down 
FastEthernet0/8        unassigned      YES unset  down                  down 
FastEthernet0/9        unassigned      YES unset  down                  down 
FastEthernet0/10       unassigned      YES unset  down                  down 
FastEthernet0/11       unassigned      YES unset  down                  down 
FastEthernet0/12       unassigned      YES unset  down                  down 
FastEthernet0/13       unassigned      YES unset  down                  down 
FastEthernet0/14       unassigned      YES unset  down                  down 
FastEthernet0/15       unassigned      YES unset  down                  down 
FastEthernet0/16       unassigned      YES unset  down                  down 
FastEthernet0/17       unassigned      YES unset  down                  down 
FastEthernet0/18       unassigned      YES unset  down                  down 
FastEthernet0/19       unassigned      YES unset  down                  down 
FastEthernet0/20       unassigned      YES unset  down                  down 
FastEthernet0/21       unassigned      YES unset  down                  down 
FastEthernet0/22       unassigned      YES unset  down                  down 
FastEthernet0/23       unassigned      YES unset  down                  down 
FastEthernet0/24       unassigned      YES unset  down                  down 
GigabitEthernet0/1     unassigned      YES unset  up                    up 
GigabitEthernet0/2     209.165.200.225 YES manual up                    up 
Vlan1                  unassigned      YES unset  administratively down down 
Vlan10                 192.168.10.254  YES manual up                    down 
Vlan20                 192.168.20.254  YES manual up                    down 
Vlan30                 192.168.30.254  YES manual up                    down 
Vlan99                 192.168.99.254  YES manual up                    down
````

The SVI line protocol should become ``up`` when its VLAN has an active Layer 2 port or an operational trunk carrying that VLAN. If an SVI is ``down/down``, check its VLAN and port connectivity.

---


#### Configure trunking on MLS

The connection between **MLS** and **S1** must carry traffic from multiple VLANs.

````
MLS# enable
MLS# configure terminal
````


##### Select MLS G0/1
````
MLS(config)# interface gigabitEthernet 0/1
MLS(config-if)# switchport trunk encapsulation dot1q
MLS(config-if)# switchport mode trunk
MLS(config-if)# switchport trunk native vlan 99
MLS(config-if)# no shutdown
MLS(config-if)# exit
MLS(config)# end
````

##### Verify the MLS trunk
````
MLS# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      99

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,99,999
````

Now we see: `Gig0/1      on           802.1q         trunking      99`.


---


#### Configure trunking on S1

Now we configure the other end of the connection.


Click on **S1** -> **CLI**, press **Enter**.

Then enter:
````
S1> enable
S1# configure terminal
S1(config)# interface gigabit
S1(config)# interface gigabitEthernet 0/1
S1(config-if)# switchport mode trunk
S1(config-if)# no shutdown
S1(config-if)# end
````


> MLS ``G0/1`` and **S1** ``G0/1`` must agree on trunking and native VLAN 99. Otherwise, the link might not operate as intended or may report a native VLAN mismatch.


Then verify:
````
S1# show interface trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      999
Fa0/2       on           802.1q         trunking      999
Gig0/1      on           802.1q         trunking      99

Port        Vlans allowed on trunk
Fa0/1       1-1005
Fa0/2       1-1005
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,30,99,999
Fa0/2       1,10,20,30,99,999
Gig0/1      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,30,99,999
Fa0/2       1,10,20,30,99,999
Gig0/1      1,10,20,30,99,999
````



**Check the native VLAN:**
````
S1# show interfaces gigabitEthernet 0/1 switchport
````
**Output:**
````
Name: Gig0/1
Switchport: Enabled
Administrative Mode: trunk
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: On
Access Mode VLAN: 1 (default)
Trunking Native Mode VLAN: 99 (Management)
Voice VLAN: none
Administrative private-vlan host-association: none
Administrative private-vlan mapping: none
Administrative private-vlan trunk native VLAN: none
Administrative private-vlan trunk encapsulation: dot1q
Administrative private-vlan trunk normal VLANs: none
Administrative private-vlan trunk private VLANs: none
Operational private-vlan: none
Trunking VLANs Enabled: All
Pruning VLANs Enabled: 2-1001
Capture Mode Disabled
Capture VLANs Allowed: ALL
Protected: false
Unknown unicast blocked: disabled
Unknown multicast blocked: disabled
Appliance trust: none
````


---


#### Verify switch management addresses

On our addressing table includes three management addresses:

- S1: ``192.168.99.1/24``
- S2: ``192.168.99.2/24``
- S3: ``192.168.99.3/24``


##### Check on S1

Then check each:
````
S1# show ip interface brief
````
**Output:**

````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual up                    up 
FastEthernet0/3        unassigned      YES manual down                  down 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual down                  down 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual down                  down 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
FastEthernet0/22       unassigned      YES manual down                  down 
FastEthernet0/23       unassigned      YES manual down                  down 
FastEthernet0/24       unassigned      YES manual down                  down 
GigabitEthernet0/1     unassigned      YES manual up                    up 
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  unassigned      YES manual administratively down down 
Vlan99                 192.168.99.1    YES manual up                    up
````

Now we got and see it have.


##### Chech on S2:
````
S2> enable
S2# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual down                  down 
FastEthernet0/3        unassigned      YES manual up                    up 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual down                  down 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual up                    up 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
FastEthernet0/22       unassigned      YES manual down                  down 
FastEthernet0/23       unassigned      YES manual up                    up 
FastEthernet0/24       unassigned      YES manual down                  down 
GigabitEthernet0/1     unassigned      YES manual down                  down 
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  unassigned      YES manual administratively down down 
Vlan99                 192.168.99.2    YES manual up                    up
````

Now we see see it.


##### Check S3

````
S3> enable
S3# show ip interface brief
````

**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual down                  down 
FastEthernet0/2        unassigned      YES manual up                    up 
FastEthernet0/3        unassigned      YES manual up                    up 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual down                  down 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual up                    up 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
FastEthernet0/22       unassigned      YES manual down                  down 
FastEthernet0/23       unassigned      YES manual up                    up 
FastEthernet0/24       unassigned      YES manual down                  down 
GigabitEthernet0/1     unassigned      YES manual down                  down 
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  unassigned      YES manual administratively down down 
Vlan99                 192.168.99.3    YES manual up                    up
````

Now we see.


---


In this if don't see it just configure it.

**S1**:

```
S3> enable
S3# configure terminal
S3(config)# vlan 99
S3(config-vlan)# name Management
S3(config-vlan)# exit
S3(config)# interface vlan 99
S3(config-if)# ip address 192.168.99.1 255.255.255.0
S3(config-if)# no shutdown
S3(config-if)# exit
S3(config)# ip default-gateway 192.168.99.254
S3(config)# end
S3#
```



**S2:**
```
S2> enable
S2# configure terminal
S2(config)# vlan 99
S2(config-vlan)# name Management
S2(config-vlan)# exit
S2(config)# interface vlan 99
S2(config-if)# ip address 192.168.99.2 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
S2(config)# ip default-gateway 192.168.99.254
S2(config)# end
S2#
```


**S3:**
```
S1> enable
S1# configure terminal
S1(config)# vlan 99
S1(config-vlan)# name Management
S1(config-vlan)# exit
S1(config)# interface vlan 99
S1(config-if)# ip address 192.168.99.3 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# ip default-gateway 192.168.99.254
S1(config)# end
S1#
```

----


#### Enable IPv4 routing

This step turns **MLS** into a Layer 3 router between VLANs.

##### Check the routing table enabling routing

On **MLS**:
````
MLS> enable
MLS# show ip route
````
**Output:**
````
Default gateway is not set

Host               Gateway           Last Use    Total Uses  Interface
ICMP redirect cache is empty
````

> So in this IP routing not yet been enabled.


##### Enable IP routing
````
MLS# configure terminal
MLS(config)# ip routing
MLS(config)# end
````



##### Verify route
````
MLS# show ip route
````
**Output:**
````
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

C    192.168.10.0/24 is directly connected, Vlan10
C    192.168.20.0/24 is directly connected, Vlan20
C    192.168.30.0/24 is directly connected, Vlan30
C    192.168.99.0/24 is directly connected, Vlan99
     209.165.200.0/30 is subnetted, 1 subnets
C       209.165.200.224 is directly connected, GigabitEthernet0/2
````

``C`` means Connected. These routes tell MLS that it can directly reach those networks.


---

#### Verify IPv4 end-to-end connectivity

Now verify that **PCs** can communicate within their **VLANs** and across different **VLANs**.


##### Check PC0 — VLAN 10

Click on **PC0** -> **Desktop** -> **IP Configuration**:
| Setting | Value |
| :--- | :--- |
| IPv4 address | `192.168.10.1` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.10.254` |

<img width="871" height="680" alt="image" src="https://github.com/user-attachments/assets/6d7025fc-0f31-4331-8350-bd0921901e67" />


Then open **Command Prompt**:
````
ipconfig
````
<img width="865" height="526" alt="image" src="https://github.com/user-attachments/assets/12e50d26-f040-418c-ab80-e89d2d7daad6" />


````
ping 192.168.10.254
ping 192.168.10.2
````

<img width="527" height="432" alt="image" src="https://github.com/user-attachments/assets/f0e3925d-d4b9-4fca-94fe-4015a7faad8d" />


Now we got successful.


##### Check PC1 - VLAN 20

Click on **PC1** -> **Desktop** -> **IP Configuration**:

| Setting | Value |
| :--- | :--- |
| IPv4 address | `192.168.20.1` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.20.254` |

<img width="876" height="662" alt="image" src="https://github.com/user-attachments/assets/d2bd76c0-5635-4242-a523-03689200fd20" />


Then open **Command Prompt**:
````
ipconfig
````
<img width="867" height="557" alt="image" src="https://github.com/user-attachments/assets/5a7a19e1-8a90-4e49-9ef5-f72ae745b325" />


````
ping 192.168.20.254
ping 192.168.20.2
````

<img width="500" height="427" alt="image" src="https://github.com/user-attachments/assets/16a37f45-37bc-4314-bea7-528bdff7c660" />



---


##### Check PC2 - VLAN 30
Click on **PC2** -> **Desktop** -> **IP Configuration**:

| Setting | Value |
| :--- | :--- |
| IPv4 address | `192.168.30.1` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.30.254` |

<img width="875" height="662" alt="image" src="https://github.com/user-attachments/assets/66037748-e226-4320-ab15-9709af9b1829" />


Then open **Command Prompt**:

````
ipconfig
````
<img width="873" height="533" alt="image" src="https://github.com/user-attachments/assets/15047cca-1b69-4234-a4f5-c7cb5f4ad153" />



````
ping 192.168.30.254
ping 192.168.30.2
````

<img width="524" height="425" alt="image" src="https://github.com/user-attachments/assets/2cd1b2e9-4147-4e9c-a4d2-c6d4292d757d" />


---



##### Check switch management connectivity

Open **S1** → **CLI**:
````
enable
ping 192.168.99.2
ping 192.168.99.3
ping 192.168.99.254
````

<img width="636" height="332" alt="image" src="https://github.com/user-attachments/assets/c60ea92a-ca14-46d9-b4c1-9ae75b1ff339" />


Now it successful.


##### Test inter-VLAN routing

From **PC0**, run:
````
ping 192.168.20.1
ping 192.168.30.1
````
<img width="497" height="421" alt="image" src="https://github.com/user-attachments/assets/af0dce7f-4de4-4e13-8c11-57fa572332ad" />


Now it successful replies.

> Now routes between VLAN 10, VLAN 20, and VLAN 30 using its SVIs.

---


##### Test IPv4 connectivity to Cloud

From **MLS** or a **PC**, run:
````
ping 209.165.200.226
````
<img width="601" height="153" alt="image" src="https://github.com/user-attachments/assets/2cf8b3e6-977e-4189-aa5f-817355daf54e" />


Now it successful replies.


---




### Part 3: Configure IPv6 Inter-VLAN Routing


#### Step 1: Enable IPv6 routing
Open **MLS** → **CLI**, then enter:
````
MLS> enable
MLS# configure terminal
MLS(config)# ipv6 unicast-routing
MLS(config)# end
MLS#
````



#### Step 2: Configure IPv6 addresses on MLS SVIs

On our VLAN we need **IPv6** addresses on VLANs 10, 20, and 30.


##### Configure VLAN 10****










































































