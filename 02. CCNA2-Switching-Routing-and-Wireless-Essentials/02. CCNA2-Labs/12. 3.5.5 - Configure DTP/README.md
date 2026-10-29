<h1 align="center"> 3.5.5 - Configure DTP </h1>


---


### Lab Guide



---


### Addressing Table

| Device | Interface | IP Address     | Subnet Mask     |
| ------ | --------- | -------------- | --------------- |
| PC1    | NIC       | `192.168.10.1` | `255.255.255.0` |
| PC2    | NIC       | `192.168.20.1` | `255.255.255.0` |
| PC3    | NIC       | `192.168.30.1` | `255.255.255.0` |
| PC4    | NIC       | `192.168.30.2` | `255.255.255.0` |
| PC5    | NIC       | `192.168.20.2` | `255.255.255.0` |
| PC6    | NIC       | `192.168.10.2` | `255.255.255.0` |
| S1     | VLAN 99   | `192.168.99.1` | `255.255.255.0` |
| S2     | VLAN 99   | `192.168.99.2` | `255.255.255.0` |
| S3     | VLAN 99   | `192.168.99.3` | `255.255.255.0` |

---

### Objectives

- Configure static trunking

- Configure and Verify DTP

> This lab teaches us how to configure VLANs, assign switch ports, configure static trunks, verify Dynamic Trunking Protocol (DTP), and troubleshoot connectivity between PCs.

---


## Lab Walkthrough

<img width="1243" height="702" alt="image" src="https://github.com/user-attachments/assets/b4ff5218-5f07-476f-a01d-e32e76263716" />


The topology contains three switches and six PCs. Our connections should follow the lab topology provided in Packet Tracer.

- **S1**: Connects to S2 through GigabitEthernet0/1 and S3 through GigabitEthernet0/2.
- **S2**: Connects to PC1, PC2, and PC6.
- **S3**: Connects to PC3, PC4, and PC5.
- **VLAN 10 (Red)**: ``192.168.10.0/24``
- **VLAN 20 (Blue)**: ``192.168.20.0/24``
- **VLAN 30 (Yellow)**: ``192.168.30.0/24``
- **VLAN 99**: Management
- **VLAN 999**: Native VLAN for trunk links

---


### Part 1: Verify VLAN configuration.

#### Check S1

Click **S1**, open the **CLI**, and press **Enter**:

````
S1> enable
````

**Then verify:**
````cisco
S1# show vlan brief
````
**Outpu:**
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
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````




#### Check S2

Click **S2**, open the **CLI**, and press **Enter**:

````
S2> enable
````

**Then verify:**
````cisco
S2# show vlan brief
````
**Outpu:**

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
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````



#### Check S3
Click **S3**, open the **CLI**, and press **Enter**:

````
S3> enable
````

**Then verify:**
````cisco
S3# show vlan brief
````
**Outpu:**
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
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


> VLANs 10, 20, and 30 will be created on S2 and S3 in Part 2.

> Initially, VLANs 1, 99, 999, and the default legacy VLANs 1002–1005 are configured. VLANs 10, 20, and 30 will be added to S2 and S3.


---


### Part 2: Create additional VLANs on S2 and S3.

#### Create VLANs on S3

Click **S2** and enter:
````cisco
S1#enable
S1#configure terminal
````

**VLAN 10:**
````
S1(config)# vlan 10
S1(config-vlan)# name Red
S1(config-vlan)# exit
````

**VLAN 20:**
````
S1(config)# vlan 20
S1(config-vlan)# name Blue
S1(config-vlan)# exit
````


**VLAN 30:**
````
S1(config)# vlan 30
S1(config-vlan)# name Yellow
S1(config-vlan)# exit
````

**Exit:**
````cisco
S1(config)# end
````

###### Verify VLANs on S2
````cisco
S1# show vlan brief
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
10   Red                              active    
20   Blue                             active    
30   Yellow                           active    
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---


#### Create VLANs on S2

