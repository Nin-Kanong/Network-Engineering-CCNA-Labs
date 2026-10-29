<img width="870" height="332" alt="image" src="https://github.com/user-attachments/assets/3c852c8d-8955-4d55-a79b-a766c8c7a550" /><h1 align="center"> LAB: 3.4.6 - Configure VLAN and Trunking Physical Mode </h1>


---


### Lab Guide:



---

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| S1 | VLAN 1 | 192.168.1.11 | 255.255.255.0 | N/A |
| S2 | VLAN 1 | 192.168.1.12 | 255.255.255.0 | N/A |
| PC-A | NIC | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 |
| PC-B | NIC | 192.168.10.4 | 255.255.255.0 | 192.168.10.1 |


---


### Objectives

Part 1: Build the Network and Configure Basic Device Settings

Part 2: Create VLANs and Assign Switch Ports

Part 3: Maintain VLAN Port Assignments and the VLAN Database

Part 4: Configure an 802.1Q Trunk Between the Switches


---

## Lab Walkthrough

<img width="980" height="254" alt="image" src="https://github.com/user-attachments/assets/aa7c88d5-a39a-499a-a024-9b40f9d92573" />


<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f08f16f9-6514-43bb-8d91-5c0a889139cf" />


---


### Part 1: Build the Network and Configure Basic Device Settings



#### Step 1: Build the network as shown in the topology.

##### Add devices and connect cables

1. Place **S1** and **S2** in the rack.
2. Place **PC-A** and **PC-B** on the table and **power them on**.
3. Connect the Ethernet cables using **Copper Straight-Through** cables.

| From Device | Port            | To Device | Port             |
| ----------- | --------------- | --------- | ---------------- |
| PC-A        | FastEthernet0   | S1        | FastEthernet0/6  |
| PC-B        | FastEthernet0   | S2        | FastEthernet0/18 |
| S1          | FastEthernet0/1 | S2        | FastEthernet0/1  |

<img width="1260" height="870" alt="image" src="https://github.com/user-attachments/assets/32f0f1d8-b2ee-423f-956e-0b7d1a362c07" />


<img width="1232" height="871" alt="image" src="https://github.com/user-attachments/assets/b92b9b0e-5185-49b6-aa02-7d5b299dd021" />


<img width="1615" height="870" alt="image" src="https://github.com/user-attachments/assets/8130545f-9a82-4698-86ea-bc215411acc8" />


<img width="1201" height="493" alt="image" src="https://github.com/user-attachments/assets/3dc04998-f741-4f5e-8dca-db8b4e0e9025" />


<img width="1235" height="876" alt="image" src="https://github.com/user-attachments/assets/1ad79087-9016-463a-9832-1bd2c65730fb" />


<img width="1453" height="703" alt="image" src="https://github.com/user-attachments/assets/75c4d0f5-9f0c-4cff-aca9-273f7f2cf9c6" />


<img width="1237" height="870" alt="image" src="https://github.com/user-attachments/assets/a962f207-1f65-40a3-8b8a-52cef5ab455a" />


<img width="1453" height="662" alt="image" src="https://github.com/user-attachments/assets/61677e4a-9e12-4ab9-bb14-4930cba6055a" />


<img width="1235" height="870" alt="image" src="https://github.com/user-attachments/assets/7109d40f-844f-4d33-a72f-8c6e9570e238" />



In this click on **Console Cable** -> Input in **RS 232** -> `Right-Click` on **S1** the select on `Ins[ect Rear`:

<img width="1472" height="742" alt="image" src="https://github.com/user-attachments/assets/682bc9c1-c6d7-449e-9378-7b4c972e260c" />


Then input it in console:

<img width="1435" height="673" alt="image" src="https://github.com/user-attachments/assets/ba01e86f-55d3-455c-922b-aeb84501bd41" />


<img width="1448" height="673" alt="image" src="https://github.com/user-attachments/assets/7714ae87-5fe1-475a-8239-221d862d48ba" />



Then on **PC-B**, in this we do the same:

In this click on **Console Cable** -> Input in **RS 232** -> `Right-Click` on **S1** the select on `Ins[ect Rear`:

