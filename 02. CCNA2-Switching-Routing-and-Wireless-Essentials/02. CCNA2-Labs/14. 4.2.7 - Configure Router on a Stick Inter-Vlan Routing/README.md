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

Then:
````
ping 172.17.30.10
````

























































































