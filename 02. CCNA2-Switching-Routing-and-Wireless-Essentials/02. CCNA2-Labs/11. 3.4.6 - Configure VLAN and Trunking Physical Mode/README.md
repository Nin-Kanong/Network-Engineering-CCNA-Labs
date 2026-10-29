<h1 align="center"> LAB: 3.4.6 - Configure VLAN and Trunking Physical Mode </h1>


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
````cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# enable secret class
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
S1(config)# line vty 0 15
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
S1(config)# service password-encryption
S1(config)# banner motd #WARNING: Unauthorized access is prohibited!#
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
````cisco
Switch> enable
Switch# configure terminal
Switch(config)# hostname S2
S2(config)# enable secret class
S2(config)# line console 0
S2(config-line)# password cisco
S2(config-line)# login
S2(config-line)# exit
S2(config)# line vty 0 15
S2(config-line)# password cisco
S2(config-line)# login
S2(config-line)# exit
S2(config)# service password-encryption
S2(config)# banner motd #WARNING: Unauthorized access is prohibited!#
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.1.12 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
S2(config)# interface range f0/2-17,f0/19-24
S2(config-if-range)# shutdown
S2(config-if-range)# exit
S2(config)# interface range g0/1-2
S2(config-if-range)# shutdown
S2(config-if-range)# end
S2# clock set 10:00:00 29 October 2026
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

