<img width="1230" height="868" alt="image" src="https://github.com/user-attachments/assets/a9b4124a-6ee0-4e1b-ab08-c742d77f318c" />


<img width="1452" height="793" alt="image" src="https://github.com/user-attachments/assets/10ed9f39-d66b-4ca8-b2ae-ba9fbca9b2a6" />


<img width="1445" height="666" alt="image" src="https://github.com/user-attachments/assets/a4d70893-9a77-4fc8-9f13-b1f5e91f44f0" />



<img width="1282" height="676" alt="image" src="https://github.com/user-attachments/assets/6d4bf5cc-8be6-4c84-947e-3c25bd38a1c7" />




Then don't forget to **Power On** **PC-A** and **PC-B**:

<img width="1432" height="687" alt="image" src="https://github.com/user-attachments/assets/3e3c954c-9051-4e4a-9332-8e6f42fe7de9" />


---


#### Step 2: Configure basic settings for each switch.

##### Configure S1

On **PC-A**, open **Desktop** → **Terminal**, accept the default serial settings, and enter:

<img width="877" height="410" alt="image" src="https://github.com/user-attachments/assets/42703fb9-118b-46b1-aa6e-2235620a3f19" />

Then enter:

**Configure the Hostname and Enable Secret:**
````cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# enable secret class
````

**Configure the Console Line:**
````cisco
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
````

**Configure the VTY Lines:**
````cisco
S1(config)# line vty 0 15
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
````


**Enable Password Encryption and Configure the Banner:**
````cisco
S1(config)# service password-encryption
S1(config)# banner motd #WARNING: Unauthorized access is prohibited!#
````


**Configure the Management Interface:**
````cisco
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.11 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
````

> Shut down unused ports while keeping the ports we need operational. In keep ``F0/1`` and ``F0/6`` active on **S1**.


````cisco
S1(config)# interface range f0/2-5,f0/7-24
S1(config-if-range)# shutdown
S1(config-if-range)# exit
S1(config)# interface range g0/1-2
S1(config-if-range)# shutdown
S1(config-if-range)# end
S1# clock set 10:00:00 29 October 2026
S1# copy running-config startup-config
````
> Press **Enter** if prompted for the destination filename.


---


##### Configure S1

On **PC-B**, open **Desktop** → **Terminal**:

<img width="872" height="381" alt="image" src="https://github.com/user-attachments/assets/00d1b7e3-b7db-4333-ab89-be5a20e08e49" />


Then press **Enter** if it show prompt.

The type:

**Configure the Hostname and Password:**
````cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname S2
S2(config)# enable secret class
````

**Configure the Console Line:**
````cisco
S2(config)# line console 0
S2(config-line)# password cisco
S2(config-line)# login
S2(config-line)# exit
````

**Configure the VTY Lines:**
````
S2(config)# line vty 0 15
S2(config-line)# password cisco
S2(config-line)# login
S2(config-line)# exit
````


**Enable Password Encryption and Configure the Banner:**
````cisco
S2(config)# service password-encryption
S2(config)# banner motd #WARNING: Unauthorized access is prohibited!#
````

**Configure the Management Interface:**
````cisco
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.1.12 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
````

**Disable Unused FastEthernet Ports:**
````cisco
S2(config)# interface range f0/2-17,f0/19-24
S2(config-if-range)# shutdown
S2(config-if-range)# exit
````

**Disable Unused Gigabit Ethernet Ports:**
````
S2(config)# interface range g0/1-2
S2(config-if-range)# shutdown
S2(config-if-range)# end
````

**Set the Clock:**
````cisco
S2# clock set 10:00:00 29 October 2026
````

**Save the Configuration:**
````cisco
S2# copy running-config startup-config
````

> Keep ``F0/1`` and ``F0/18`` active on **S2**. If the **PC** is connected to a different port in our topology, adjust the port ranges accordingly.


---


#### Step 3: Configure PC hosts.

For each **PC**, open **Desktop** → **IP Configuration**.

##### PC-A Configuration

| Setting         | Value           |
| --------------- | --------------- |
| IPv4 address    | `192.168.10.3`  |
| Subnet mask     | `255.255.255.0` |
| Default gateway | `192.168.10.1`  |