Click **S2** and enter:
````cisco
S2#enable
S2#configure terminal
````

**VLAN 10:**
````
S2(config)# vlan 10
S2(config-vlan)# name Red
S2(config-vlan)# exit
````

**VLAN 20:**
````
S2(config)# vlan 20
S2(config-vlan)# name Blue
S2(config-vlan)# exit
````


**VLAN 30:**
````
S2(config)# vlan 30
S2(config-vlan)# name Yellow
S2(config-vlan)# exit
````

**Exit:**
````cisco
S2(config)# end
````


###### Verify VLANs on S2
````cisco
S2# show vlan brief
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
10   Red                              active    
20   Blue                             active    
30   Yellow                           active    
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> **VLAN 10 (Red)**, **VLAN 20 (Blue)**, and **VLAN 30 (Yellow)**.

---



#### Create VLANs on S3

Click **S3** and enter:

````
S3# enable
S3# configure terminal
````

**VLAN 10:**
````
S3(config)# vlan 10
S3(config-vlan)# name Red
S3(config-vlan)# exit
````

**VLAN 20:**
````
S3(config)# vlan 20
S3(config-vlan)# name Blue
S3(config-vlan)# exit
````

**VLAN 30:**
````
S3(config)# vlan 30
S3(config-vlan)# name Yellow
S3(config-vlan)# exit
````

**Exit:**
````
S3(config)# end
````



**Verify:**
````cisco
S3#show vlan brief
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
10   Red                              active    
20   Blue                             active    
30   Yellow                           active    
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> Confirm that **VLANs 10**, **20**, and **30** are active on **S3**.

---



### Part 3: Assign VLANs to Ports

Configure the access ports on **S2** and **S3** as specified in the table.

| Ports                    | Assignments      | Network           |
| ------------------------ | ---------------- | ----------------- |
| S2 F0/1–8, S3 F0/1–8     | VLAN 10 (Red)    | `192.168.10.0/24` |
| S2 F0/9–16, S3 F0/9–16   | VLAN 20 (Blue)   | `192.168.20.0/24` |
| S2 F0/17–24, S3 F0/17–24 | VLAN 30 (Yellow) | `192.168.30.0/24` |

---


#### Configure S2

Click on **S2** and enter:

**Enter Global Configuration Mode:**
````cisco
S2> enable
S2# configure terminal
````

**Assign VLAN 10 (Red)**:
````
S2(config)# interface range fastEthernet 0/1 - 8
S2(config-if-range)# switchport mode access
S2(config-if-range)# switchport access vlan 10
S2(config-if-range)# exit
````

**Assign VLAN 20 (Blue)**:
````cisco
S2(config)# interface range fastEthernet 0/9 - 16
S2(config-if-range)# switchport mode access
S2(config-if-range)# switchport access vlan 20
S2(config-if-range)# exit
````

**Assign VLAN 30 (Yellow)**:
````
S2(config)# interface range fastEthernet 0/17 - 24
S2(config-if-range)# switchport mode access
S2(config-if-range)# switchport access vlan 30
S2(config-if-range)# exit
````

**Exit Configuration Mode**:
````
S2(config)# end
````


**Then verify:**
````
S2# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gig0/1, Gig0/2
10   Red                              active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
20   Blue                             active    Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
30   Yellow                           active    Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---


#### Configure S3

Click on **S3** and enter:

**Enter Global Configuration Mode:**
````
S3> enable
S3# configure terminal
````


**Assign VLAN 10 (Red):**
````
S3(config)# interface range fastEthernet 0/1 - 8
S3(config-if-range)# switchport mode access
S3(config-if-range)# switchport access vlan 10
S3(config-if-range)# exit
````


**Assign VLAN 20 (Blue)**:
````
S3(config)# interface range fastEthernet 0/9 - 16
S3(config-if-range)# switchport mode access
S3(config-if-range)# switchport access vlan 20
S3(config-if-range)# exit
````

