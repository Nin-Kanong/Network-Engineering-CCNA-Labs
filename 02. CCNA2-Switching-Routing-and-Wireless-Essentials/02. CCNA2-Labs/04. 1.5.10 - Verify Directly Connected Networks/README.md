<h1 align="center"> LAB: 1.5.10 - Verify Directly Connected Networks </h1>


---


### Lab Guide

[1.5.10 Packet Tracer - Verify Directly Connected Networks.docx](https://github.com/user-attachments/files/34030930/1.5.10.Packet.Tracer.-.Verify.Directly.Connected.Networks.docx)


---


### Addressing Table

#### IPv4 - R1

| Device | Interface | IP Address / Prefix | Default Gateway |
|---|---|---|---|
| R1 | G0/0/0 | `172.16.20.1/25` | N/A |
| R1 | G0/0/1 | `172.16.20.129/25` | N/A |
| R1 | S0/1/0 | `209.165.200.225/30` | N/A |
| PC1 | NIC | `172.16.20.10/25` | `172.16.20.1` |
| PC2 | NIC | `172.16.20.138/25` | `172.16.20.129` |


#### IPv6 - R2

| Device | Interface | IPv6 Address / Prefix | Default Gateway |
|---|---|---|---|
| R2 | G0/0/0 | `2001:db8:c0de:12::1/64` | N/A |
| R2 | G0/0/1 | `2001:db8:c0de:13::1/64` | N/A |
| R2 | S0/1/1 | `2001:db8:c0de:11::1/64` | N/A |
| R2 | S0/1/1 | `fe80::2` (link-local) | N/A |
| PC3 | NIC | `2001:db8:c0de:12::a/64` | `fe80::2` |
| PC4 | NIC | `2001:db8:c0de:13::a/64` | `fe80::2` |

The ``/25`` IPv4 subnet mask is ``255.255.255.128``. The IPv6 LANs use a ``/64`` prefix.

---

## Lab Walkthrough

<img width="1160" height="522" alt="image" src="https://github.com/user-attachments/assets/c6ceed06-488f-4ff5-8eb7-31534c7a718a" />


### Part 1: Verify IPv4 directly connected networks

#### Step 1: Open R1 and check interface status

Click on **R1** -> **CLI**, then press `Enter`:

And it will show required password:
````
cisco
````
<img width="867" height="866" alt="image" src="https://github.com/user-attachments/assets/3b06b4df-2a1a-41a9-99bd-d40ed2ca48cc" />


Enter privileged EXEC mode using the password ``class``:
````
R1> enable
Password: class
R1#
````


Run the required command:
```cisco
R1# show ip interface brief | exclude unassigned
```

**Output:**

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   172.16.20.1     YES manual administratively down down
GigabitEthernet0/0/1   172.16.20.129   YES manual up                    up
Serial0/1/0            209.165.200.229 YES manual up                    up
R1#
```

Check the **Status** and **Protocol** columns:
| Status | Protocol | Meaning |
|---|---|---|
| `up` | `up` | Interface is operating normally. |
| `administratively down` | `down` | Interface is disabled by configuration. |
| `down` | `down` | Interface or its connection may have a problem. |
| `up` | `down` | The interface protocol is not operating correctly. |



````
R1# configure terminal
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# no shutdown
R1(config-if)# end
````

Then verify:
````
R1# show ip interface brief | exclude unassigned
````
**Output**:
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0/0   172.16.20.1     YES manual up                    up 
GigabitEthernet0/0/1   172.16.20.129   YES manual up                    up 
Serial0/1/0            209.165.200.229 YES manual up                    up 
R1#
````

Now it up all.

> ``G0/0/0`` is administratively down.
> ``S0/1/0`` has an incorrect IPv4 address. It should be ``209.165.200.225/30``, not ``209.165.200.229``.



#### the R1 serial IPv4 address
````
R1(config)# interface serial 0/1/0
R1(config-if)# ip address 209.165.200.225 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# end
R1#
````

Then check again:
````
R1# show ip interface brief | exclude unassigned
````
**Output**:
````cisco
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0/0   172.16.20.1     YES manual up                    up 
GigabitEthernet0/0/1   172.16.20.129   YES manual up                    up 
Serial0/1/0            209.165.200.225 YES manual up                    up
````




Find the gateway of last resort:


````
R1# show ip route | begin Gate
````

**Output**:
````
Gateway of last resort is 209.165.200.226 to network 0.0.0.0

     172.16.0.0/16 is variably subnetted, 4 subnets, 2 masks
C       172.16.20.0/25 is directly connected, GigabitEthernet0/0/0
L       172.16.20.1/32 is directly connected, GigabitEthernet0/0/0
C       172.16.20.128/25 is directly connected, GigabitEthernet0/0/1
L       172.16.20.129/32 is directly connected, GigabitEthernet0/0/1
     209.165.200.0/24 is variably subnetted, 2 subnets, 2 masks
C       209.165.200.224/30 is directly connected, Serial0/1/0
L       209.165.200.225/32 is directly connected, Serial0/1/0
S*   0.0.0.0/0 [1/0] via 209.165.200.226
````

Here, ``C`` means connected, and ``S*`` identifies a candidate default static route.


##### Find the Circuit ID
````
R1# show interfaces | include Desc|conn
````
**Output**:
````cisco
GigabitEthernet0/0/0 is up, line protocol is up (connected)
  Description: Connection to SW1
GigabitEthernet0/0/1 is up, line protocol is up (connected)
  Description: Connection to SW2
Serial0/1/0 is up, line protocol is up (connected)
  Description: Circuit ID BCB123450001
````

> Circuit ID: ``BCB123450001``



##### Check duplex, speed, and media type
````
R1# show interfaces gigabitethernet 0/0/0
````
<img width="612" height="402" alt="image" src="https://github.com/user-attachments/assets/c4b31a5d-ecce-41ec-bcdf-206dc7a27b05" />


---



#### Step 2: Test IPv4 connectivity

##### Check PC1's settings

1. Click **PC1**.
2. Open **Desktop**.
3. Open **IP Configuration**.
4. Check that the values match this table.

Now we see this:

<img width="875" height="658" alt="image" src="https://github.com/user-attachments/assets/ea2eb526-4463-4123-a062-22c058954683" />


##### Check PC2's settings

Click **PC2** → **Desktop** → **IP Configuration**:

<img width="870" height="683" alt="image" src="https://github.com/user-attachments/assets/b136a008-2967-4d97-81d1-cf69965205bd" />




##### Ping PC2 from PC1

On **PC1** → open **Desktop** → **Command Prompt**:
````
ping 172.16.20.138
````
<img width="873" height="442" alt="image" src="https://github.com/user-attachments/assets/d64aa3f0-09b0-4bcd-b395-6395b7dd1c5e" />


##### Ping the Dual Stack Server
From the same **PC1** command prompt, run:
````
ping 64.100.1.10
````
<img width="868" height="655" alt="image" src="https://github.com/user-attachments/assets/3d7a3be1-4ee7-4bea-b6ad-0f3a8e49de64" />


----




### Part 2: Verify IPv6 Directly Connected Networks

#### Step 1: Verify IPv6 addresses and port status on R2.


Click **R2** → **CLI** → press **Enter**, Password is:
````
cisco
````

<img width="868" height="872" alt="image" src="https://github.com/user-attachments/assets/6cfa6c75-15e1-4811-baa2-b3f8ca23dcce" />



And enter privileged EXEC mode:
````
R2> enable
Password: class
R2#
````



##### Check IPv6 interface status
````
R2>show ipv6 interface brief
````
**Output:**
````
GigabitEthernet0/0/0       [up/up]
    FE80::2
    2001:DB8:C0DE:12::1
GigabitEthernet0/0/1       [up/up]
    FE80::2
    2001:DB8:C0DE:14::1
Serial0/1/0                [administratively down/down]
    unassigned
Serial0/1/1                [up/up]
    FE80::2D0:BCFF:FE32:7C24
    2001:DB8:C0DE:11::1
Vlan1                      [administratively down/down]
    unassigned
````



##### Correct R2 G0/0/1

````
R2> enable
Password: class
R2#
````
Then:
````
R2# configure terminal
R2(config)# interface gigabitethernet 0/0/1
R2(config-if)# no ipv6 address 2001:DB8:C0DE:14::1/64
R2(config-if)# ipv6 address 2001:DB8:C0DE:13::1/64
R2(config-if)# no shutdown
R2(config-if)# end
````


##### Correct the serial link-local address

Our addressing table specifies ``FE80::2`` for **R2** ``S0/1/1``, but out output shows an automatically generated address. To match the table, enter:
````
R2# configure terminal
R2(config)# interface serial 0/1/1
R2(config-if)# ipv6 address FE80::2 link-local
R2(config-if)# no shutdown
R2(config-if)# end
````



##### Verify the IPv6 addresses
````
R2# show ipv6 int brief
````
**Output:**
````
GigabitEthernet0/0/0       [up/up]
    FE80::2
    2001:DB8:C0DE:12::1
GigabitEthernet0/0/1       [up/up]
    FE80::2
    2001:DB8:C0DE:13::1
Serial0/1/0                [administratively down/down]
    unassigned
Serial0/1/1                [up/up]
    FE80::2
    2001:DB8:C0DE:11::1
Vlan1                      [administratively down/down]
    unassigned
````


Now it correct all.

----


#### Step 2: Verify connectivity.


##### On PC3

1. Click **PC3** in the topology.
2. Select **Desktop**.
3. Click **Command Prompt**.
4. Enter this command:

````
ping 2001:db8:c0de:13::a
````

<img width="872" height="433" alt="image" src="https://github.com/user-attachments/assets/9b16a7f5-4c5c-42a5-9c77-daaf93cb6d2d" />


Now it have connection.




##### Ping PC3 from PC4

Open **PC4** → **Desktop** → **Command Prompt** and enter:
````
ping 2001:db8:c0de:12::a
````
<img width="870" height="538" alt="image" src="https://github.com/user-attachments/assets/1b60f406-fb76-46b0-8b44-7519d78edb21" />


Now we it correct all.


----



#### Score:

<img width="1907" height="1076" alt="image" src="https://github.com/user-attachments/assets/c99f6140-71c1-4771-895c-f934b738f41d" />



Now we got full score.


-------