<img width="873" height="681" alt="image" src="https://github.com/user-attachments/assets/ec6ea1cb-4fda-4fc5-85be-0d5e9c7f2f27" />



##### PC-B Configuration

| Setting         | Value           |
| --------------- | --------------- |
| IPv4 address    | `192.168.10.4`  |
| Subnet mask     | `255.255.255.0` |
| Default gateway | `192.168.10.1`  |

<img width="871" height="665" alt="image" src="https://github.com/user-attachments/assets/217424c7-7c26-40ac-959b-84a75b2a131e" />


---


#### Step 4: Test connectivity.

On **PC-A**, open **Command Prompt**:
````
ping 192.168.10.4
ping 192.168.1.11
````

<img width="870" height="567" alt="image" src="https://github.com/user-attachments/assets/3b45b869-c150-4d26-b6f0-b8b4c524f7a4" />


**On PC-B:**
````
ping 192.168.1.12
````
<img width="871" height="383" alt="image" src="https://github.com/user-attachments/assets/5c8d6a8e-d6d4-4520-9603-c70121aff3fb" />


**On S1:**

In this just click on **PC-A** -> **Desktop** -> **Terminal**, then click **Ok**:
````
S1# ping 192.168.1.12
````
**Output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.12, timeout is 2 seconds:
..!!!
Success rate is 60 percent (3/5), round-trip min/avg/max = 0/0/0 ms
````


Now the result is:

| Test        | Expected result | Explanation                                                                                                                    |
| ----------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| PC-A → PC-B | succeed     | Both PCs are in the same subnet, `192.168.10.0/24`, and can communicate if their switch ports are active and in the same VLAN. |
| PC-A → S1   | Fails           | They are in different IP subnets: `192.168.10.0/24` and `192.168.1.0/24`. No router is configured to route between them.       |
| PC-B → S2   | Fails           | They are in different IP subnets, and no router is configured to route between them.                                           |
| S1 → S2     | Succeeds        | Both switch management addresses are in `192.168.1.0/24` and initially use VLAN 1, assuming the inter-switch link is active.   |

----



### Part 2: Create VLANs and Assign Switch Ports

In this we will create these four VLANs on both swtiches.

| VLAN ID | VLAN Name     | Purpose                   |
| ------- | ------------- | ------------------------- |
| 10      | `Operations`  | User data VLAN            |
| 20      | `Parking_Lot` | Unused-port VLAN          |
| 99      | `Management`  | Switch management         |
| 1000    | `Native`      | Native VLAN for the trunk |


---


#### Step 1: Create VLANs on the switches.

##### Create VLANs on S1

Click on **PC-A** -> **Desktop** -> **Terminal**, then Enter:

````
S1> enable
S1# configure terminal
````

**VLAN 10:**
````cisco
S1(config)# vlan 10
S1(config-vlan)# name Operations
````

**VLAN 20:**
````
S1(config-vlan)# vlan 20
S1(config-vlan)# name Parking_Lot
````

**VLAN 99:**
````cisco
S1(config-vlan)# vlan 99
S1(config-vlan)# name Management
````

**VLAN 1000:**
````
S1(config-vlan)# vlan 1000
S1(config-vlan)# name Native
````

**Exit:**
````
S1(config-vlan)# end
````


**Then verify:**
````cisco
S1# show vlan brief
````
**Output:**
````text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
10   Operations                       active    
20   Parking_Lot                      active    
99   Management                       active    
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


---


##### Create VLANs on S2

Click on **PC-B** -> **Desktop** -> **Terminal**, then Enter:

````cisco
S1> enable
S2# configure terminal
````

**VLAN 10:**
````cisco
S2(config)# vlan 10
S2(config-vlan)# name Operations
````

**VLAN 20:**
````cisco
S2(config-vlan)# vlan 20
S2(config-vlan)# name Parking_Lot
````

**VLAN 99:**
````cisco
S2(config-vlan)# vlan 99
S2(config-vlan)# name Management
````

**VLAN 1000**
````cisco
S2(config-vlan)# vlan 1000
S2(config-vlan)# name Native
````

