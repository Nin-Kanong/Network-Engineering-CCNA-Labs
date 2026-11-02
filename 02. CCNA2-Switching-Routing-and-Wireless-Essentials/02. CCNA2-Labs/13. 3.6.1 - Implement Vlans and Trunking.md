<h1 align="center"> Implement Vlans and Trunking </h1>


---


### Lab Guide

[3.6.1 Packet Tracer - Implement VLANs and Trunking.docx](https://github.com/user-attachments/files/34262172/3.6.1.Packet.Tracer.-.Implement.VLANs.and.Trunking.docx)



---


### Addressing Table


| Device | Interface | IP Address     | Subnet Mask   | Switchport | VLAN                     |
| ------ | --------- | -------------- | ------------- | ---------- | ------------------------ |
| PC1    | NIC       | 192.168.10.10  | 255.255.255.0 | SWB F0/1   | VLAN 10                  |
| PC2    | NIC       | 192.168.20.20  | 255.255.255.0 | SWB F0/2   | VLAN 20                  |
| PC3    | NIC       | 192.168.30.30  | 255.255.255.0 | SWB F0/3   | VLAN 30                  |
| PC4    | NIC       | 192.168.10.11  | 255.255.255.0 | SWC F0/1   | VLAN 10                  |
| PC5    | NIC       | 192.168.20.21  | 255.255.255.0 | SWC F0/2   | VLAN 20                  |
| PC6    | NIC       | 192.168.30.31  | 255.255.255.0 | SWC F0/3   | VLAN 30                  |
| PC7    | NIC       | 192.168.10.12  | 255.255.255.0 | SWC F0/4   | VLAN 10, VLAN 40 (Voice) |
| SWA    | SVI       | 192.168.99.252 | 255.255.255.0 | N/A        | VLAN 99                  |
| SWB    | SVI       | 192.168.99.253 | 255.255.255.0 | N/A        | VLAN 99                  |
| SWC    | SVI       | 192.168.99.254 | 255.255.255.0 | N/A        | VLAN 99                  |

---


### Objectives

- **Part 1**: Configure VLANs
- **Part 2**: Assign Ports to VLANs
- **Part 3**: Configure Static Trunking
- **Part 4**: Configure Dynamic Trunking


---


## Lab Walkthrough


<img width="1111" height="488" alt="image" src="https://github.com/user-attachments/assets/428f4202-1edd-4cd3-a7cd-e530c80a3144" />



---


### Part 1: Configure VLANs


**VLAN Table:**
| VLAN Number | VLAN Name  |
| ----------- | ---------- |
| 10          | Admin      |
| 20          | Accounts   |
| 30          | HR         |
| 40          | Voice      |
| 99          | Management |
| 100         | Native     |


#### Configure SWA

click **SWA** → **CLI**, and press **Enter**:

<img width="872" height="865" alt="image" src="https://github.com/user-attachments/assets/7a13e39a-74e4-4543-ac94-44b1bd7d2bda" />


Enter privileged EXEC mode:
````
SWA> enable
SWA#
````

Then enter global configuration mode:
````
SWA# configure terminal
````

Create VLAN 10:
````
SWA(config)# vlan 10
SWA(config-vlan)# name Admin
SWA(config-vlan)# exit
````


Create VLAN 20:
````
SWA(config)# vlan 20
SWA(config-vlan)# name Accounts
SWA(config-vlan)# exit
````



Create VLAN 30:
````
SWA(config)# vlan 30
SWA(config-vlan)# name HR
SWA(config-vlan)# exit
````


Create VLAN 40:
````
SWA(config)# vlan 40
SWA(config-vlan)# name Voice
SWA(config-vlan)# exit
````


Create VLAN 99:
````
SWA(config)# vlan 99
SWA(config-vlan)# name Management
SWA(config-vlan)# exit
````


Create VLAN 100:
````
SWA(config)# vlan 100
SWA(config-vlan)# name Native
SWA(config-vlan)# exit
````


Finish:
````
SWA(config)# end
````


Verify:
````
SWA# show vlan brief
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
                                                Gig0/1, Gig0/2
10   Admin                            active    
20   Accounts                         active    
30   HR                               active    
40   Voice                            active    
99   Management                       active    
100  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---




#### Configure SWB

Click on **SWB** -> **CLI**, then press **Enter**:


**Enter privileged EXEC mode:**
````
SWB> enable
````

**Then enter global configuration mode:**
````
SWB# configure terminal
````


**Create Vlan 10:**
````
SWB(config)# vlan 10
SWB(config-vlan)# name Admin
SWB(config-vlan)# exit
````


**Create vlan 20:**
````
SWB(config)# vlan 20
SWB(config-vlan)# name Accounts
SWB(config-vlan)# exit
````

**Create vlan 30:**
````
SWB(config)# vlan 30
SWB(config-vlan)# name HR
SWB(config-vlan)# exit
````


**Create vlan 40:**
````
SWB(config)# vlan 40
SWB(config-vlan)# name Voice
SWB(config-vlan)# exit
````

**Create vlan 99:**
````
SWB(config)# vlan 99
SWB(config-vlan)# name Management
SWB(config-vlan)# exit
````


**Create vlan 100:**
````
SWB(config)# vlan 100
SWB(config-vlan)# Name Native
SWB(config-vlan)# exit
````

**Exit:**
````
SWB(config)# end
````


**Verify:**
````
SWB# show vlan brief
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
                                                Gig0/1, Gig0/2
10   Admin                            active    
20   Accounts                         active    
30   HR                               active    
40   Voice                            active    
99   Management                       active    
100  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


---



#### Configure SWC

Click **SWC** -> **CLI**, then press **Enter**:

````
SWC> enable
SWC# configure terminal
````


**Create vlan 10:**
````
SWC(config)# vlan 10
SWC(config-vlan)# name Admin
SWC(config-vlan)# exit
````

**Create vlan 20:**
````
SWC(config)# vlan 20
SWC(config-vlan)# name Accounts
SWC(config-vlan)# exit
````

**Create vlan 30:**
````
SWC(config)# vlan 30
SWC(config-vlan)# name HR
SWC(config-vlan)# exit
````

**Create vlan 40:**
````
SWC(config)# vlan 40
SWC(config-vlan)# name Voice
SWC(config-vlan)# exit
````


**Create vlan 99:**
````
SWC(config)# vlan 99
SWC(config-vlan)# name Management
SWC(config-vlan)# exit
````

**Create vlan 100:**
````
SWC(config)# vlan 100
SWC(config-vlan)# name Native
SWC(config-vlan)# exit
````


**Exit:**
````
SWC(config)# end
````


**Verify:**
````
SWC# show vlan brief
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
                                                Gig0/1, Gig0/2
10   Admin                            active    
20   Accounts                         active    
30   HR                               active    
40   Voice                            active    
99   Management                       active    
100  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---



### Part 2: Assign Ports to VLANs

#### Step 1: Assign Access ports to VLANs


##### Configure SWB access ports

The addressing table requires:
| Switch | Port | Connected PC | VLAN |
| ------ | ---- | ------------ | ---- |
| SWB    | F0/1 | PC1          | 10   |
| SWB    | F0/2 | PC2          | 20   |
| SWB    | F0/3 | PC3          | 30   |


Click **SWB** -> **CLI**:

````
SWB> enable
SWB# configure terminal
````


**Configure PC1 port:**
````
SWB(config)# interface fastEthernet 0/1
SWB(config-if)# switchport mode access
SWB(config-if)# switchport access vlan 10
SWB(config-if)# exit
````


**Configure PC2 port:**
````
SWB(config)# interface fastEthernet 0/2
SWB(config-if)# switchport mode access
SWB(config-if)# switchport access vlan 20
SWB(config-if)# exit
````


**Configure PC3 port:**
````
SWB(config)# interface fastEthernet 0/3
SWB(config-if)# switchport mode access
SWB(config-if)# switchport access vlan 30
SWB(config-if)# exit
````


**Exit:**
````
SWB(config)# end
````

---


##### Configure SWC access ports

Thw addressing tables requires:

| Switch | Port | Connected PC | VLAN                            |
| ------ | ---- | ------------ | ------------------------------- |
| SWC    | F0/1 | PC4          | 10                              |
| SWC    | F0/2 | PC5          | 20                              |
| SWC    | F0/3 | PC6          | 30                              |
| SWC    | F0/4 | PC7          | VLAN 10 (Data), VLAN 40 (Voice) |


Click on **SWC** -> **CLI**, then press **Enter**:


````
SWC> enable
SWC# configure terminal
````


**Configure PC4:**

````
SWC(config)# interface fastEthernet 0/1
SWC(config-if)# switchport mode access
SWC(config-if)# switchport access vlan 10
SWC(config-if)# exit
````



**Configure PC5:**
````
SWC(config)# interface fastEthernet 0/2
SWC(config-if)# switchport mode access
SWC(config-if)# switchport access vlan 20
SWC(config-if)# exit
````


**Configure PC6:**
````
SWC(config)# interface fastEthernet 0/3
SWC(config-if)# switchport mode access
SWC(config-if)# switchport access vlan 30
SWC(config-if)# exit
````


---



#### Step 2: Configure the Voice VLAN port

**PC7** is connected to **SWC** ``F0/4``.

This port needs:
- Data VLAN: 10
- Voice VLAN: 40

On **SWC**, enter:
````
SWC(config)# interface fastEthernet 0/4
SWC(config-if)# switchport mode access
SWC(config-if)# switchport access vlan 10
SWC(config-if)# switchport voice vlan 40
SWC(config-if)# mls qos trust cos
SWC(config-if)# exit
SWC(config)# end
````


> **PC7**'s normal PC traffic uses **VLAN 10**. **VLAN 40** is intended for a voice device, such as an IP phone, connected to this port.


Verify SWC:
````
SWC# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
10   Admin                            active    Fa0/1, Fa0/4
20   Accounts                         active    Fa0/2
30   HR                               active    Fa0/3
40   Voice                            active    Fa0/4
99   Management                       active    
100  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


Now we see ``F0/4`` associated with **VLAN 10** for its data traffic. 

Voice VLAN configuration is also visible with:
````
SWC# show interfaces fastEthernet 0/4 switchport
````
**Output:**
````
Name: Fa0/4
Switchport: Enabled
Administrative Mode: static access
Operational Mode: static access
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
Access Mode VLAN: 10 (Admin)
Trunking Native Mode VLAN: 1 (default)
Voice VLAN: 40
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



#### Step 3: Configure the virtual management interfaces

##### Configure SWA management interface

The addressing table specifies:

| Switch | Management VLAN | IP Address       | Subnet Mask     |
| ------ | --------------- | ---------------- | --------------- |
| SWA    | 99              | `192.168.99.252` | `255.255.255.0` |
| SWB    | 99              | `192.168.99.253` | `255.255.255.0` |
| SWC    | 99              | `192.168.99.254` | `255.255.255.0` |

> An **SVI (Switched Virtual Interface)** gives a **Layer 2** switch an IP address for management.


Click on **SWA** -> **CLI**:

````
SWA >enable
SWA# configure terminal
SWA(config)# interface vlan 99
SWA(config-if)# ip address 192.168.99.252 255.255.255.0
SWA(config-if)# no shutdown
SWA(config-if)# end
````


**Verify:**
````
SWA# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual down                  down 
FastEthernet0/2        unassigned      YES manual down                  down 
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
GigabitEthernet0/2     unassigned      YES manual up                    up 
Vlan1                  unassigned      YES manual administratively down down 
Vlan99                 192.168.99.252  YES manual up                    down
````

Now it up.

---

##### Configure SWB management interface

Click **SWB** -> **CLI**:

````
SWB> enable
SWB# configure terminal
SWB(config)# interface vlan 99
SWB(config-if)# ip address 192.168.99.253 255.255.255.0
SWB(config-if)# no shutdown
SWB(config-if)# end
````


**Verify:**
````
SWB# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
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
Vlan99                 192.168.99.253  YES manual up                    down
````



---



##### Configure SWC management interface

Click on **SWC** -> **CLI**:

````
SWC# enable
SWC# configure terminal
SWC(config)# interface vlan 99
SWC(config-if)# ip address 192.168.99.254 255.255.255.0
SWC(config-if)# no shutdown
SWC(config-if)# end
````


**Verify:**
````
SWC# show ip interface brief
````
**Ourput:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual up                    up 
FastEthernet0/3        unassigned      YES manual up                    up 
FastEthernet0/4        unassigned      YES manual up                    up 
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
GigabitEthernet0/1     unassigned      YES manual down                  down 
GigabitEthernet0/2     unassigned      YES manual up                    up 
Vlan1                  unassigned      YES manual administratively down down 
Vlan99                 192.168.99.254  YES manual up                    down
````

Now it show it up all.


> At this stage, before the switch-to-switch trunks are configured, the management VLAN does not yet have an established trunk path between the switches. Therefore, management pings may fail. After configuring the trunks, VLAN 99 is carried by default, so the management interfaces should be able to communicate if their SVIs and trunks are operational.


-----



### Part 3: Configure Static Trunking

A trunk carries traffic for multiple **VLANs** between switches.

For this part, configure:
- **SWA G0/1**
- **SWB G0/1**

Both ends must be configured as static trunk ports.



#### Configure the static trunk on SWA

Click on **SWA** -> **CLI**:

````
SWA> enable
SWA# configure terminal
SWA(config)# interface gigabitEthernet 0/1
SWA(config-if)# switchport mode trunk
SWA(config-if)# switchport nonegotiate
SWA(config-if)# switchport trunk native vlan 100
SWA(config-if)# end
````


Then verify:
```
SWA# show interfaces trunk
```
**Output:**
```
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      100

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,40,99,100

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,40,99,100
```

Now we see `Gig0/1      on           802.1q         trunking      100`.


> The allowed VLAN list should include the required VLANs. By default, the trunk allows all VLANs unless we have changed its allowed list.

---



#### Configure the static trunk on SWB

Click on **SWB** -> **CLI**:
````
SWB> enable
SWB# configure terminal
SWB(config)# interface gigabitEthernet 0/1
SWB(config-if)# switchport mode trunk
SWB(config-if)# switchport nonegotiate
SWB(config-if)# switchport trunk native vlan 100
SWB(config-if)# end
````


Then verify it:
```
SWB# show interfaces trunk
```
**Output:**
```
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      100

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,40,99,100

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,40,99,100
```

Now we see `Gig0/1      on           802.1q         trunking      100`.

---




### Part 4: Configure Dynamic Trunking

In this we will configure, **SWA** ``G0/2`` connects to **SWC** ``G0/2``.


In this the task says ``SWC is using the default DTP mode for a 2960 switch``.

The default is:
````
switchport mode dynamic auto
````

> This means SWC waits for the other switch to initiate trunk negotiation. SWA will actively initiate it using ``dynamic desirable``. Cisco documents that ``dynamic desirable`` negotiates a trunk with a neighboring port in ``dynamic`` auto mode.  



#### Configure SWA G0/2

Click on **SWA** -> **CLI**:

````
SWA> enable
SWA# configure terminal
SWA(config)# interface gigabitEthernet 0/2
SWA(config-if)# switchport mode dynamic desirable
SWA(config-if)# switchport trunk native vlan 100
SWA(config-if)# end
````


Then verify:
````
SWA# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      100
Gig0/2      desirable    n-802.1q       trunking      100

Port        Vlans allowed on trunk
Gig0/1      1-1005
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,40,99,100
Gig0/2      1,10,20,30,40,99,100

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,40,99,100
Gig0/2      1,10,20,30,40,99,100
````

---



#### Configure SWC G0/2

Click on **SWC** -> **CLI**:

Because the task tells us to keep SWC's default DTP mode, do not force it into static trunk mode. Keep it in dynamic auto.

Configure the native VLAN:
````
SWC> enable
SWC# configure terminal
SWC(config)# interface gigabitEthernet 0/2
SWC(config-if)# switchport trunk native vlan 100
SWC(config-if)# end
````

> The port should remain in its default dynamic auto mode.


> **Note**: Do not enter ``switchport nonegotiate`` on either end of this dynamic trunk. DTP negotiation must remain enabled.


---



#### save configuration 

**On SWA:**
````
SWA> enable
SWA# copy running-config startup-config
````
**Output:**
````
Destination filename [startup-config]? 
Building configuration...
[OK]
````


**On SWB:**
````
SWB> enable
SWB# copy running-config startup-config
````

**On SWC:**
````
SWC> enable
SWC# copy running-config startup-config
````
**Output:**
````
Destination filename [startup-config]? 
Building configuration...
[OK]
````

----




#### Configure all PC IP addresses

Now configure the end devices.


For each **PC**:
1. Click the **PC**.
2. Select **Desktop**.
3. Select **IP Configuration**.
4. Choose **Static**.
5. Enter the IP address and subnet mask.

Use these values:

| PC  | IPv4 Address    | Subnet Mask     | Connected Switch Port | VLAN |
| --- | --------------- | --------------- | --------------------- | ---- |
| PC1 | `192.168.10.10` | `255.255.255.0` | SWB F0/1              | 10   |
| PC2 | `192.168.20.20` | `255.255.255.0` | SWB F0/2              | 20   |
| PC3 | `192.168.30.30` | `255.255.255.0` | SWB F0/3              | 30   |
| PC4 | `192.168.10.11` | `255.255.255.0` | SWC F0/1              | 10   |
| PC5 | `192.168.20.21` | `255.255.255.0` | SWC F0/2              | 20   |
| PC6 | `192.168.30.31` | `255.255.255.0` | SWC F0/3              | 30   |
| PC7 | `192.168.10.12` | `255.255.255.0` | SWC F0/4              | 10   |


All of this after we open each **PC** then it will auto set IP ready.


---

#### Test connectivity

##### Test VLAN 10

On **PC1**, open **Desktop** → **Command Prompt**:
````
ping 192.168.10.11
ping 192.168.10.12
````
<img width="873" height="603" alt="image" src="https://github.com/user-attachments/assets/faa0f826-24d2-49ef-b29d-52b99c762e7f" />


Now it got successful all.



##### Test VLAN 20

On **PC2**, run:
````
ping 192.168.20.21
````
<img width="876" height="431" alt="image" src="https://github.com/user-attachments/assets/5e5a7499-82bc-4441-8d8a-a24cf60d677b" />



##### Test VLAN 30

On **PC3**, run:
````
ping 192.168.30.31
````
<img width="877" height="452" alt="image" src="https://github.com/user-attachments/assets/ac45ed5f-d468-4f23-9ad3-1d958e1dcbe6" />


Now it got successful all.

----



#### Scores


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/681ef936-af7c-4c04-be6e-afa91588f1ed" />



Now we got full score.

---------
