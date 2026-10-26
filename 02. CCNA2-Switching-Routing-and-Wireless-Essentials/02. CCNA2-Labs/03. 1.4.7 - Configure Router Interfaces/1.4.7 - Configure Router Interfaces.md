<h1 align="center"> LAB: 1.4.7 - Configure Router Interface </h1>


---


### Lab Guide

[1.4.7 Packet Tracer - Configure Router Interfaces.docx](https://github.com/user-attachments/files/33981916/1.4.7.Packet.Tracer.-.Configure.Router.Interfaces.docx)


---

### Addressing Table
| Device | Interface | IP Address/Prefix      | Default Gateway |
| ------ | --------- | ---------------------- | --------------- |
| R1     | G0/0      | 172.16.20.1 /25        | N/A             |
| R1     | G0/1      | 172.16.20.129 /25      | N/A             |
| R1     | S0/0/0    | 209.165.200.225 /30    | N/A             |
| PC1    | NIC       | 172.16.20.10 /25       | 172.16.20.1     |
| PC2    | NIC       | 172.16.20.138 /25      | 172.16.20.129   |
| R2     | G0/0      | 2001:db8:c0de:12::1/64 | N/A             |
| R2     | G0/1      | 2001:db8:c0de:13::1/64 | N/A             |
| R2     | S0/0/1    | 2001:db8:c0de:11::1/64 | N/A             |
| R2     | S0/0/1    | fe80::2                | N/A             |
| PC3    | NIC       | 2001:db8:c0de:12::a/64 | fe80::2         |
| PC4    | NIC       | 2001:db8:c0de:13::a/64 | fe80::2         |

---

## Lab Walkthrough 

<img width="1227" height="473" alt="image" src="https://github.com/user-attachments/assets/49c3372c-64ef-46ac-a034-b99b8d37f207" />


### Part 1: Configure IPv4 addressing

#### Configure R1

Click router **R1** -> Select **CLI** -> Press **Enter** if prompted -> Enter the user EXEC password:
````
cisco
````
<img width="867" height="875" alt="image" src="https://github.com/user-attachments/assets/d67b34f9-ade3-41c1-af06-2dab0dd9548d" />


````
enable
````
Password: 
````
class
````
<img width="136" height="62" alt="image" src="https://github.com/user-attachments/assets/d292669b-e483-4722-a93c-c1cd21089f3f" />


````
Router# configure terminal
Router(config)# hostname R1
````

Configure the first LAN interface, **G0/0**:
````
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# ip address 172.16.20.1 255.255.255.128
R1(config-if)# no shutdown
R1(config-if)# exit
````

Configure the second LAN interface, **G0/1**:
````
R1(config)# interface gigabitEthernet 0/1
R1(config-if)# ip address 172.16.20.129 255.255.255.128
R1(config-if)# no shutdown
R1(config-if)# exit
````


Save the configuration:
````
R1(config)# end
R1# copy running-config startup-config
````
Press ``Enter`` if prompted for the destination filename.

---


#### Configure PC1
Click **PC1** -> Select **Desktop** → **IP Configuration** -> Select **Static** -> Enter the following settings:
| Setting         | Value             |
| --------------- | ----------------- |
| IPv4 Address    | `172.16.20.10`    |
| Subnet Mask     | `255.255.255.128` |
| Default Gateway | `172.16.20.1`     |


<img width="877" height="671" alt="image" src="https://github.com/user-attachments/assets/a4d2eb7e-85be-4904-9a95-6ff035d5647a" />


---


#### Configure PC1
Click **PC2** -> Select **Desktop** → **IP Configuration** -> Select **Static** -> Enter the following settings:

| Setting         | Value             |
| --------------- | ----------------- |
| IPv4 Address    | `172.16.20.138`   |
| Subnet Mask     | `255.255.255.128` |
| Default Gateway | `172.16.20.129`   |

<img width="873" height="668" alt="image" src="https://github.com/user-attachments/assets/6ada9de8-7d18-48b7-acba-a721495d0fd7" />


---


#### Verify IPv4 connectivity

On **PC1**, open **Desktop** → **Command Prompt** and run:
````
ping 172.16.20.1
ping 172.16.20.138
````
<img width="872" height="636" alt="image" src="https://github.com/user-attachments/assets/a2656091-ccb7-41e4-be0f-269f52875e20" />

Now it success.


On PC2, run:
````
ping 172.16.20.129
ping 172.16.20.10
````
<img width="875" height="645" alt="image" src="https://github.com/user-attachments/assets/c8d8df85-1787-4482-830f-c023fea82e92" />


---




### Part 2: Configure IPv6 addressing


#### Configure R2

Click on **R2** -> then go to **CLI**, then press `Enter`:

And Password is:
````
cisco
````

<img width="872" height="837" alt="image" src="https://github.com/user-attachments/assets/aee6213b-d4e4-4691-9109-0b24669e771d" />


````
R2>enable
Password: class
R2#
````

````
Router# configure terminal
Router(config)# hostname R2
````

> **Note**: In this it has ready have hostname, we can set hostname to others hostname.


- Enable IPv6 routing:
````
R2(config)# ipv6 unicast-routing
````

- Configure **G0/0** for **PC3**'s LAN:
````
R2(config)# interface gigabitEthernet 0/0
R2(config-if)# ipv6 address 2001:DB8:C0DE:12::1/64
R2(config-if)# no shutdown
R2(config-if)# exit
````

- Configure **G0/1** for **PC4**'s LAN:
````
R2(config)# interface gigabitEthernet 0/1
R2(config-if)# ipv6 address 2001:DB8:C0DE:13::1/64
R2(config-if)# no shutdown
R2(config-if)# exit
````

<img width="834" height="467" alt="image" src="https://github.com/user-attachments/assets/faf43939-15f4-458d-89d3-0a898a9a6d8b" />



#### Configure the R2 serial link-local address

So in this our lab says ``the serial interface is already configured``, so first inspect it:
````
exit
R2# show ipv6 interface brief
````
<img width="491" height="287" alt="image" src="https://github.com/user-attachments/assets/1c39be9c-1ef4-4ad8-95e3-2a807b9a0603" />


So now it ready.


---


#### Configure PC3

Click **PC3** → **Desktop** → **IP Configuration**, In the IPv6 section, enter:

| Setting       | Value                 |
| ------------- | --------------------- |
| IPv6 Address  | `2001:DB8:C0DE:12::A` |
| Prefix Length | `64`                  |
| IPv6 Gateway  | `FE80::2`             |

<img width="872" height="682" alt="image" src="https://github.com/user-attachments/assets/6d94daf2-8c17-4b56-8fe8-baeaf8285f50" />

---


#### Configure PC4

Click **PC4** → **Desktop** → **IP Configuration**:

| Setting       | Value                 |
| ------------- | --------------------- |
| IPv6 Address  | `2001:DB8:C0DE:13::A` |
| Prefix Length | `64`                  |
| IPv6 Gateway  | `FE80::2`             |

<img width="872" height="671" alt="image" src="https://github.com/user-attachments/assets/0ee2721e-72e4-4dfe-935b-03e74e2c1b34" />


---


#### Score:

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/fe2685b0-7a8e-4197-99f0-20d0c33c9320" />


Now we completed and got full score.


---



#### Verify IPv6 connectivity

So in this if we want to verify, just go to **PC3**, open **Desktop** → **Command Prompt** and run:
````
ping 2001:DB8:C0DE:12::1
ping 2001:DB8:C0DE:13::A
````
<img width="866" height="627" alt="image" src="https://github.com/user-attachments/assets/1c94424e-d3f8-4586-a7c8-2d5c69057874" />


Now we got success.


On **PC4**, run:
````
ping 2001:DB8:C0DE:13::1
ping 2001:DB8:C0DE:12::A
````

<img width="872" height="661" alt="image" src="https://github.com/user-attachments/assets/733633af-5fad-4ec2-84c3-08c3a69dfcc1" />


Now we got success all.

-----