**Assign VLAN 30 (Yellow)**:
````
S3(config)# interface range fastEthernet 0/17 - 24
S3(config-if-range)# switchport mode access
S3(config-if-range)# switchport access vlan 30
S3(config-if-range)# exit
````

**Exit Configuration Mode:**
````
S3(config)# end
````



Then verify:
````
S3# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gig0/1, Gig0/2
10   Red                              active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
20   Blue                             active    Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
30   Yellow                           active    Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
99   Management                       active    
999  Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


Confirm that:
- ``Fa0/1–8`` appear under VLAN 10.
- ``Fa0/9–16`` appear under VLAN 20.
- ``Fa0/17–24`` appear under VLAN 30.

----


#### Test PC1 to PC6

On **PC1**, open **Desktop** → **Command Prompt** and enter:
````
ping 192.168.10.2
````

**Output:**
````
Pinging 192.168.10.2 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.10.2:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
````

> The ping is unsuccessful at this stage if PC1 and PC6 are on different switches and the inter-switch links are not yet correctly carrying VLAN 10. Although both PCs are in the same subnet, their VLAN traffic cannot cross a link that is not functioning as a trunk carrying VLAN 10.


---



### Part 4: Configure Trunks on S1, S2, and S3.

In this part, we will configure:
- ``S1 Gi0/1`` using DTP negotiation.
- ``S1 Gi0/2`` as a static trunk with DTP negotiation disabled.
- **VLAN 999** as the native VLAN on all trunk links.


#### Configure S1 Gi0/1 as dynamic desirable

##### On **S1**:

````
S1>enable
S1#configure terminal
S1(config)#interface gigabitEthernet 0/1
S1(config-if)#switchport mode dynamic desirable
S1(config-if)#end
````
> This places S1 Gi0/1 in **dynamic desirable** mode. It actively attempts to negotiate a trunk using DTP.



> In this if ``S2 Gi0/1`` is still in its default dynamic auto mode and the link is connected, S1 and S2 should negotiate a trunk successfully.


---


##### On S2:
````
S2> show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      auto         n-802.1q       trunking      1

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,99,999
````

> The mode shows the local configuration (``auto``), while the status confirms that the link successfully negotiated trunking.

---



#### Configure S1 Gi0/2 as a static trunk

On **S1**:
````
S1> enable
S1# configure terminal
S1(config)# interface gigabitEthernet 0/2
S1(config-if)# switchport mode trunk
S1(config-if)# switchport nonegotiate
S1(config-if)# end
````

- ``switchport mode trunk`` forces the interface to trunk mode.
- ``switchport nonegotiate`` disables DTP transmission on that interface.

> The other end, S3 Gi0/2, must also be configured to trunk. A static trunk with DTP disabled on S1 does not automatically guarantee that S3's default dynamic-auto port will become a trunk.

---



#### Verify DTP on S1
````
S1# show dtp
````
**Output:**
````
Global DTP information
    Sending DTP Hello packets every 30 seconds
    Dynamic Trunk timeout is 300 seconds
    1 interfaces using DTP
````

> The exact number of interfaces using DTP may vary according to the current configuration and switch model.

---

#### Verify trunk interfaces on S1
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      desirable    n-802.1q       trunking      1
Gig0/2      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Gig0/1      1-1005
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,99,999
Gig0/2      1,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,99,999
Gig0/2      1,99,999
````

---

#### Change the native VLAN on S1

On **S1**:

````
S1> enable
S1# configure terminal
S1(config)# interface range gigabitEthernet 0/1 - 2
S1(config-if-range)# switchport trunk native vlan 999
S1(config-if-range)# end
````

**Verify:**
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      desirable    n-802.1q       trunking      999
Gig0/2      on           802.1q         trunking      999

Port        Vlans allowed on trunk
Gig0/1      1-1005
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,99,999
Gig0/2      1,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,99,999
Gig0/2      1,99,999
````

#### Configure native VLAN 999 on S2