**Exit:**
````cisco
S2(config-vlan)# end
````


**Then verify:**
````cisco
S1# show vlan brief
````

**Output:**
````text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
10   Operations                       active    
20   Parking_Lot                      active    
99   Management                       active    
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---


#### Step 2: Assign VLANs to the correct switch interfaces.

##### Assign PC-A to VLAN 10 on S1

Click on **PC-A** -> **Desktop** -> **Terminal**:

> **Note**: In this after we go to terminal again it will require password, so in this password is `cisco`.

> **Note**: in this we we type `enable` it also requre passwrd, also the password is `class`.

````cisco
S1> enable
Password: class
S1#
````

````cisco
S1# configure terminal
S1(config)# interface f0/6
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 10
S1(config-if)# no shutdown
S1(config-if)# exit
````

Move **S1**'s management IP address from **VLAN 1** to **VLAN 99**:
````
S1(config)# interface vlan 1
S1(config-if)# no ip address
S1(config-if)# exit
S1(config)# interface vlan 99
S1(config-if)# ip address 192.168.1.11 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# end
````


**Then verify:**
````cisco
S1# show vlan brief
````
**Output:**
````text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/1
                                                Gig0/2
10   Operations                       active    Fa0/6
20   Parking_Lot                      active    
99   Management                       active    
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


````cisco
S1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual administratively down down 
FastEthernet0/3        unassigned      YES manual administratively down down 
FastEthernet0/4        unassigned      YES manual administratively down down 
FastEthernet0/5        unassigned      YES manual administratively down down 
FastEthernet0/6        unassigned      YES manual up                    up 
FastEthernet0/7        unassigned      YES manual administratively down down 
FastEthernet0/8        unassigned      YES manual administratively down down 
FastEthernet0/9        unassigned      YES manual administratively down down 
FastEthernet0/10       unassigned      YES manual administratively down down 
FastEthernet0/11       unassigned      YES manual administratively down down 
FastEthernet0/12       unassigned      YES manual administratively down down 
FastEthernet0/13       unassigned      YES manual administratively down down 
FastEthernet0/14       unassigned      YES manual administratively down down 
FastEthernet0/15       unassigned      YES manual administratively down down 
FastEthernet0/16       unassigned      YES manual administratively down down 
FastEthernet0/17       unassigned      YES manual administratively down down 
FastEthernet0/18       unassigned      YES manual administratively down down 
FastEthernet0/19       unassigned      YES manual administratively down down 
FastEthernet0/20       unassigned      YES manual administratively down down 
FastEthernet0/21       unassigned      YES manual administratively down down 
FastEthernet0/22       unassigned      YES manual administratively down down 
FastEthernet0/23       unassigned      YES manual administratively down down 
FastEthernet0/24       unassigned      YES manual administratively down down 
GigabitEthernet0/1     unassigned      YES manual administratively down down 
GigabitEthernet0/2     unassigned      YES manual administratively down down 
Vlan1                  unassigned      YES manual up                    up 
Vlan99                 192.168.1.11    YES manual up                    down
````


> The SVI may initially show ``down/down`` because VLAN 99 has no active access port or trunk carrying that VLAN. Once a port in **VLAN 99** becomes active, or the trunk carries **VLAN 99** with an active link, the SVI can become ``up/up``.

---


##### Assign PC-B to VLAN 10 on S2

Click on **PC-A** -> **Desktop** -> **Terminal**, then click **Ok**, and press **Enter**:


````cisco
S2> enable
Password: class
S2#
````

````cisco
S2# configure terminal
S2(config)# interface f0/18
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 10
S2(config-if)# no shutdown
S2(config-if)# exit
````

Move **S2**'s management address to **VLAN 99**:

````cisco
S2(config)# interface vlan 1
S2(config-if)# no ip address
S2(config-if)# exit
S2(config)# interface vlan 99
S2(config-if)# ip address 192.168.1.12 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# end
````

**Then verify:**
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
                                                Fa0/17, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24, Gig0/1
                                                Gig0/2
10   Operations                       active    Fa0/18
20   Parking_Lot                      active    
99   Management                       active    
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


