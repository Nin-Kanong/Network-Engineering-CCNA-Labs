<h1 align="center"> LAB: 3.3.12 - VLAN Configuration </h1> 



---


### Lab Guide

[3.3.12 Packet Tracer - VLAN Configuration.docx](https://github.com/user-attachments/files/34070479/3.3.12.Packet.Tracer.-.VLAN.Configuration.docx)


---


### Addressing Table

| Device | Interface | IP Address | Subnet Mask | VLAN |
|---|---|---|---|---|
| PC1 | NIC | 172.17.10.21 | 255.255.255.0 | 10 |
| PC2 | NIC | 172.17.20.22 | 255.255.255.0 | 20 |
| PC3 | NIC | 172.17.30.23 | 255.255.255.0 | 30 |
| PC4 | NIC | 172.17.10.24 | 255.255.255.0 | 10 |
| PC5 | NIC | 172.17.20.25 | 255.255.255.0 | 20 |
| PC6 | NIC | 172.17.30.26 | 255.255.255.0 | 30 |


---

### Objectives

**Part 1: Verify the Default VLAN Configuration**

**Part 2: Configure VLANs**

**Part 3: Assign VLANs to Ports**

---


## Lab Walkthrough

<img width="1307" height="622" alt="image" src="https://github.com/user-attachments/assets/93706faa-dfa9-4fdb-946f-93128913dd20" />


---


### Part 1: View the Default VLAN Configuration

#### Step 1: Display the current VLANs

1. Click **S1** switch.
2. In **CLI**.
3. Press **Enter**.
4. Enter privileged EXEC mode:

````
S1>enable
S1#
````

````cisco
S1#show vlan brief
````
**Output:**
````cisco
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active   
````

By default, access ports belong to **VLAN 1**.

> The default configuration places switch ports in **VLAN 1** until they are assigned to other **VLANs**.



#### Step 2: Verify connectivity between PCs on the same network.

Open **PC1** → **Desktop** → **Command Prompt**:
````
ping 172.17.10.24
````
**Output**:
````cisco
Pinging 172.17.10.24 with 32 bytes of data:

Reply from 172.17.10.24: bytes=32 time<1ms TTL=128
Reply from 172.17.10.24: bytes=32 time<1ms TTL=128
Reply from 172.17.10.24: bytes=32 time<1ms TTL=128
Reply from 172.17.10.24: bytes=32 time=1ms TTL=128

Ping statistics for 172.17.10.24:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
````


Repeat these tests:
| Source PC | Command | Destination |
|---|---|---|
| PC1 | `ping 172.17.10.24` | PC4 |
| PC2 | `ping 172.17.20.25` | PC5 |
| PC3 | `ping 172.17.30.26` | PC6 |

> These pings should succeed because each pair is in the same IPv4 subnet and, before VLAN configuration, the connected ports are in the default VLAN.


---


### Part 2: Configure VLANs


#### Step 1: Create and name VLANs on S1.

Click **S1** → **CLI** and **Enter**:

````
S1> enable
S1# configure terminal
````

````cisco
S1(config)# vlan 10
S1(config-vlan)# name Faculty/Staff
S1(config-vlan)# exit
````

````cisco
S1(config)# vlan 20
S1(config-vlan)# name Students
S1(config-vlan)# exit
````


````cisco
S1(config)# vlan 30
S1(config-vlan)# name Guest(Default)
S1(config-vlan)# exit
````


````cisco
S1(config)# vlan 99
S1(config-vlan)# name Management&Native
S1(config-vlan)# exit
````


````cisco
S1(config)# vlan 150
S1(config-vlan)# name VOICE
S1(config-vlan)# exit
````

````cisco
S1(config)# end
````
**Output:**
````
S1#
%SYS-5-CONFIG_I: Configured from console by console
````


> VLAN names are case-sensitive. Type them exactly as shown, including the capitalization, parentheses, slash, and ampersand.


---


#### Step 2: Verify the VLANs on S1
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
10   Faculty/Staff                    active    
20   Students                         active    
30   Guest(Default)                   active    
99   Management&Native                active    
150  VOICE                            active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

Not it active all.

---


#### Step 3: Create the VLANs on S2 and S3.

##### Create the same VLANs on S2

Click **S2** → **CLI** and **Enter**:

````cisco
S2> enable
S2# configure terminal
````


````cisco
S2(config)# vlan 10
S2(config-vlan)# name Faculty/Staff
S2(config-vlan)# exit
````

````cisco
S2(config)# vlan 20
S2(config-vlan)# name Students
S2(config-vlan)# exit
````


````cisco
S2(config)# vlan 30
S2(config-vlan)# name Guest(Default)
S2(config-vlan)# exit
````

````cisco
S2(config)# vlan 99
S2(config-vlan)# name Management&Native
S2(config-vlan)# exit
````

````cisco
S2(config)# vlan 150
S2(config-vlan)# name VOICE
S2(config-vlan)# exit
````


````cisco
S2(config)# end
````
**Output:**
````
S2#
%SYS-5-CONFIG_I: Configured from console by console
````


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
10   Faculty/Staff                    active    
20   Students                         active    
30   Guest(Default)                   active    
99   Management&Native                active    
150  VOICE                            active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> Now it confirm that all five VLANs are active.



##### Create the same VLANs on S3

Click **S3** → **CLI** and **Enter**:
````cisco
S3> enable
S3# configure terminal
````

````cisco
S3(config)# vlan 10
S3(config-vlan)# name Faculty/Staff
S3(config-vlan)# exit
````


````cisco
S3(config)# vlan 20
S3(config-vlan)# name Students
S3(config-vlan)# exit
````


````cisco
S3(config)# vlan 30
S3(config-vlan)# name Guest(Default)
S3(config-vlan)# exit
````


````cisco
S3(config)# vlan 99
S3(config-vlan)# name Management&Native
S3(config-vlan)# exit
````


````cisco
S3(config)# vlan 150
S3(config-vlan)# name VOICE
S3(config-vlan)# exit
````


````cisco
S3(config)#end
````

**Output:**
````
S3#
%SYS-5-CONFIG_I: Configured from console by console
````


````
S3# show vlan brief
````
**Output:**
````cisco
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
99   Management&Native                active    
150  VOICE                            active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

Verify that **S3** has the same five VLANs.

----



### Part 3: Assign VLANs to Ports

Follow the interface assignments exactly as specified.


#### Step 1: Assign VLANs to the active ports on S2.

The required assignments are:

| S2 Interface | Connected Device | VLAN | VLAN Name |
|---|---|---|---|
| FastEthernet0/11 | PC1 | 10 | Faculty/Staff |
| FastEthernet0/18 | PC2 | 20 | Students |
| FastEthernet0/6 | PC3 | 30 | Guest (Default) |


On **S2** → **CLI**, **Enter**:

````cisco
S2> enable
S2# configure terminal
````


````cisco
S2(config)# interface fastEthernet 0/11
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 10
S2(config-if)# exit
````


````cisco
S2(config)# interface fastEthernet 0/18
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 20
S2(config-if)# exit
````


````cisco
S2(config)# interface fastEthernet 0/6
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 30
S2(config-if)# exit
````


````
S2(config)# end
````
**Output**:
````
S2#
%SYS-5-CONFIG_I: Configured from console by console
````


Then verify it:
````
S2# show vlan brief
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
99   Management&Native                active    
150  VOICE                            active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````
Now we see:
````
10   Faculty/Staff                    active    Fa0/11
20   Students                         active    Fa0/18
30   Guest(Default)                   active    Fa0/6
````



---


#### Step 2: Assign VLANs to the active ports on S3.

The required assignments are:

| S3 Interface | Connected Device | Data VLAN |
|---|---|---|
| FastEthernet0/11 | IP phone and PC4 | 10 |
| FastEthernet0/18 | PC5 | 20 |
| FastEthernet0/6 | PC6 | 30 |

On **S3** → **CLI**, **Enter**:
````cisco
S3> enable
S3# configure terminal
````


````cisco
S3(config)# interface fastEthernet 0/11
S3(config-if)# switchport mode access
S3(config-if)# switchport access vlan 10
S3(config-if)#`exit
````


````cisco
S3(config)# interface fastEthernet 0/18
S3(config-if)# switchport mode access
S3(config-if)# switchport access vlan 20
S3(config-if)# exit
````


````cisco
S3(config)# interface fastEthernet 0/6
S3(config-if)# switchport mode access
S3(config-if)# switchport access vlan 30
S3(config-if)# exit
````


````
S3(config)# end
````
**Output:**
````
S3#
%SYS-5-CONFIG_I: Configured from console by console
````

---


#### Step 3: Assign the VOICE VLAN to FastEthernet 0/11 on S3.

This step allows the same physical port to carry data traffic for **PC4** and voice traffic for the IP phone.


On **S3** -> **CLI** -> **Enter**:
````cisco
S3> enable
S3# configure terminal
S3(config)# interface fastEthernet 0/11
S3(config-if)# mls qos trust cos
S3(config-if)# switchport voice vlan 150
S3(config-if)# end
````

> The port should remain an access port for the PC's data traffic, with the additional voice VLAN for the phone.



Verify the voice VLAN:
````cisco
S3# show interfaces fastEthernet 0/11 switchport
````
**Output:**
````
Name: Fa0/11
Switchport: Enabled
Administrative Mode: static access
Operational Mode: static access
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
Access Mode VLAN: 10 (Faculty/Staff)
Trunking Native Mode VLAN: 1 (default)
Voice VLAN: 150
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

In this looking for:
````
Access Mode VLAN: 10 (Faculty/Staff)
Voice VLAN: 150
````

---


#### Step 4: Verify loss of connectivity

> This is an important diagnostic part of the activity. Do not configure trunk ports yet because we need to observe the failure first.


##### Check S2's VLAN configuration

On **S2** -> **CLI** -> run:
````cisco
S2# show vlan brief
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
99   Management&Native                active    
150  VOICE                            active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> In this we Notice that the uplink ``Gig0/1`` remains in **VLAN 1**.





##### Ping PC4 from PC1

Click **PC1** → **Desktop** → **Command Prompt** and run:
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

Now in this it failed.

> The ping fails because **PC1** and **PC4** belong to **VLAN 10**, but the inter-switch connections are still in **VLAN 1** instead of carrying **VLAN 10** between switches. As a result, **VLAN 10** traffic cannot cross the switch-to-switch links correctly.


Now we completed the Lab.


-----



#### Score


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/c4700ee7-86cb-44e7-9406-fbb76b97969e" />


Now we got full score.


------
