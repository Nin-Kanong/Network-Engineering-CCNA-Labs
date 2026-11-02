<h1 align="center"> LAB: Configure Router On A Stick Inter-VLAN Routing </h1>



---


### Lab Guide



---


### Addressing Table

| Device | Interface | IPv4 Address   | Subnet Mask     | Default Gateway |
| ------ | --------- | -------------- | --------------- | --------------- |
| R1     | G0/0.10   | `172.17.10.1`  | `255.255.255.0` | N/A             |
| R1     | G0/0.30   | `172.17.30.1`  | `255.255.255.0` | N/A             |
| PC1    | NIC       | `172.17.10.10` | `255.255.255.0` | `172.17.10.1`   |
| PC3    | NIC       | `172.17.30.10` | `255.255.255.0` | `172.17.30.1`   |


---


### Objectives
Part 1: Add VLANs to a Switch

Part 2: Configure Subinterfaces

Part 3: Test Connectivity with Inter-VLAN Routing

---

## Lab Walk-through 

<img width="1092" height="668" alt="image" src="https://github.com/user-attachments/assets/e52cd242-4824-4442-9d90-765ac5685896" />



---



### Part 1: Add VLANs to a Switch


#### Step 1: Create VLANs on S1.

Open **S1** -> **CLI**, then press **Enter**.

**Then enter privileged EXEC mode:**
````cisco
S1>enable
S1#
````

**Enter global configuration mode:**
````
S1# configure terminal
````


**Create VLAN 10:**
````
S1(config)# vlan 10
S1(config-vlan)# exit
````

**Create VLAN 30**:
````
S1(config)# vlan 30
S1(config-vlan)# exit
````


**Verify VLANs:**
````
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
                                                Gig0/1, Gig0/2
10   VLAN0010                         active    
30   VLAN0030                         active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


Now our VLAN names appeared as ``VLAN0010`` and ``VLAN0030``. That is normal when you create VLANs without assigning custom names.


---


#### Step 2: Assign VLANs to ports.

In this it requires:

- **PC1** → **VLAN 10** → ``F0/11``

- **PC3** → **VLAN 30** → ``F0/6``



##### configure F0/11 for VLAN 10

On **S1**, enter:
````
S1> enable
S1# configure terminal
S1(config)# interface fastEthernet 0/11
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 10
S1(config-if)# exit
S1(config)# end
````


Then verify it:
````
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/1
                                                Gig0/2
10   VLAN0010                         active    Fa0/11
30   VLAN0030                         active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


##### configure F0/6 for VLAN 30

````
S1> enable
S1# configure terminal
````

````
S1(config)# interface fastEthernet 0/6
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 30
S1(config-if)# no shutdown
S1(config-if)# exit
````

````
S1(config)# end
````


**Verify:**
````
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/2
10   VLAN0010                         active    Fa0/11
30   VLAN0030                         active    Fa0/6
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````



---

#### Step 3: Test connectivity between PC1 and PC3

At this point, we have not configured inter-VLAN routing.

##### Configuration PC1 IP Address 

Click on **Pc1** -> **Desktop** -> **IP Configuration** -> select **Static**:, then input:

| Setting         | Value           |
| --------------- | --------------- |
| IPv4 Address    | `172.17.10.10`  |
| Subnet Mask     | `255.255.255.0` |
| Default Gateway | `172.17.10.1`   |

<img width="872" height="677" alt="image" src="https://github.com/user-attachments/assets/f5e3f010-7966-4589-beea-3f9aa9a2a3ec" />


> **Note**: In this it may ready auto set IP address.

---

##### Configure PC3 IP Address

Click on **PC3** -> **Desktop** -> **IP Configuration** -> **Static**,  then input this:

| Setting         | Value           |
| --------------- | --------------- |
| IPv4 Address    | `172.17.30.10`  |
| Subnet Mask     | `255.255.255.0` |
| Default Gateway | `172.17.30.1`   |


<img width="877" height="658" alt="image" src="https://github.com/user-attachments/assets/a385b3a9-0dfc-418c-b8ef-e3c0ef685abf" />


---


##### Test from PC1