````cisco
S2# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual administratively down down 
FastEthernet0/3        unassigned      YES manual administratively down down 
FastEthernet0/4        unassigned      YES manual administratively down down 
FastEthernet0/5        unassigned      YES manual administratively down down 
FastEthernet0/6        unassigned      YES manual administratively down down 
FastEthernet0/7        unassigned      YES manual administratively down down 
FastEthernet0/8        unassigned      YES manual administratively down down 
FastEthernet0/9        unassigned      YES manual administratively down down 
FastEthernet0/10       unassigned      YES manual administratively down down 
FastEthernet0/11       unassigned      YES manual administratively down down 
FastEthernet0/12       unassigned      YES manual administratively down down 
FastEthernet0/13       unassigned      YES manual administratively down down 
FastEthernet0/14       unassigned      YES manual administratively down down 
FastEthernet0/15       unassigned      YES manual administratively down down 
FastEthernet0/16       unassigned      YES manual administratively down down 
FastEthernet0/17       unassigned      YES manual administratively down down 
FastEthernet0/18       unassigned      YES manual up                    up 
FastEthernet0/19       unassigned      YES manual administratively down down 
FastEthernet0/20       unassigned      YES manual administratively down down 
FastEthernet0/21       unassigned      YES manual administratively down down 
FastEthernet0/22       unassigned      YES manual administratively down down 
FastEthernet0/23       unassigned      YES manual administratively down down 
FastEthernet0/24       unassigned      YES manual administratively down down 
GigabitEthernet0/1     unassigned      YES manual administratively down down 
GigabitEthernet0/2     unassigned      YES manual administratively down down 
Vlan1                  unassigned      YES manual up                    up 
Vlan99                 192.168.1.12    YES manual up                    down
````


> Can **S1** ping **S2**? Initially, likely not if VLAN 99 is not yet carried over an active trunk.
>
> > Can **PC-A** ping **PC-B**? They may not communicate across switches until the trunk is configured to carry **VLAN 10**.

----



### Part 3: Maintain VLAN Port Assignments and the VLAN Database

#### Step 1: Assign a VLAN to multiple interfaces.

Click on **PC-A** -> **Desktop** -> **Terminal**:

````cisco
S1> enable 
Password: class
S1#
````

````cisco
S1# configure terminal
S1(config)# interface range f0/11-24
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 99
S1(config-if-range)# end
````


**Verify:**
````cisco
S1# show vlan brief
````
**Output:**
````cisco
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Gig0/1, Gig0/2
10   Operations                       active    Fa0/6
20   Parking_Lot                      active    
99   Management                       active    Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


Reassign **F0/11** and **F0/21** to **VLAN 10**:
````
S1# configure terminal
S1(config)# interface range f0/11,f0/21
S1(config-if-range)# switchport access vlan 10
S1(config-if-range)# end
````



---



#### Step 2: Remove a VLAN assignment from an interface

Remove the VLAN assignment from F0/24:
````cisco
S1# configure terminal
S1(config)# interface f0/24
S1(config-if)# no switchport access vlan
S1(config-if)# end
````

**Verify:**
````cisco
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/24, Gig0/1, Gig0/2
10   Operations                       active    Fa0/6, Fa0/11, Fa0/21
20   Parking_Lot                      active    
99   Management                       active    Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/22, Fa0/23
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> In this it returns to the default access VLAN, VLAN 1.


---

##### Create VLAN 30 by assigning it to F0/24
````cisco
S1# configure terminal
S1(config)# interface f0/24
S1(config-if)# switchport access vlan 30
end
````

> On some Cisco switches, this creates VLAN 30 automatically if it does not already exist.


**Verify:**
````cisco
S1# show vlan brief
````

**Output:**
````text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Gig0/1, Gig0/2
10   Operations                       active    Fa0/6, Fa0/11, Fa0/21
20   Parking_Lot                      active    
30   VLAN0030                         active    Fa0/24
99   Management                       active    Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/22, Fa0/23
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


> ``VLAN0030`` (the default VLAN name format).

---


