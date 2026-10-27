<h1 align="center"> LAB: 1.5.10 - Verify Directly Connected Networks </h1>



---


### Lab Guide



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
R1#configure terminal
R1(config)#interface gigabitEthernet 0/0/0
R1(config-if)#no shutdown
R1(config-if)#end
````

Then verify:
````
R1#show ip interface brief | exclude unassigned
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



#### Step 2: Verify R1's IPv4 addresses
````
R1#show running-config
````
**Output**:
````
R1#show running-config
Building configuration...

Current configuration : 1007 bytes
!
version 15.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
!
ip cef
no ipv6 cef
!
spanning-tree mode pvst
!
interface GigabitEthernet0/0/0
 description Connection to SW1
 ip address 172.16.20.1 255.255.255.128
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/1
 description Connection to SW2
 ip address 172.16.20.129 255.255.255.128
 duplex auto
 speed auto
!
interface Serial0/1/0
 description Circuit ID BCB123450001
 ip address 209.165.200.229 255.255.255.248
 clock rate 2000000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 mac-address 0005.5e16.5301
 no ip address
 shutdown
!
ip classless
ip route 0.0.0.0 0.0.0.0 209.165.200.226 
!
ip flow-export version 9
!
line con 0
 password cisco
 login
line aux 0
line vty 0 4
 password cisco
 login
end
````



#### Step 3: Display the IPv4 routing table










































































































