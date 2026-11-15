<h1 align="center"> LAB: 4.4.8 - Troubleshoot Inter VLAN Routing</h1>


---


### Lab Guide

[4.4.8 Packet Tracer - Troubleshoot Inter-VLAN Routing.docx](https://github.com/user-attachments/files/34878987/4.4.8.Packet.Tracer.-.Troubleshoot.Inter-VLAN.Routing.docx)


---


### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway | VLAN |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/1.10 | 172.17.10.1 | 255.255.255.0 | N/A | VLAN 10 |
| **R1** | G0/1.30 | 172.17.30.1 | 255.255.255.0 | N/A | VLAN 30 |
| **PC1** | NIC | 172.17.10.10 | 255.255.255.0 | 172.17.10.1 | VLAN 10 |
| **PC3** | NIC | 172.17.30.10 | 255.255.255.0 | 172.17.30.1 | VLAN 30 |


---


### Objectives

- **Part 1: Locate Network Problems**

- **Part 2: Implement the Solution**

- **Part 3: Verify Network Connectivity**

----



## Lab WalkThrough 

<img width="1082" height="531" alt="image" src="https://github.com/user-attachments/assets/f951cfa8-7069-4e33-8caf-d5b5706a853d" />


---


### Part 1: Locate the Network Problems


#### addressing table

| Device | Interface | IP address | Gateway | VLAN |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/1.10 | 172.17.10.1/24 | N/A | 10 |
| **R1** | G0/1.30 | 172.17.30.1/24 | N/A | 30 |
| **PC1** | NIC | 172.17.10.10/24 | 172.17.10.1 | 10 |
| **PC3** | NIC | 172.17.30.10/24 | 172.17.30.1 | 30 |


#### Problems and Solutions

Here is the information formatted as a Markdown table:

| No. | Problem | Solution |
| :--- | :--- | :--- |
| **1** | R1 subinterface G0/1.10 is administratively down. | Enable it using `no shutdown`. |
| **2** | PC3 has the wrong default gateway. | Set it to `172.17.30.1`. |
| **3** | S1 interface G0/1 is an access port instead of a trunk. | Configure `switchport mode trunk`. |
| **4** | R1's VLAN tags for subinterfaces G0/1.10 and G0/1.30 are swapped. | Set `encapsulation dot1Q 10` and `encapsulation dot1Q 30` on the correct subinterfaces. |


#### Inspect the incorrect configurations

Click **R1** -> Select the **CLI** tab -> Press **Enter**:

<img width="862" height="801" alt="image" src="https://github.com/user-attachments/assets/5488e8a2-b01b-4a02-9431-823863254e48" />


Enter these commands:
````
R1> enable
R1# show ip interface brief
R1# show interfaces g0/1.10
R1# show interfaces g0/1.30
R1# show running-config
````

Then Look for ``administratively down`` on ``G0/1.10``, and check whether ``encapsulation dot1Q`` uses the wrong VLAN numbers.


Then click on **S1**, go to **CLI** then **Enter**:

<img width="885" height="798" alt="image" src="https://github.com/user-attachments/assets/8000d628-9e7a-4c2e-8745-3d3d1cfaf500" />


````
S1> enable
S1# show interfaces trunk
S1# show vlan brief
S1# show running-config
````

> If ``G0/1`` is an access port, it will not appear as an operational trunk in ``show interfaces trunk``.


----


  
### Part 2: Implement the Solutions


#### Enable R1 subinterface G0/1.10

In this the `Problem 1` is **G0/1.10 is administratively down**.


On **R1**, open the **CLI** and type:
````
R1> enable
R1# configure terminal
R1(config)# interface gigabitEthernet0/1.10
R1(config-subif)# no shutdown
R1(config-subif)# exit
````


Then verify that the parent physical interface is enabled:
````
R1(config)# interface gigabitEthernet0/1
R1(config-if)# no shutdown
R1(config-if)# exit
````

In this this addresses the disabled interface condition. However, connectivity may still fail until the other configuration errors are repaired.


---


#### Correct PC3's Default Gateway

In this the `Problem 2` **PC3 has an incorrect gateway**.


Click **PC3** -> Open the **Desktop** tab -> Click **IP Configuration** -> Select **Static**, if needed. Set the following values:

| Setting | Value |
| :--- | :--- |
| **IPv4 Address** | ``172.17.30.10`` |
| **Subnet Mask** | ``255.255.255.0`` |
| **Default Gateway** | ``172.17.30.1`` |


So in this **PC3** belongs to **VLAN 30**, so its gateway must be the router's **VLAN 30** address, not the **VLAN 10** address.

<img width="875" height="686" alt="image" src="https://github.com/user-attachments/assets/95488f32-9116-4cfe-8b92-e5e74870831e" />


---


#### Configure S1 G0/1 as a trunk port

In this this `Problem 3` The switch uplink is configured as an access port.

Click **S1** -> **CLI**, then press **Enter** and type:

````
S1> enable
S1# configure terminal
````



##### Configure the trunk

````
S1(config)# interface gigabitEthernet0/1
S1(config-if)# switchport mode trunk
S1(config-if)# no shutdown
S1(config-if)# exit
````


Thn verify it:
````
S1(config)# end
S1# show interface trunk
````

**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,30

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,30
````
---


#### Check access port VLAN membership

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
10   Faculty/Staff                    active    Fa0/11
30   Guest(Default)                   active    Fa0/6
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

---



#### Correct the VLAN assignments on R1

On `Problem 4` The router subinterface VLAN tags are reversed.

In this the required settings are:

| Router subinterface | Correct VLAN tag | IP address |
| :--- | :--- | :--- |
| **G0/1.10** | dot1Q 10 | 172.17.10.1 |
| **G0/1.30** | dot1Q 30 | 172.17.30.1 |


Then open **R1** -> **CLI**:

````
R1> enable
R1# configure terminal
````



##### Remove the swapped encapsulation settings

In this we will remove the existing VLAN encapsulation on both subinterfaces first to avoid duplicate VLAN assignments.

````
R1(config)# interface gigabitEthernet0/1.10
R1(config-subif)# no encapsulation dot1Q
R1(config-subif)# exit
````

Then:
````
R1(config)# interface gigabitEthernet0/1.30
R1(config-subif)# no encapsulation dot1Q
R1(config-subif)# exit
````



##### Configure subinterface G0/1.10
````
R1(config)# interface gigabitEthernet0/1.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 172.17.10.1 255.255.255.0
R1(config-subif)# no shutdown
R1(config-subif)# exit
````


> **Note**: ``dot1Q`` stands for **IEEE 802.1Q**, which is the standard protocol for VLAN tagging on Ethernet networks.




##### Configure subinterface G0/1.30
````
R1(config)# interface gigabitEthernet0/1.30
R1(config-subif)# encapsulation dot1Q 30
R1(config-subif)# ip address 172.17.30.1 255.255.255.0
R1(config-subif)# no shutdown
R1(config-subif)# exit
````

##### Enable the physical interface and save

````
R1(config)# interface gigabitEthernet0/1
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# end
R1# copy running-config startup-config
````



------



### Part 3: Verify Network Connectivity

In this after repairing all four problems, we must verify that the devices can communicate.

#### Verify router interfaces

Click on **R1** -> **CLI**, then enter:
````
R1> enable
R1# show ip interface brief
````
**Output:**
````
GigabitEthernet0/0     unassigned      YES unset  administratively down down 
GigabitEthernet0/1     unassigned      YES unset  up                    up 
GigabitEthernet0/1.10  172.17.10.1     YES manual up                    up 
GigabitEthernet0/1.30  172.17.30.1     YES manual up                    up 
Vlan1                  unassigned      YES unset  administratively down down
````

Now we see it `up`.


---


#### Verify switch trunking

On **S1**:

````
S1> show interfaces trunk
````
**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Gig0/1      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Gig0/1      1-1005

Port        Vlans allowed and active in management domain
Gig0/1      1,10,30

Port        Vlans in spanning tree forwarding state and not pruned
Gig0/1      1,10,30
````


````
S1> show vlan brief
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
10   Faculty/Staff                    active    Fa0/11
30   Guest(Default)                   active    Fa0/6
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


---


#### Ping R1 from PC1

Click **PC1** -> Open **Desktop** -> **Command Prompt**, Enter:
````cmd
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

----




#### Ping R1 from PC3

On **PC3** → **Desktop** → **Command Prompt**:

````cmd
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


-----



### Scoreboard 


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/636606d6-92cf-4a47-a756-a77542f7e0bc" />



Now we got full score.

-----
