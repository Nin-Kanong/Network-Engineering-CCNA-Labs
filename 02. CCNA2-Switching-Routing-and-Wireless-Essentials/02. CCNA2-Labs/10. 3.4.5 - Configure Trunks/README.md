<h1 align="center"> 3.4.5 - Configure Trunks </h1>


---


### Lab Guide

[3.4.5 Packet Tracer - Configure Trunks.docx](https://github.com/user-attachments/files/34094554/3.4.5.Packet.Tracer.-.Configure.Trunks.docx)


---


### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Switch Port | VLAN |
|---|---|---|---|---|---|
| PC1 | NIC | 172.17.10.21 | 255.255.255.0 | S2 F0/11 | 10 |
| PC2 | NIC | 172.17.20.22 | 255.255.255.0 | S2 F0/18 | 20 |
| PC3 | NIC | 172.17.30.23 | 255.255.255.0 | S2 F0/6 | 30 |
| PC4 | NIC | 172.17.10.24 | 255.255.255.0 | S3 F0/11 | 10 |
| PC5 | NIC | 172.17.20.25 | 255.255.255.0 | S3 F0/18 | 20 |
| PC6 | NIC | 172.17.30.26 | 255.255.255.0 | S3 F0/6 | 30 |

---


### Objectives

**Part 1: Verify VLANs**

**Part 2: Configure Trunks**



---


## Lab Walkthrough

<img width="1174" height="577" alt="image" src="https://github.com/user-attachments/assets/3e81bc61-70fe-41da-b20c-70ad8ebed8cc" />


---


### Part 1: Verify VLANs


#### Step 1: Display the current VLANs.

##### Check the VLANs on S1

Click **S1** → **CLI**, then press **Enter**:

````
S1> enable
S1#
````

````shell
S1# show vlan brief
````
**Output:**
````shell
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
10   Faculty/Staff                    active    
20   Students                         active    
30   Guest(Default)                   active    
88   Management                       active    
99   Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

Now it active all.



##### Verify VLANs and port assignments on S2

Click **S2** → **CLI** and **Enter**:
````cisco
S2> enable
S2# show vlan brief
````
**Output**:
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
88   Management                       active    
99   Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````



##### Verify VLANs and port assignments on S3

Click **S3** → **CLI** and **Enter**:
````
S3> enable
S3# show vlan brief
````

**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
88   Management                       active    
99   Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


---


#### Step 2: Verify loss of connectivity between PCs on the same network.

On **PC1** → **Desktop** → **Command Prompt**, run:
````
ping 172.17.10.24
````
**Output:**
````
Pinging 172.17.10.24 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 172.17.10.24:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
````

> Before trunking is configured, the ping should fail. Although **PC1** and **PC4** belong to **VLAN 10** and share the same subnet, the inter-switch link is initially an access port in **VLAN 1**. It therefore does not carry **VLAN 10** traffic between the switches.


---


### Part 2: Configure Trunks

#### Step 1: Configure trunking on S1 and use VLAN 99 as the native VLAN.


##### Configure trunk ports on S1


**S1** connects to **S2** through ``Gig0/1`` and to **S3** through ``Gig0/2``.

Click **S1** → **CLI** and enter these commands:

````cisco
S1> enable
S1# configure terminal
S1(config)# interface range gigabitEthernet 0/1 - 2
S1(config-if-range)# switchport mode trunk
S1(config-if-range)# switchport trunk native vlan 99
S1(config-if-range)# end
````



##### Wait for the trunk ports to become active
Then in this Click **Fast Forward Time** on the bottom toolbar and wait for the links to converge.

<img width="1917" height="941" alt="image" src="https://github.com/user-attachments/assets/7db527e7-411f-4eaf-af2b-f73c3be8bd83" />


Then back to our **S1**, We may see messages like these:

<img width="872" height="818" alt="image" src="https://github.com/user-attachments/assets/66c19bbb-49f5-4f6e-82ab-389b08ff28d3" />


> This is expected at this stage. We configured native VLAN 99 on S1, but S2 and S3 still use native VLAN 1.

---

#### Step 2: Verify trunking is enabled on S2 and S3.

##### Verify the trunks on S1

On **S1**, at ``S1#``, enter:
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      99
Gig0/2      on           802.1q         trunking      99

Port        Vlans allowed on trunk
Gig0/1      1-1005
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,88,99
Gig0/2      1,10,20,30,88,99

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,88,99
Gig0/2      1,10,20,30,88,99
````

> The trunks now carry traffic for VLANs 10, 20, and 30 between the switches. The native VLAN mismatch mainly affects untagged traffic: S1 uses VLAN 99 while S2 and S3 still use VLAN 1. Because the PC traffic is carried in its respective tagged VLAN, same-VLAN communication can work even before the native VLAN mismatch is corrected.



##### Verify trunking on S2
On **S2**, run:
````
S2> enable
S2# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      auto         n-802.1q       trunking      1

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,88,99

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      10,20,30,88
````

> S2's ``Gig0/1`` should have negotiated trunking with ``S1`` through DTP.



##### Verify trunking on S3

click **S3** → **CLI** and enter:

````
S3> enable
S3# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/2      auto         n-802.1q       trunking      1

Port        Vlans allowed on trunk
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/2      1,10,20,30,88,99

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/2      10,20,30,88
````

> **S3**'s ``Gig0/2`` should also be trunking, with its native VLAN still 1.

---


#### Step 3: Correct the native VLAN mismatch on S2 and S3.

##### Correct the native VLAN on S2

Now configure VLAN 99 as the native VLAN on **S2**'s uplink.

Click **S2** → **CLI** and enter:
````
S2# enable
S2# configure terminal
S2(config)# interface gigabitEthernet 0/1
S2(config-if)# switchport trunk native vlan 99
S2(config-if)# end
````
> Now both ends of each trunk should use native VLAN 99.

Verify:
````
S2# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      auto         n-802.1q       trunking      99

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,20,30,88,99

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,20,30,88,99
````


##### Correct the native VLAN on S3

Click **S3** → **CLI** and enter:

````cisco
S3# enable
S3# configure terminal
S3(config)# interface gigabitEthernet 0/2
S3(config-if)# switchport trunk native vlan 99
S3(config-if)# end
````

> Now both ends of each trunk should use native **VLAN 99**.


Verify:
````
S3# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/2      auto         n-802.1q       trunking      99

Port        Vlans allowed on trunk
Gig0/2      1-1005

Port        Vlans allowed and active in management domain
Gig0/2      1,10,20,30,88,99

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/2      1,10,20,30,88,99
````

> The native VLAN mismatch messages should stop once both sides agree.


---


#### Step 4: Verify configurations on S2 and S3.

##### Verify S2's trunk port


On **S2**, enter:
````
S2# show interfaces gigabitEthernet 0/1 switchport
````
**Output:**
````
Name: Gig0/1
Switchport: Enabled
Administrative Mode: dynamic auto
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: On
Access Mode VLAN: 1 (default)
Trunking Native Mode VLAN: 99 (Native)
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

Look for fields similar to:
````
Administrative Mode: dynamic auto
Operational Mode: trunk
Trunking Native Mode VLAN: 99
````


> The administrative mode may remain ``dynamic auto`` because S2 negotiated trunking with S1 using DTP. The important checks are that the operational mode is trunk and the native VLAN is 99.




##### Verify S3's trunk port

On **S3**, enter:
````
S3# show interfaces gigabitEthernet 0/2 switchport
````
**Output:**
````
Name: Gig0/2
Switchport: Enabled
Administrative Mode: dynamic auto
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: On
Access Mode VLAN: 1 (default)
Trunking Native Mode VLAN: 99 (Native)
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



##### Display VLAN information on S2 and S3


On **S2**:
````
S2# show vlan
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/2
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
88   Management                       active    
99   Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
20   enet  100020     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
88   enet  100088     1500  -      -      -        -    -        0      0
99   enet  100099     1500  -      -      -        -    -        0      0
1002 fddi  101002     1500  -      -      -        -    -        0      0   
1003 tr    101003     1500  -      -      -        -    -        0      0   
1004 fdnet 101004     1500  -      -      -        ieee -        0      0   
1005 trnet 101005     1500  -      -      -        ibm  -        0      0   

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------

Remote SPAN VLANs
------------------------------------------------------------------------------

Primary Secondary Type              Ports
------- --------- ----------------- -----------------------------------------
````






On **S3**:
````
S3# show vlan
````

**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
88   Management                       active    
99   Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
20   enet  100020     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
88   enet  100088     1500  -      -      -        -    -        0      0
99   enet  100099     1500  -      -      -        -    -        0      0
1002 fddi  101002     1500  -      -      -        -    -        0      0   
1003 tr    101003     1500  -      -      -        -    -        0      0   
1004 fdnet 101004     1500  -      -      -        ieee -        0      0   
1005 trnet 101005     1500  -      -      -        ibm  -        0      0   

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------

Remote SPAN VLANs
------------------------------------------------------------------------------

Primary Secondary Type              Ports
------- --------- ----------------- ------------------------------------------
````

> We see VLANs 10, 20, and 30 assigned to their corresponding access ports. VLAN 99 should be present.


##### Test connectivity again

After the trunks are active and their native VLANs match, return to **PC1** → **Desktop** → **Command Prompt**:
````
ping 172.17.10.24
````
**Output:**
````
Pinging 172.17.10.24 with 32 bytes of data:

Reply from 172.17.10.24: bytes=32 time<1ms TTL=128
Reply from 172.17.10.24: bytes=32 time=1ms TTL=128
Reply from 172.17.10.24: bytes=32 time<1ms TTL=128
Reply from 172.17.10.24: bytes=32 time<1ms TTL=128

Ping statistics for 172.17.10.24:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
````

Now it response n=back.


Now we got successful.

----


#### Scores

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/d4611a94-7ee3-4ee2-aef6-f657591c43ab" />


Now we got full score.


-----
