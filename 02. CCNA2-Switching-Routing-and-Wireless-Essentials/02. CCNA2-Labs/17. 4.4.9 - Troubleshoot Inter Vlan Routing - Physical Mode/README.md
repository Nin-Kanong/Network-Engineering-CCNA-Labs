<h1 align="center"> 4.4.9 - Troubleshoot Inter Vlan Routing - Physical Mode </h1>



### Lab Guide


[4.4.9 Packet Tracer - Troubleshoot Inter-VLAN Routing - Physical Mode.docx](https://github.com/user-attachments/files/34880944/4.4.9.Packet.Tracer.-.Troubleshoot.Inter-VLAN.Routing.-.Physical.Mode.docx)



---



### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/0/1.3 | 10.3.0.1 | 255.255.255.0 | N/A |
| **R1** | G0/0/1.4 | 10.4.0.1 | 255.255.255.0 | N/A |
| **R1** | G0/0/1.13 | 10.13.0.1 | 255.255.255.0 | N/A |
| **S1** | VLAN 3 | 10.3.0.11 | 255.255.255.0 | 10.3.0.1 |
| **S2** | VLAN 3 | 10.3.0.12 | 255.255.255.0 | 10.3.0.1 |
| **PC-A** | NIC | 10.4.0.50 | 255.255.255.0 | 10.4.0.1 |
| **PC-B** | NIC | 10.13.0.50 | 255.255.255.0 | 10.13.0.1 |


### VLAN Table

| VLAN | Name | Interface Assigned |
| :--- | :--- | :--- |
| **3** | Management | S1: VLAN 3<br>S2: VLAN 3 |
| **4** | Operations | S1: F0/6 |
| **7** | ParkingLot | S1: F0/2-4, F0/7-24, G0/1-2<br>S2: F0/2-17, F0/19-24, G0/1-2 |
| **8** | Native | N/A |
| **13** | Maintenance | S2: F0/18 |


---



### Objectives

- **Part 1: Evaluate Network Operation**

- **Part 2: Gather Information, Create an Action Plan, and Implement Corrections**



---


## Lab Walkthrough


### Topology:

<img width="846" height="245" alt="image" src="https://github.com/user-attachments/assets/e284e3b5-8c46-406b-ab34-b794ab9ce564" />


---


#### The five problems we need to fix

| No. | Device | Incorrect configuration | Solution |
| :--- | :--- | :--- | :--- |
| **1** | R1 | VLAN 4 is incorrectly configured as native | Make VLAN 8 native |
| **2** | S1 | F0/5 is an access port | Configure F0/5 as a trunk |
| **3** | S1 | F0/1 has incorrect trunk settings | Native VLAN 8 and correct allowed VLANs |
| **4** | S1 | VLAN 13 does not exist | Create VLAN 13 |
| **5** | S2 | F0/1 has missing allowed VLANs | Allow VLANs 3, 4, 8, 13 |


----



### Part 1: Evaluate Network Operation

Open your activity and locate the laptop, then select the light-blue **Console** cable from Connections, Connect the laptop's ``RS-232`` port to R1's Console port:

<img width="1521" height="900" alt="image" src="https://github.com/user-attachments/assets/1ba1caa2-eecf-48cd-9a54-a96d372113db" />


<img width="1452" height="857" alt="image" src="https://github.com/user-attachments/assets/bc1b8aa2-8bae-4d0d-a295-a8f7f12d3a48" />


<img width="1497" height="862" alt="image" src="https://github.com/user-attachments/assets/0115b8d1-e374-4c01-a2a0-172a77ef2e1e" />


<img width="1515" height="866" alt="image" src="https://github.com/user-attachments/assets/7a96c7a7-0857-4865-a6f6-8b7a1d69271a" />



Then click **Desktop**, go to **Desktop** -> **Terminal**:

<img width="1521" height="862" alt="image" src="https://github.com/user-attachments/assets/c7f560d4-32a4-43a8-ba1a-6ee82104dae8" />



<img width="870" height="517" alt="image" src="https://github.com/user-attachments/assets/c9f57fb6-9425-48cc-b521-e277f805da1b" />


Then press **Enter**, and enter password:
````
cisco
````
<img width="873" height="816" alt="image" src="https://github.com/user-attachments/assets/729eb906-69b6-439d-8ec9-5dd523bd7bef" />



Then:
````
R1> enable
````
And enter password is:
````
class
````
<img width="432" height="97" alt="image" src="https://github.com/user-attachments/assets/ecba8b06-bb26-4a52-8867-04c9533fb595" />




----





### Part 2: Gather Information, Create an Action Plan, and Implement Corrections

#### Gather information and identify the problems

##### Investigate Router R1



Then verify:
````
R1> enable
Password: class
````
````
R1# show ip interface brief
R1# show running-config
R1# show ip route
````

Then we can we all abput this, like:
````
interface GigabitEthernet0/0/1.4
 encapsulation dot1Q 4 native
 ip address 10.4.0.1 255.255.255.0
````


``Problem 1``: Wrong native VLAN: VLAN 4 is incorrectly configured as native.



---


##### Investigate Switch S1


First in this `Right-Click` on **S1**:

<img width="1517" height="862" alt="image" src="https://github.com/user-attachments/assets/424e41ff-ac42-4586-b879-e5427c1e286a" />


<img width="1495" height="865" alt="image" src="https://github.com/user-attachments/assets/7bce59ba-9546-4cb7-8d8c-ca692d9385f8" />


<img width="1487" height="852" alt="image" src="https://github.com/user-attachments/assets/f6daed0c-6753-4e64-be95-e6b964c962a7" />


In this just click on it and move it to connsole:

<img width="1495" height="832" alt="image" src="https://github.com/user-attachments/assets/88852f7c-90bd-4766-9976-ab43b4f6e8d0" />


Now it was move to this:

<img width="1492" height="850" alt="image" src="https://github.com/user-attachments/assets/708c6f2c-9bae-4afa-87aa-e7467d16ae97" />



Then click on **PC-A**:

<img width="1501" height="856" alt="image" src="https://github.com/user-attachments/assets/6fffc752-9108-4b42-af17-c66e91e97bf1" />



Then to to **Desktop** -> **Terminal**:

<img width="877" height="437" alt="image" src="https://github.com/user-attachments/assets/1e35fcfc-0b2f-439b-aeab-a54255175a77" />



Then press **Enter**./

And in this password is:
````
cisco
````
<img width="870" height="827" alt="image" src="https://github.com/user-attachments/assets/46adbac0-b976-4458-921b-be9e9c3db8bb" />



Then verify:
````
S1> enable
Password: class
````
````
S1# show running-config
S1# show vlan brief
S1# show interfaces trunk
S1# show ip interface brief
````


Problem ion this is **F0/5 uses access mode**:

Incorrect:
```
interface FastEthernet0/5
 switchport mode access
 switchport access vlan 3
````
> ``F0/5`` is connected to Router R1. It needs to be a trunk because multiple VLANs must travel through this connection.



----


#### Implement Corrections One at a Time

In this on **R1**:

<img width="1496" height="832" alt="image" src="https://github.com/user-attachments/assets/a04b4582-98bd-4ab3-9692-06deac18ce6a" />


<img width="1417" height="712" alt="image" src="https://github.com/user-attachments/assets/a72df031-bce0-45fb-b537-b870d774a70f" />


<img width="1510" height="847" alt="image" src="https://github.com/user-attachments/assets/d15bd985-c02c-43eb-ba4d-0680a6002d46" />


Then click on **PC-A**:

<img width="1520" height="862" alt="image" src="https://github.com/user-attachments/assets/fb4a4f45-55b7-4de8-8e19-ee675f2d87f2" />


Go to **Desktop** -> **Terminal** -> click **Ok**, then **Enter** and password is:
````
cisco
````


Then:
````
R1> enable
Password: class
````

````
R1# configure terminal
````


##### Correct VLAN 4

````
R1(config)# interface g0/0/1.4
R1(config-subif)# encapsulation dot1Q 4
R1(config-subif)# exit
````




##### Set VLAN 8 as native.
````
R1(config)# interface g0/0/1.8
R1(config-subif)# encapsulation dot1Q 8 native
R1(config-subif)# exit
````


Then Exit configuration mode:
````
R1(config)# end
````


Then verify:
````
R1# show running-config
````

Then find:
````
interface GigabitEthernet0/0/1.4
 encapsulation dot1Q 4
 ip address 10.4.0.1 255.255.255.0

interface GigabitEthernet0/0/1.8
 encapsulation dot1Q 8 native
````


---


#### Connection S1 F0/5


In this move the labtop console cable to **S1**, then open **Terminal**:

<img width="1497" height="847" alt="image" src="https://github.com/user-attachments/assets/7480e985-b910-4be9-b629-ae667b438387" />



<img width="1497" height="767" alt="image" src="https://github.com/user-attachments/assets/bf0c17c0-7f88-4ccc-beb8-bf42f0980610" />


<img width="1502" height="830" alt="image" src="https://github.com/user-attachments/assets/4944ccb5-4939-40ad-b929-19b4d38398c8" />



Then click on **PC-A**:


<img width="1512" height="865" alt="image" src="https://github.com/user-attachments/assets/3b93f4ba-b7b5-43cf-9ef5-646974cad825" />



Then go to **Desktop** -> **Terminal**, then click **Ok**, then enter password:
````
cisco
````



Then:
````
S1> enable
Password: class
````

````
S1# configure terminal
````

Then reset the incorrect interface:
````
S1(config)# default interface f0/5
````



---


#### Configure F0/5 as a static trunk


````
S1# configure terminal
S1(config)# interface f0/5
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 8
S1(config-if)# switchport trunk allowed vlan 3,4,8,13
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# end
S1#
````



Then verify:
````
S1# show interfaces f0/5 switchport
S1# show interfaces trunk
````


---



#### Fix S1 F0/1

``Device S1`` Switch-to-switch trunk correction.

Enter configuration mode:

````
S1# configure terminal
S1(config)#
````

Correct ``F0/1``:
````
S1(config)# interface f0/1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 8
S1(config-if)# switchport trunk allowed vlan 3,4,8,13
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# end
S1#
````


Then verify it:
````
S1# show interface trunk
````
**Output:**

````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      8
Fa0/5       on           802.1q         trunking      8

Port        Vlans allowed on trunk
Fa0/1       3-4,8,13
Fa0/5       3-4,8,13

Port        Vlans allowed and active in management domain
Fa0/1       3,4,8
Fa0/5       3,4,8

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       3,4,8
Fa0/5       3,4,8
````


----



#### Create VLAN 13 on S1


``Device S1`` Missing VLAN correction.


```text
S1#`configure terminal
S1(config)#
```

Enter:
````
S1(config)# vlan 13
S1(config-vlan)# name Maintenance
S1(config-vlan)# exit
S1(config)# end
S1#
````



Then verify it:
````
S1# show vlan brief
````
**Output:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    
3    Management                       active    
4    Operations                       active    Fa0/6
7    ParkingLot                       active    Fa0/2, Fa0/3, Fa0/4, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
8    Native                           active    
13   Maintenance                      active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````



---


#### Fix S2 F0/1

`Device S2` Final trunk correction.

Move the console cable to S2 and open a new Terminal session.

First in this `Right-Click` on **S2**: select **Inspect Rear**:

<img width="1522" height="757" alt="image" src="https://github.com/user-attachments/assets/65673f6b-6d17-4f37-a029-50611cd67896" />


Then `right-Click` on **S1** then select **Inspect Rear**:


<img width="1517" height="872" alt="image" src="https://github.com/user-attachments/assets/63afdd65-eec4-4d84-8562-5d0aa21e295c" />



The move from console **S1** to console **S2**:

<img width="1525" height="851" alt="image" src="https://github.com/user-attachments/assets/ca1b079e-77d5-4d12-8ae6-c4ec451431af" />


<img width="1518" height="861" alt="image" src="https://github.com/user-attachments/assets/d7d911c0-bc2e-43cf-b0d7-e31adb0b9dd5" />


Now we was successful.




Then click on **PC-A** -> **Desktop** -> **Terminal** -> Click **Ok**. then press **Enter**, and enter password:
````
cisco
````


<img width="1171" height="948" alt="image" src="https://github.com/user-attachments/assets/f442f54a-de95-4a0e-b158-68a8702defc6" />



After enter this:
````
S2> enable
Password: class
````

````
S2# configure terminal
S2(config)#
````



Then configure the correct trunk:
````
S2(config)# interface f0/1
S2(config-if)# switchport mode trunk
S2(config-if)# switchport trunk native vlan 8
S2(config-if)# switchport trunk allowed vlan 3,4,8,13
S2(config-if)# no shutdown
S2(config-if)# exit
S2(config)# end
````



Then verify it:


````
S2# show interfaces trunk
````

**Output:**
````
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      8

Port        Vlans allowed on trunk
Fa0/1       3-4,8,13

Port        Vlans allowed and active in management domain
Fa0/1       3,4,8,13

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       3,4,8,13
````


````
S2# show vlan brief
````
**OLutput:**
````
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    
3    Management                       active    
4    Operations                       active    
7    ParkingLot                       active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
8    Native                           active    
13   Maintenance                      active    Fa0/18
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active
````


Now we are corrected all.


----


#### Scoreboard


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/b625a955-cfd9-4399-90a7-61440b77a15d" />



Now we got full score.

-----
