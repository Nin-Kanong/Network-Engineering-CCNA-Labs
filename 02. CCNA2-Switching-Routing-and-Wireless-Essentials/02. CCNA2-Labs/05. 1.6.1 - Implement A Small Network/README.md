<h1 align="center"> LAB: 1.6.1 - Implement A Small Network </h1>



---


### Lab Guide

[1.6.1 Packet Tracer - Implement a Small Network.docx](https://github.com/user-attachments/files/34034585/1.6.1.Packet.Tracer.-.Implement.a.Small.Network.docx)


---


### Addressing Table

| Device | Interface | Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| RTA | G0/0 | 10.10.10.1 | 255.255.255.0 | N/A |
| RTA | G0/1 | 10.10.20.1 | 255.255.255.0 | N/A |
| SW1 | VLAN 1 | 10.10.10.2 | 255.255.255.0 | 10.10.10.1 |
| SW2 | VLAN 1 | 10.10.20.2 | 255.255.255.0 | 10.10.20.1 |
| PC-1 | NIC | Blank | 255.255.255.0 | Blank |
| PC-2 | NIC | Blank | 255.255.255.0 | Blank |


---

### Objectives

- **Part 1**: Create the Network Topology
- **Part 2**: Configure Devices and Verify Connectivity


---


## **Lab Walkthrough**


### Part 1: Create the Network Topology

#### Step 1: Obtain the required devices.

| Quantity | Device | Location in Packet Tracer | Model |
|---|---|---|---|
| 1 × | Router | Network Devices → Routers | 1941 |
| 2 × | Switches | Network Devices → Switches | 2960 |
| 2 × | PCs | End Devices → PC | PC-PT |



Arrange the devices in this general layout:

````mermaid
flowchart TD
    %% Router
    RTA["🖧 <b>RTA</b><br/>Router"]
    
    %% Interfaces branching from Router
    RTA ---|G0/0| SW1
    RTA ---|G0/1| SW2
    
    %% Switches
    SW1["🔀 <b>SW1</b><br/>Switch"]
    SW2["🔀 <b>SW2</b><br/>Switch"]
    
    %% End Devices
    SW1 ---|Fa0/1| PC1["🖥️ <b>PC-1</b>"]
    SW2 ---|Fa0/1| PC2["🖥️ <b>PC-2</b>"]

    %% Styling to match the clean look
    classDef router fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#fff;
    classDef switch fill:#2b6cb0,stroke:#2c5282,stroke-width:2px,color:#fff;
    classDef pc fill:#2f855a,stroke:#276749,stroke-width:2px,color:#fff;
    
    class RTA router;
    class SW1,SW2 switch;
    class PC1,PC2 pc;
````

<img width="1000" height="552" alt="image" src="https://github.com/user-attachments/assets/672a3c2b-e8c9-4426-bd05-911591253080" />


---

#### Step 2: Name the devices.

Change the display name beneath each device icon to exactly match this table:
| Device Type | Required Display Name |
|---|---|
| Router | `RTA` |
| First switch | `SW1` |
| Second switch | `SW2` |
| First PC | `PC-1` |
| Second PC | `PC-2` |

<img width="975" height="537" alt="image" src="https://github.com/user-attachments/assets/463d6c2e-08ea-4b59-9835-22c2b3d9dec7" />


---


#### Step 3: Connect the devices.

Select **Connections** (the orange lightning-bolt icon) and choose **Copper Straight-Through**:

| From Device | Port | To Device | Port |
|---|---|---|---|
| RTA | `G0/0` | SW1 | `G0/1` |
| RTA | `G0/1` | SW2 | `G0/1` |
| SW1 | `F0/1` | PC-1 | `FastEthernet0` |
| SW2 | `F0/1` | PC-2 | `FastEthernet0` |


<img width="890" height="527" alt="image" src="https://github.com/user-attachments/assets/1a5aba60-d78d-4902-a515-f57edc8d305e" />


> Wait for the connections to become active. Switch ports may initially display orange while spanning-tree processing takes place; allow time for them to turn green.


----



### Part 2: Configure Devices


#### Step 1: Configure the router.

Click **RTA** → **CLI** and press **Enter**:

<img width="866" height="857" alt="image" src="https://github.com/user-attachments/assets/2bbb5c1e-f940-4927-9b8d-a6f03f8d74b9" />


Enter privileged EXEC mode:
````
Router> enable
Router#
````

Enter global configuration mode:
````
Router# configure terminal
Router(config)#
````



##### Configure the hostname, passwords, and banner
````
Router(config)# hostname RTA
RTA(config)# enable secret Ciscoenpa55
RTA(config)# service password-encryption
RTA(config)# banner motd #Unauthorized access is prohibited!#
````

Passwords are case-sensitive. Type ``Ciscoenpa55`` exactly as shown.




##### Configure the console password
````
RTA(config)# line console 0
RTA(config-line)# password Ciscolinepa55
RTA(config-line)# login
RTA(config-line)# exit
````

> The ``login`` command tells the console line to require the configured password.




##### Configure remote access through VTY lines
````
RTA(config)# line vty 0 4
RTA(config-line)# password Ciscolinepa55
RTA(config-line)# login
RTA(config-line)# transport input telnet
RTA(config-line)# exit
````

> This configures the router's VTY lines to accept Telnet connections using the line password.




##### Configure RTA G0/0

This interface connects **RTA** to **SW1** and the ``10.10.10.0/24`` network:

````
RTA(config)# interface gigabitEthernet 0/0
RTA(config-if)# description Link to SW1
RTA(config-if)# ip address 10.10.10.1 255.255.255.0
RTA(config-if)# no shutdown
RTA(config-if)# exit
````



##### Configure RTA G0/1

This interface connects **RTA** to **SW2** and the ``10.10.20.0/24`` network:
````
RTA(config)# interface gigabitEthernet 0/1
RTA(config-if)# description Link to SW2
RTA(config-if)# ip address 10.10.20.1 255.255.255.0
RTA(config-if)# no shutdown
RTA(config-if)# end
````





##### Verify RTA
````
RTA# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     10.10.10.1      YES manual up                    up 
GigabitEthernet0/1     10.10.20.1      YES manual up                    up 
Vlan1                  unassigned      YES unset  administratively down down
````



Next, check the interface descriptions:
````
RTA# show interfaces description
````



##### Save the router
````
RTA# copy running-config startup-config
````
Press ``Enter`` if prompted to confirm the destination filename.

**Output:**
````
Destination filename [startup-config]? 
Building configuration...
[OK]
````

----



#### Step 2: Configure switch SW1 and SW2.

##### Configure switch SW1

Click **SW1** → **CLI**, press **Enter**, and type:
````
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# enable secret Ciscoenpa55
SW1(config)# service password-encryption
SW1(config)# banner motd #Unauthorized access is prohibited!#
````



**Configure the console password:**
````
SW1(config)# line console 0
SW1(config-line)# password Ciscolinepa55
SW1(config-line)# login
SW1(config-line)# exit
````



**Configure the VTY lines:**
````
SW1(config)# line vty 0 15
SW1(config-line)# password Ciscolinepa55
SW1(config-line)# login
SW1(config-line)# transport input telnet
SW1(config-line)# exit
````


**Configure the VLAN 1 management interface:**

The switch needs a management IP address so that we can reach it over the network.
````
SW1(config)# interface vlan 1
SW1(config-if)# ip address 10.10.10.2 255.255.255.0
SW1(config-if)# no shutdown
SW1(config-if)# exit
````

**Configure the default gateway:**
````
SW1(config)# ip default-gateway 10.10.10.1
SW1(config)# end
````

Verify **SW1**:
````
SW1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
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
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  10.10.10.2      YES manual up                    up
````

Now in ``Vlan1                  10.10.10.2      YES manual up                    up`` is show `up`.



**Check the VLANs:**
````
SW1# show vlan brief
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
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````



**Save **SW1**:**
````
SW1# copy running-config startup-config
````
Press **Enter** to accept the default destination filename if requested.

**Output:**
````
Destination filename [startup-config]? 
Building configuration...
[OK]
````


----



##### Configure switch SW2

**SW2** is configured almost identically to **SW1**, but its management IP address and default gateway must belong to the second subnet.


**Configure its hostname and passwords:**


Click **SW2** → **CLI**, press **Enter**, and enter:
````
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW2
SW2(config)# enable secret Ciscoenpa55
SW2(config)# service password-encryption
SW2(config)# banner motd #Unauthorized access is prohibited!#
````


**Configure console and VTY passwords:**
````
SW2(config)# line console 0
SW2(config-line)# password Ciscolinepa55
SW2(config-line)# login
SW2(config-line)# exit
SW2(config)# line vty 0 15
SW2(config-line)# password Ciscolinepa55
SW2(config-line)# login
SW2(config-line)# transport input telnet
SW2(config-line)# exit
````


**Configure the management IP address:**
````
SW2(config)# interface vlan 1
SW2(config-if)# ip address 10.10.20.2 255.255.255.0
SW2(config-if)# no shutdown
SW2(config-if)# exit
````

Configure the default gateway:
````
SW2(config)# ip default-gateway 10.10.20.1
SW2(config)# end
````



**Verify and save SW2:**
````
SW2# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
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
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  10.10.20.2      YES manual up                    up
````

The output confirms that the switch management interface is working and both connected physical ports are up:
| Interface | IP Address | Status | Result |
|---|---|---|---|
| GigabitEthernet0/1 | Unassigned | `up/up` | Correct — connects to RTA |
| FastEthernet0/1 | Unassigned | `up/up` | Correct — connects to PC-2 |
| VLAN 1 | `10.10.20.2` | `up/up` | Correct |



````
SW2# copy running-config startup-config
````
Press **Enter** if asked to confirm the destination filename.
**Output:**
````
Destination filename [startup-config]? 
Building configuration...
[OK]
````

----



#### Step 3: Configure the hosts.

##### Configure PC-1
1. Click **PC-1**.
2. Open **Desktop**.
3. Select **IP Configuration**.
4. Select IPv4 configuration and enter these values.

| Setting | Value |
|---|---|
| IPv4 address | `10.10.10.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.10.10.1` |

<img width="870" height="668" alt="image" src="https://github.com/user-attachments/assets/3f555571-5527-4714-8457-59a4ebfb310a" />



##### Configure PC-2

1. Click **PC-2**.
2. Open **Desktop** → **IP Configuration**.
3. Enter these values.

| Setting | Value |
|---|---|
| IPv4 address | `10.10.20.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.10.20.1` |

<img width="875" height="672" alt="image" src="https://github.com/user-attachments/assets/3a24e94d-4632-46c5-9434-c455187d1799" />



##### Verify connectivity

Ping **RTA** from **PC-1**:

Click **PC-1** → **Desktop** →** Command Prompt**:

````
ping 10.10.10.1
ping 10.10.10.2
ping 10.10.20.10
ping 10.10.20.2
````

<img width="876" height="817" alt="image" src="https://github.com/user-attachments/assets/a16644b1-1933-4341-8987-04d17bfb5bfb" />


Now it success.



Test from **PC-2**:

Open **PC-2** → **Desktop** → **Command Prompt** and test these addresses:
````
ping 10.10.20.1
ping 10.10.20.2
ping 10.10.10.10
ping 10.10.10.2
````
<img width="828" height="1028" alt="image" src="https://github.com/user-attachments/assets/c329b7ea-73c6-4f4e-b8b4-cd8f3a4e25cf" />


Now we completed all.

-----


#### Score:

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/c2137a75-9791-49ab-ba04-45fb0036ae49" />


Now we got full score.


------