Click on **PC1** -> **Desktop** -> **Command Prompt**, then enter:

````
ipconfig
````
**Output:**
````
FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: FE80::2D0:BCFF:FEE8:B8A
   IPv6 Address....................: ::
   IPv4 Address....................: 172.17.10.10
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     172.17.10.1

Bluetooth Connection:

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: ::
   IPv6 Address....................: ::
   IPv4 Address....................: 0.0.0.0
   Subnet Mask.....................: 0.0.0.0
   Default Gateway.................: ::
                                     0.0.0.0
````



Then:
````
ping 172.17.30.10
````
**Output:**
```
Pinging 172.17.30.10 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 172.17.30.10:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

Now it failed.

> The **pings** were **unsuccessful** because PC1 and PC3 are in different VLANs and different IP networks. VLAN 10 and VLAN 30 are separate broadcast domains. At this point, the router has not been configured to route traffic between these VLANs.



---


### Part 2: Configure Subinterfaces

#### Step 1: Configure subinterfaces on R1 using the 802.1Q encapsulation.

Click on **R1** -> **CLI** -> then press **Enter**:

````
R1> enable
R1#
````

**Enter global configuration mode:**
````
R1# configure terminal
````




**Create subinterface G0/0.10:**

````
R1(config)# interface gigabitEthernet 0/0.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 172.17.10.1 255.255.255.0
R1(config-subif)# exit
````

Now we configuration for VLAN 10 is complete.

---


**Create subinterface G0/0.30:**
````
R1(config)# interface gigabitEthernet 0/0.30
R1(config-subif)# encapsulation dot1Q 30
R1(config-subif)# ip address 172.17.30.1 255.255.255.0
R1(config-subif)# exit
````


**Finished it:**
````
R1(config)# end
````

**Then verify:**
````
R1# show running-config | section interface GigabitEthernet0/0
````
**Output:**
````
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 shutdown
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 172.17.10.1 255.255.255.0
interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 172.17.30.1 255.255.255.0
````

> The physical interface is ``G0/0``. The virtual subinterfaces are ``G0/0.10`` and ``G0/0.30``.


---



#### Step 2: Verify configuration

##### Check the interface status:

On **R1**, then enter:
````
R1> enable
R1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES unset  administratively down down 
GigabitEthernet0/0.10  172.17.10.1     YES manual administratively down down 
GigabitEthernet0/0.30  172.17.30.1     YES manual administratively down down 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
````

Now we see it:
````
GigabitEthernet0/0.10  172.17.10.1     YES manual administratively down down 
GigabitEthernet0/0.30  172.17.30.1     YES manual administratively down down
````

The subinterfaces depend on their physical parent interface.



##### Enable the physical interface G0/0

````
R1> enable	
R1# configure terminal
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# no shutdown
R1(config-if)# end
````

> Enable the physical interface, not the subinterfaces. Both subinterfaces use the physical G0/0 connection.



##### Verify the interface status again
````
R1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES unset  up                    up 
GigabitEthernet0/0.10  172.17.10.1     YES manual up                    up 
GigabitEthernet0/0.30  172.17.30.1     YES manual up                    up 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
````

Now we see it up:
````
GigabitEthernet0/0.10  172.17.10.1     YES manual up                    up 
GigabitEthernet0/0.30  172.17.30.1     YES manual up                    up
````


---



### Part 3: Test Connectivity with Inter-VLAN Routing


#### Step 1: Ping between PC1 and PC3.

Click on **PC1** -> **Desktop** -> **Command Prompt**, then:
````
ping 172.17.30.10
````
**Output:**
````
Pinging 172.17.30.10 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 172.17.30.10:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
````

In this it still faied.

> The router subinterfaces have been configured, but the switch port connecting S1 to R1 has not yet been configured as a trunk.
>
> **R1** expects to receive **VLAN 10** and **VLAN 30** traffic with their ``802.1Q`` VLAN tags. The switch port is still operating as a normal access port, so it cannot correctly carry both VLANs to the router.


---


#### Step 2: Enable trunking

##### Check which VLAN G0/1 is assigned to

Click on **S1** -> **CLI**:
````
S1> enable
S1# show vlan
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/1
                                                Gig0/2
10   VLAN0010                         active    Fa0/11
30   VLAN0030                         active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
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

In this before trunking, the ``G0/1`` port should normally appear under `VLAN 1    default`.

> In this witch ports are normally assigned to **VLAN 1** by default.



##### Configure G0/1 ad a trunk port

On **S1**, enter:
````
S1# configure terminal
S1(config)# interface gigabitEthernet 0/1
S1(config-if)# switchport mode trunk
S1(config-if)# end
````


> For a **Cisco 2960** switch, we normally do not need switchport trunk encapsulation dot1q; the switch uses ``802.1Q``.


##### Check the VLAN output again
````
S1# show vlan
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/2
10   VLAN0010                         active    Fa0/11
30   VLAN0030                         active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
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

Now we see different 

Before:
````
1    default    active    Fa0/1, Fa0/2, ..., Gig0/1, Gig0/2
````

After:
````
1    default    active    Fa0/1, Fa0/2, ..., Gig0/2
````

> The trunk port ``G0/1`` no longer appears under the access-port membership of **VLAN 1** or another VLAN. Trunk ports carry multiple VLANs rather than belonging to a single access VLAN.


##### Verify trunk configuration

````
S1# show interface trunk
````
<img width="607" height="197" alt="image" src="https://github.com/user-attachments/assets/cb2fd0ba-7ddf-4a6f-ad3f-ba835070c13a" />


The exact mode display can vary by switch and Packet Tracer version. The important information is:

- **Port**: ``Gi0/1``
- **Encapsulation**: ``802.1q``
- **Status**: ``trunking``



Also in this we can inspect the port directly:

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
Trunking Native Mode VLAN: 1 (default)
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



#### Step 3: Test connectivity


Now the router and switch are configured to carry **VLAN 10** and **VLAN 30** traffic.


##### Test PC1's default gateway

Click **PC1** → **Desktop** → **Command Prompt**:
````cmd
ipconfig
````
**Output:**
````cmd
FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: FE80::2D0:BCFF:FEE8:B8A
   IPv6 Address....................: ::
   IPv4 Address....................: 172.17.10.10
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     172.17.10.1

Bluetooth Connection:

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: ::
   IPv6 Address....................: ::
   IPv4 Address....................: 0.0.0.0
   Subnet Mask.....................: 0.0.0.0
   Default Gateway.................: ::
                                     0.0.0.0
````




````
ping 172.17.10.1
````
**Output:**
````
Pinging 172.17.10.1 with 32 bytes of data:

Reply from 172.17.10.1: bytes=32 time<1ms TTL=255
Reply from 172.17.10.1: bytes=32 time<1ms TTL=255
Reply from 172.17.10.1: bytes=32 time<1ms TTL=255
Reply from 172.17.10.1: bytes=32 time<1ms TTL=255

Ping statistics for 172.17.10.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
````

Now we got successful.


---



##### Test PC3's default gateway

Click **PC3** → **Desktop** → **Command Prompt**:

````
ipconfig
````
**Output:**
````
FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: FE80::2D0:BAFF:FEBE:CEAA
   IPv6 Address....................: ::
   IPv4 Address....................: 172.17.30.10
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     172.17.30.1

Bluetooth Connection:

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: ::
   IPv6 Address....................: ::
   IPv4 Address....................: 0.0.0.0
   Subnet Mask.....................: 0.0.0.0
   Default Gateway.................: ::
                                     0.0.0.0
````




````
ping 172.17.30.1
````
**Output:**
````
Pinging 172.17.30.1 with 32 bytes of data:

Reply from 172.17.30.1: bytes=32 time<1ms TTL=255
Reply from 172.17.30.1: bytes=32 time<1ms TTL=255
Reply from 172.17.30.1: bytes=32 time<1ms TTL=255
Reply from 172.17.30.1: bytes=32 time<1ms TTL=255

Ping statistics for 172.17.30.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
````


Now we got successful all.


------

#### Scores


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/b3a2d4f0-6c2e-4f13-8bb8-9256fee1c90b" />



Now we got full score.



-------