##### Delete VLAN 30
````
S1# configure terminal
S1(config)# no vlan 30
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
                                                Fa0/10, Gig0/1, Gig0/2
10   Operations                       active    Fa0/6, Fa0/11, Fa0/21
20   Parking_Lot                      active    
99   Management                       active    Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/22, Fa0/23
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


---

##### Reset F0/24 to VLAN 1
````cisco
S1# configure terminal
S1(config)# interface f0/24
S1(config-if)# no switchport access vlan
S1(config-if)# end
````

**Verify:**
````cisco
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/24, Gig0/1, Gig0/2
10   Operations                       active    Fa0/6, Fa0/11, Fa0/21
20   Parking_Lot                      active    
99   Management                       active    Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/22, Fa0/23
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


> ``F0/24`` now belongs to **VLAN 1**.

-----



### Part 4: Configure an 802.1Q Trunk Between the Switches

The **trunk** uses **FastEthernet0/1** on **both switches**.

#### Step 1: Use DTP to initiate trunking on F0/1.

##### On S1:

````cisco
S1# configure terminal
S1(config)# interface f0/1
S1(config-if)# switchport mode dynamic desirable
S1(config-if)# no shutdown
S1(config-if)# end
````

**S2**'s **F0/1** can remain in the default ``dynamic auto`` mode for this negotiation step, provided it has not been shut down.


**Verify:**
````cisco
S1# show interfaces trunk
````

**Output:**
````text
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       desirable    n-802.1q       trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       none
````



**Verify on S2**:

````
S2# show interfaces trunk
````

**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       auto         n-802.1q       trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````

We should see ``F0/1`` operating as a trunk after negotiation succeeds.

---

##### Verify trunk operation
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       auto         n-802.1q       trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````

````
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
10   Operations                       active    Fa0/18
20   Parking_Lot                      active    
99   Management                       active    
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

> Trunk ports are not listed as normal access ports in ``show vlan brief``.


Test on **S1**:
````
S1# ping 192.168.1.12
````
**output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.12, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/3/6 ms
````

**From PC-A:**

On **PC-A** -> **Desktop** -> **Command Prompt**:
````
ping 192.168.10.4
````
<img width="870" height="440" alt="image" src="https://github.com/user-attachments/assets/74999a66-a0a0-4ac7-991c-2847ac4d3be9" />


> The PCs should be able to communicate once **VLAN 10** is correctly assigned on both access ports and **VLAN 10** is carried across the trunk.

> The switch management ping also depends on **VLAN 99** being active across the trunk.

---



#### Step 2: Manually configure trunk interface F0/1.


##### On **S1**:
````
S1# configure terminal
S1(config)# interface f0/1
S1(config-if)# switchport mode trunk
S1(config-if)# end
````


Then verify it:
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````



##### On S2:
````cisco
S2# configure terminal
S2(config)# interface f0/1
S2(config-if)# switchport mode trunk
S2(config-if)# end
````


Verify:
````
S2# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````

---


##### Configure native VLAN 1000

**On S1:**
````cisco
S1# configure terminal
S1(config)# interface f0/1
S1(config-if)# switchport trunk native vlan 1000
S1(config-if)# end
````


**Verify:**
````
S1# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````


**On S2:**
````cisco
S2# configure terminal
S2(config)# interface f0/1
S2(config-if)# switchport trunk native vlan 1000
S2(config-if)# end
````

**Verify:**
````
S2# show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       1-1005

Port        Vlans allowed and active in management domain
Fa0/1       1,10,20,99,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1,10,20,99,1000
````

> The native VLAN should show 1000 on both sides.

---

#### Reflection questions

1. What is needed to allow hosts on VLAN 10 to communicate to hosts on VLAN 99?

> Inter-VLAN routing using a router or a Layer 3 switch, with appropriate IP addresses and routing configuration.

2. What are some primary benefits that an organization can receive through effective use of VLANs?

> 1. VLANs reduce broadcast domains, improve traffic organization, support logical segmentation, and help separate groups of users or devices for security and administration.

------


#### Scores

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/755ea282-d125-47fb-8d33-46bb79b944c9" />


Now we got full score.


**Now we completed the lab.**

------