On **S2**:
````
S2> enable
S2# configure terminal
S2(config)# interface gigabitEthernet 0/1
S2(config-if)# switchport trunk native vlan 999
S2(config-if)# end
````
> This assumes Gi0/1 is the trunk connection to S1, as specified in the lab.


````
S2# show interfaces trunk
````
**output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      auto         n-802.1q       trunking      999

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,99,999
````



#### Configure native VLAN 999 on S3
On **S3**:

````
S3> enable
S3# configure terminal
S3(config)# interface gigabitEthernet 0/2
S3(config-if)# switchport trunk native vlan 999
S3(config-if)# end
````

> This sets the native VLAN but does not, by itself, force the S3 interface into trunk mode. You will explicitly configure that in Part 5.

````
S3#show interfaces trunk
````

**Output:**
````
S3#show interfaces trunk


S3#
````
> At this point, ``S3 Gi0/2`` may still not appear in ``show interfaces trunk`` until we configure it as a trunk.

---


#### Test switch management connectivity

From **S1**, test **S2** and **S3**:

````
S1# ping 192.168.99.2
````
**Output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.99.2, timeout is 2 seconds:
..!!!
Success rate is 60 percent (3/5), round-trip min/avg/max = 0/0/0 ms
````

````
S1# ping 192.168.99.3
````
**Output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.99.3, timeout is 2 seconds:
.....
Success rate is 0 percent (0/5)
````

> The pings succeed once VLAN 99 exists on all switches, the management SVIs are correctly configured and up, and VLAN 99 is carried over the required trunk links.

---


#### Test PC1 to PC6 again

From **PC1**:
````
ping 192.168.10.2
````

**Output:**
````
Pinging 192.168.10.2 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.10.2:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
````
> In this it unsuccessful, cause check the VLAN database and trunk output. The switches must have VLAN 10 configured, and every link between PC1 and PC6 must carry VLAN 10. If VLAN 10 is missing from an intermediate switch or the link between switches is not trunking, the PCs cannot communicate at Layer 2.

---


### Part 5: Reconfigure trunk on S3.

#### Check S3 Gi0/2

On **S3**:
````
S3# enable
S3# show interfaces trunk
````
> If the port is still in its default dynamic-auto mode and has not negotiated a trunk, it may not appear in the output at all.

---


#### Configure S3 Gi0/2 to match S1

On **S3**, enter:
````
S3# configure terminal
S3(config)# interface gigabitEthernet 0/2
S3(config-if)# switchport mode trunk
S3(config-if)# switchport trunk native vlan 999
S3(config-if)# switchport nonegotiate
S3(config-if)# end
````
> This matches S1 Gi0/2's static trunk configuration and disables DTP negotiation at both ends.


##### Verify the change
````
S3# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/2      on           802.1q         trunking      999

Port        Vlans allowed on trunk
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/2      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/2      1,10,20,30,99,999
````

##### Check trunk negotiation status

````
S3# show interfaces gigabitEthernet 0/2 switchport
````
**output:**
````
Name: Gig0/2
Switchport: Enabled
Administrative Mode: trunk
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: Off
Access Mode VLAN: 1 (default)
Trunking Native Mode VLAN: 999 (Native)
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

> `Negotiation of Trunking` ``Off``, because switchport nonegotiate disables DTP negotiation on the interface.


---


#### Verify all trunk links

##### On **S1**:
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      desirable    n-802.1q       trunking      999
Gig0/2      on           802.1q         trunking      999

Port        Vlans allowed on trunk
Gig0/1      1-1005
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,99,999
Gig0/2      1,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,99,999
Gig0/2      1,99,999
````


##### On **S2**:
````
S2# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      auto         n-802.1q       trunking      999

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,99,999
````

##### On **S3**:
````
S3# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/2      on           802.1q         trunking      999

Port        Vlans allowed on trunk
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/2      1,10,20,30,99,999

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/2      1,10,20,30,99,999
````


All listed trunk interfaces should have status ``trunking``.

---



### Part 6: Verify end to end connectivity.


















