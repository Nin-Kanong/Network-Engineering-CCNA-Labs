<h1 align="center"> LAB: 4.3.8 - Cinfigure Layer3 Switching And Inter VLAN Routing </h1>


---


## Lab Guide




---


## Addressing Table


| Device | Interface | IP Address / Prefix |
| :--- | :--- | :--- |
| **MLS** | VLAN 10 | `192.168.10.254 /24` |
| **MLS** | VLAN 10 | `2001:db8:acad:10::1/64` |
| **MLS** | VLAN 20 | `192.168.20.254 /24` |
| **MLS** | VLAN 20 | `2001:db8:acad:20::1/64` |
| **MLS** | VLAN 30 | `192.168.30.254/24` |
| **MLS** | VLAN 30 | `2001:db8:acad:30::1/64` |
| **MLS** | VLAN 99 | `192.168.99.254/24` |
| **MLS** | G0/2 | `209.165.200.225` |
| **MLS** | G0/2 | `2001:db8:acad:a::1/64` |
| **PC0** | NIC | `192.168.10.1` |
| **PC1** | NIC | `192.168.20.1` |
| **PC2** | NIC | `192.168.30.1` |
| **PC3** | NIC | `192.168.10.2/24` |
| **PC3** | NIC | `2001:db8:acad:10::2/64` |
| **PC4** | NIC | `192.168.20.2/24` |
| **PC4** | NIC | `2001:db8:acad:20::2/64` |
| **PC5** | NIC | `192.168.30.2` |
| **PC5** | NIC | `2001:db8:acad:30::2/64` |
| **S1** | VLAN 99 | `192.168.99.1` |
| **S2** | VLAN 99 | `192.168.99.2` |
| **S3** | VLAN 99 | `192.168.99.3` |


---



## Lab Walkkthrough


<img width="1107" height="618" alt="image" src="https://github.com/user-attachments/assets/baf8b7f9-531f-44d2-95bd-fa5e1dd106a8" />




---



### Part 1: Configure Layer 3 Switching

In this part, we will configure MLS ``G0/2`` as a routed port and test connectivity to the Cloud.

Click on **MLS** -> **CLI**, press **Enter**.


**Enter privileged EXEC mode:**
````
MLS> enable
MLS# configure terminal
````


#### Configure G0/2 as a routed port:

A multilayer switch normally uses switchports for Layer 2 switching. The ``no switchport`` command converts ``G0/2`` into a Layer 3 routed interface.

````
MLS(config)# interface gigabitEthernet 0/2
MLS(config-if)# no switchport
MLS(config-if)# ip address 209.165.200.225 255.255.255.252
MLS(config-if)# no shutdown
MLS(config-if)# exit
MLS(config)# end
````


| Command | Purpose |
| :--- | :--- |
| `no switchport` | Converts the port into a Layer 3 routed interface |
| `ip address` | Assigns the IPv4 address |
| `no shutdown` | Enables the interface |

---


#### Verify the routed interface
````
MLS# show ip interface brief
````

<img width="657" height="455" alt="image" src="https://github.com/user-attachments/assets/5591ff31-4306-44b7-a956-951b8d3328be" />


Now it show `up`.


#### Test connectivity to cloud
On **MLS**, run:
````
ping 209.165.200.226
````

**Output:**
````
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 209.165.200.226, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms
````

> Now **MLS** can communicate with the Cloud through its directly connected network.

---



### Part 2: Configure Inter-VLAN Routing


#### Step 1: Add VLANs.
In this we will add **VLANs** on **MLS**.


Open **MLS** -> **CLI**, then enter:
````
MLS> enable
MLS# configure terminal
````


##### Create VLAN 10
````
MLS(config)# vlan 10
MLS(config-vlan)# name staff
MLS(config-vlan)# exit
````

##### Create VLAN 20
````
MLS(config)# vlan 20
MLS(config-vlan)# name Student
MLS(config-vlan)# exit
````

##### Create VLAN 30
````
MLS(config)# vlan 30
MLS(config-vlan)# name Faculty
MLS(config-vlan)# exit
````




















