<h1 align="center"> LAB: 4.5.1 - Inter Vlan Routing Challenge </h1>



---


### Lab Guide


[4.5.1 Packet Tracer - Inter-VLAN Routing Challenge.docx](https://github.com/user-attachments/files/34923361/4.5.1.Packet.Tracer.-.Inter-VLAN.Routing.Challenge.docx)



---



### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/0 | 172.17.25.2 | 255.255.255.252 | N/A |
| **R1** | G0/1.10 | 172.17.10.1 | 255.255.255.0 | N/A |
| **R1** | G0/1.20 | 172.17.20.1 | 255.255.255.0 | N/A |
| **R1** | G0/1.30 | 172.17.30.1 | 255.255.255.0 | N/A |
| **R1** | G0/1.88 | 172.17.88.1 | 255.255.255.0 | N/A |
| **R1** | G0/1.99 | 172.17.99.1 | 255.255.255.0 | N/A |
| **S1** | VLAN 99 | 172.17.99.10 | 255.255.255.0 | 172.17.99.1 |
| **PC1** | NIC | 172.17.10.21 | 255.255.255.0 | 172.17.10.1 |
| **PC2** | NIC | 172.17.20.22 | 255.255.255.0 | 172.17.20.1 |
| **PC3** | NIC | 172.17.30.23 | 255.255.255.0 | 172.17.30.1 |
| **Server** | NIC | 172.17.50.254 | 255.255.255.0 | 172.17.50.1 |

### VLAN and Port Assignments Table

| VLAN | Name | Interface |
| :--- | :--- | :--- |
| **10** | Faculty/Staff | F0/11-17 |
| **20** | Students | F0/18-24 |
| **30** | Guest(Default) | F0/6-10 |
| **88** | Native | G0/1 |
| **99** | Management | VLAN 99 |

---


## Lab Walkthrough


<img width="1152" height="597" alt="image" src="https://github.com/user-attachments/assets/0777faf8-4633-4267-a06b-8f440f788f36" />



---

### Configure Router R1 IP addressing
Assign IP addressing to **R1** and **S1** based on the Addressing Table.


First click on **R1** -> **CLI**, then press **Enter**:

<img width="991" height="823" alt="image" src="https://github.com/user-attachments/assets/ac56a124-e2af-47b9-b3f9-022401b95d74" />



Then enter:
````
R1> enable
R1# configure terminal
R1(config)# hostname R1
R1(config)#
````


#### Configure physical interface G0/0

This interface connects **R1** to the network containing the server.

````
R1(config)# interface gigabitEthernet0/0
R1(config-if)# ip address 172.17.25.2 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)#
````


#### Enable interface G0/1

``G0/1`` connects to the switch and will carry all VLANs:
````
R1(config)# interface gigabitEthernet0/1
R1(config-if)# no ip address
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)#
````

> The physical ``G0/1`` interface does not need an IP address because the IP addresses will be configured on its subinterfaces.


----



### Configure Switch S1

Click **S1** -> **CLI**, then press **Enter**:

<img width="1000" height="920" alt="image" src="https://github.com/user-attachments/assets/f529b5de-27f0-42fd-a8f2-e16f5d2bd8a1" />


Then enter:
````
S1> enable
S1# configure terminal
S1(config)# hostname S1
S1(config)#
````


#### Create all five VLANs

Type:


**Create Vlan 10:**
````
S1(config)# vlan 10
S1(config-vlan)# name Faculty/Staff
S1(config-vlan)# exit
````


**Create Vlan 20:**
````
S1(config)# vlan 20
S1(config-vlan)# name Students
S1(config-vlan)# exit
````


**Create Vlan 30:**

````
S1(config)# vlan 30
S1(config-vlan)# name Guest(Default)
S1(config-vlan)# exit
````


**Create Vlan 88:**

````
S1(config)# vlan 88
S1(config-vlan)# name Native
S1(config-vlan)# exit
````


**Create Vlan 99:**
````
S1(config)# vlan 99
S1(config-vlan)# name Management
S1(config-vlan)# exit
S1(config)#
````



**Exit configuration mode:**
````
S1# end
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
88   Native                           active    
99   Management                       active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````

----



### Assign VLLANs to access ports

| VLAN | Name | S1 Ports |
|---|---|---|
| 10 | Faculty/Staff | Fa0/11–Fa0/17 |
| 20 | Students | Fa0/18–Fa0/24 |
| 30 | Guest(Default) | Fa0/6–Fa0/10 |



#### Configure VLAN 10 


On **S1**:
````
S1# configure terminal
S1(config)# interface range fastEthernet0/11 - 17
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 10
S1(config-if-range)# no shutdown
S1(config-if-range)# exit
S1(config)#
````



#### Configure VLAN 20
````
S1(config)# interface range fastEthernet0/18 - 24
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 20
S1(config-if-range)# no shutdown
S1(config-if-range)# exit
S1(config)#
````





#### Configure VLAN 30

````
S1(config)# interface range fastEthernet0/6 - 10
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 30
S1(config-if-range)# no shutdown
S1(config-if-range)# exit
S1(config)#
````



