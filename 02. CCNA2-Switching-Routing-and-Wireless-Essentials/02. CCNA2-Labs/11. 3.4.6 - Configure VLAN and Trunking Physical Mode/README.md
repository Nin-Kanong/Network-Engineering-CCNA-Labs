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


















































