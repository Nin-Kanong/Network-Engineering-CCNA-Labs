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





