Thhen verify:
````
S1(config)# end
````
````
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Gig0/1, Gig0/2
10   Faculty/Staff                    active    Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17
20   Students                         active    Fa0/18, Fa0/19, Fa0/20, Fa0/21
                                                Fa0/22, Fa0/23, Fa0/24
30   Guest(Default)                   active    Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10
88   Native                           active    
99   Management                       active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


----


### Configure the static trunk on S1

In this we will configure ``G0/1`` of S1 as a static trunk and assign the native VLAN.


Then enter:
````
S1# configure terminal
S1(config)#
````



#### Configiure G0/1
```
S1(config)# interface gigabitEthernet0/1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 88
S1(config-if)# switchport trunk allowed vlan 10,20,30,88,99
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# end
S1#
```


Then verify:
````
S1# show interfaces trunk
````

In this we see nothing, but no wrroy it corrected.

---


### Disable all unused S1 ports


#### Configure unused ports

````
S1# configure terminal
S1(config)# interface range fastEthernet0/1 - 5
S1(config-if-range)# shutdown
S1(config-if-range)# exit
````

````
S1(config)# interface gigabitEthernet0/2
S1(config-if)# shutdown
S1(config-if)# exit
S1(config)# end
S1#
````


Then verify:
````
S1# show interfaces status
````
**Output:**
````
Port      Name               Status       Vlan       Duplex  Speed Type
Fa0/1                        disabled 1          auto    auto  10/100BaseTX
Fa0/2                        disabled 1          auto    auto  10/100BaseTX
Fa0/3                        disabled 1          auto    auto  10/100BaseTX
Fa0/4                        disabled 1          auto    auto  10/100BaseTX
Fa0/5                        disabled 1          auto    auto  10/100BaseTX
Fa0/6                        connected    30         a-full  a-100 10/100BaseTX
Fa0/7                        notconnect   30         auto    auto  10/100BaseTX
Fa0/8                        notconnect   30         auto    auto  10/100BaseTX
Fa0/9                        notconnect   30         auto    auto  10/100BaseTX
Fa0/10                       notconnect   30         auto    auto  10/100BaseTX
Fa0/11                       connected    10         a-full  a-100 10/100BaseTX
Fa0/12                       notconnect   10         auto    auto  10/100BaseTX
Fa0/13                       notconnect   10         auto    auto  10/100BaseTX
Fa0/14                       notconnect   10         auto    auto  10/100BaseTX
Fa0/15                       notconnect   10         auto    auto  10/100BaseTX
Fa0/16                       notconnect   10         auto    auto  10/100BaseTX
Fa0/17                       notconnect   10         auto    auto  10/100BaseTX
Fa0/18                       connected    20         a-full  a-100 10/100BaseTX
Fa0/19                       notconnect   20         auto    auto  10/100BaseTX
Fa0/20                       notconnect   20         auto    auto  10/100BaseTX
Fa0/21                       notconnect   20         auto    auto  10/100BaseTX
Fa0/22                       notconnect   20         auto    auto  10/100BaseTX
Fa0/23                       notconnect   20         auto    auto  10/100BaseTX
Fa0/24                       notconnect   20         auto    auto  10/100BaseTX
Gig0/1                       notconnect   trunk      auto    auto  10/100/1000BaseTX
Gig0/2                       disabled 1          auto    auto  10/100/1000BaseTX
````



In this some port may show notconnect if there is no cable attached; that does not mean the port is configured incorrectly. The key requirement for unused ports is that they are administratively shut down.


---


### Configure S1 Management IP and Default Gateway

| Setting | Value |
|---|---|
| Management VLAN | 99 |
| IP address | 172.17.99.10 |
| Subnet mask | 255.255.255.0 |
| Default gateway | 172.17.99.1 |



#### Configure S1 default gateway

On **S1**:

```
S1> enable
S1# configure terminal
S1(config)# interface vlan 99
S1(config-if)# ip address 172.17.99.10 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)#
```



#### Configure S1's default gateway

```
S1(config)# ip default-gateway 172.17.99.1
S1(config)# end
S1#
```


In this we use `ip default-gateway` **S1** is a **Layer 2** switch. It needs a gateway to communicate with devices in other IP networks through **R1**.



#### Verify S1 IP configuration
```
S1# show ip interface brief
```
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
Vlan99                 172.17.99.10    YES manual up                    down
````


---


### Configure Inter VLAN Routing on R1

In this we will configure five router subinterfaces so that devices in different VLANs can communicate.


#### Configure VLAN 10 subinterface

On **R1**:

````
R1> enable
R1# configure terminal
R1(config)# interface gigabitEthernet0/1.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 172.17.10.1 255.255.255.0
R1(config-subif)# exit
R1(config)#
````

> ``encapsulation dot1Q 10``: Associates traffic tagged with VLAN 10.


---


#### Configure VLAN 20 subinterface

```
R1(config)# interface gigabitEthernet0/1.20
R1(config-subif)# encapsulation dot1Q 20
R1(config-subif)# ip address 172.17.20.1 255.255.255.0
R1(config-subif)# exit
R1(config)#
```


#### Configure VLAN 30 subinterface
````
R1(config)# interface gigabitEthernet0/1.30
R1(config-subif)# encapsulation dot1Q 30
R1(config-subif)# ip address 172.17.30.1 255.255.255.0
R1(config-subif)# exit
R1(config)#
````



#### Configure Native VLAN 88
````
R1(config)# interface gigabitEthernet0/1.88
R1(config-subif)# encapsulation dot1Q 88 native
R1(config-subif)# ip address 172.17.88.1 255.255.255.0
R1(config-subif)# exit
````


#### Configure Management VLAN 99

````
R1(config)# interface gigabitEthernet0/1.99
R1(config-subif)# encapsulation dot1Q 99
R1(config-subif)# ip address 172.17.99.1 255.255.255.0
R1(config-subif)# exit
````



Then after configure all then verify:
````
R1(config)# end
R1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     172.17.25.2     YES manual up                    up 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
GigabitEthernet0/1.10  172.17.10.1     YES manual administratively down down 
GigabitEthernet0/1.20  172.17.20.1     YES manual administratively down down 
GigabitEthernet0/1.30  172.17.30.1     YES manual administratively down down 
GigabitEthernet0/1.88  172.17.88.1     YES manual administratively down down 
GigabitEthernet0/1.99  172.17.99.1     YES manual administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
````


In this if we see `Administratively` ``down`` on ``G0/1```, then enter:
````
R1# configure terminal
R1(config)# interface gigabitEthernet0/1
R1(config-if)# no shutdown
R1(config-if)# end
R1#
````

Then verify again:
````
R1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     172.17.25.2     YES manual up                    up 
GigabitEthernet0/1     unassigned      YES unset  up                    up 
GigabitEthernet0/1.10  172.17.10.1     YES manual up                    up 
GigabitEthernet0/1.20  172.17.20.1     YES manual up                    up 
GigabitEthernet0/1.30  172.17.30.1     YES manual up                    up 
GigabitEthernet0/1.88  172.17.88.1     YES manual up                    up 
GigabitEthernet0/1.99  172.17.99.1     YES manual up                    up 
Vlan1                  unassigned      YES unset  administratively down down
````



#### Verify connected routed

````
R1# show ip route
````
**Output:**
````
Gateway of last resort is 0.0.0.0 to network 0.0.0.0

     172.17.0.0/16 is variably subnetted, 12 subnets, 3 masks
C       172.17.10.0/24 is directly connected, GigabitEthernet0/1.10
L       172.17.10.1/32 is directly connected, GigabitEthernet0/1.10
C       172.17.20.0/24 is directly connected, GigabitEthernet0/1.20
L       172.17.20.1/32 is directly connected, GigabitEthernet0/1.20
C       172.17.25.0/30 is directly connected, GigabitEthernet0/0
L       172.17.25.2/32 is directly connected, GigabitEthernet0/0
C       172.17.30.0/24 is directly connected, GigabitEthernet0/1.30
L       172.17.30.1/32 is directly connected, GigabitEthernet0/1.30
C       172.17.88.0/24 is directly connected, GigabitEthernet0/1.88
L       172.17.88.1/32 is directly connected, GigabitEthernet0/1.88
C       172.17.99.0/24 is directly connected, GigabitEthernet0/1.99
L       172.17.99.1/32 is directly connected, GigabitEthernet0/1.99
S*   0.0.0.0/0 is directly connected, GigabitEthernet0/0
````



Then back our package it work all:


<img width="1140" height="602" alt="image" src="https://github.com/user-attachments/assets/d82d16f9-8931-4fdf-be96-43eb89b1329a" />


The **PCs** may already have their IP addresses configured. Verify them rather than changing correct settings.

----



### Verify Complete Network Connectivity


#### Test R1 to S1
On **R1**:
````cmd
ping 172.17.99.10
````



#### Test R1 to all PCs and the server
````cmd
ping 172.17.10.21
ping 172.17.20.22
ping 172.17.30.23
ping 172.17.50.254
````



#### Test from S1
On **S1**:
````cmd
ping 172.17.99.1
ping 172.17.10.21
ping 172.17.20.22
ping 172.17.30.23
ping 172.17.50.254
````


#### Test from S1
On **S1**:
````cmd
ping 172.17.99.1
ping 172.17.10.21
ping 172.17.20.22
ping 172.17.30.23
ping 172.17.50.254
````


#### Test from PC2:
````cmd
ping 172.17.20.1
ping 172.17.10.21
ping 172.17.30.23
ping 172.17.99.10
ping 172.17.50.254
````



#### Test from PC3

````cmd
ping 172.17.30.1
ping 172.17.10.21
ping 172.17.20.22
ping 172.17.99.10
ping 172.17.50.254
````


Now we got successful all.


----



#### Scoreboard 


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/539460e9-13f7-46d4-b0bb-691998f9d78f" />



Now we got successful.

----
