<h1 align="center"> 1.6.2 - Configure Basic Router Settings Physical Mode </h1>



---

### Lab Guide:


[1.6.2 Packet Tracer  - Configure Basic Router Settings - Physical Mode.docx](https://github.com/user-attachments/files/34061846/1.6.2.Packet.Tracer.-.Configure.Basic.Router.Settings.-.Physical.Mode.docx)


---


### Addressing Table


| Device | Interface | IP Address / Prefix | Default Gateway |
|---|---|---|---|
| R1 | G0/0/0 | `192.168.0.1/24` | N/A |
| R1 | G0/0/0 | `2001:db8:acad::1/64` | N/A |
| R1 | G0/0/0 | `fe80::1` | N/A |
| R1 | G0/0/1 | `192.168.1.1/24` | N/A |
| R1 | G0/0/1 | `2001:db8:acad:1::1/64` | N/A |
| R1 | G0/0/1 | `fe80::1` | N/A |
| R1 | Loopback0 | `10.0.0.1/24` | N/A |
| R1 | Loopback0 | `2001:db8:acad:2::1/64` | N/A |
| R1 | Loopback0 | `fe80::1` | N/A |
| PC-A | NIC | `192.168.1.10/24` | `192.168.1.1` |
| PC-A | NIC | `2001:db8:acad:1::10/64` | `fe80::1` |
| Server | NIC | `192.168.0.10/24` | `192.168.0.1` |
| Server | NIC | `2001:db8:acad::10/64` | Not provided |


---


### Topology

````mermaid
flowchart LR
    %% Devices
    PCA["🖥️ <b>PC-A</b>"]
    S1["🔀 <b>S1</b>"]
    R1["🖧 <b>R1</b>"]
    Server["🗄️ <b>Server</b>"]

    %% Connections with Interfaces
    PCA ---|F0/6| S1
    S1 ---|F0/5| R1
    R1 ---|G0/0/0| Server

    %% Styling (Cisco Packet Tracer colors)
    classDef pc fill:#4a90e2,stroke:#2c5282,stroke-width:2px,color:#fff;
    classDef switch fill:#3182ce,stroke:#2b6cb0,stroke-width:2px,color:#fff;
    classDef router fill:#4299e1,stroke:#2b6cb0,stroke-width:2px,color:#fff;
    classDef server fill:#2b6cb0,stroke:#1a365d,stroke-width:2px,color:#fff;
    
    class PCA pc;
    class S1 switch;
    class R1 router;
    class Server server;
````

---


### Objectives

**Part 1: Set Up the Topology and Initialize Devices**

**Part 2: Configure Devices and Verify Connectivity**

**Part 3: Display Router Information**


---

## Lab Walkthrough

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/a3e9c8f3-8027-423e-adbc-6d4fb653ca77" />



---


### Part 1: Set Up the Topology and Initialize Devices


#### Step 1: Cable the network as shown in the topology

<img width="1230" height="871" alt="image" src="https://github.com/user-attachments/assets/1a824148-3bcd-4a03-b9b4-953f615bef39" />



<img width="1235" height="871" alt="image" src="https://github.com/user-attachments/assets/badab24c-4aae-427c-9265-029184967016" />


<img width="1230" height="872" alt="image" src="https://github.com/user-attachments/assets/21472b00-cd30-429f-a5cc-a494eee27f7e" />


<img width="1235" height="872" alt="image" src="https://github.com/user-attachments/assets/7ad465ca-89b6-4fb8-af50-ed3e326a285d" />


<img width="1232" height="872" alt="image" src="https://github.com/user-attachments/assets/d86c2fbd-1b75-45f1-b400-a2cac678d3c6" />



<img width="1245" height="857" alt="image" src="https://github.com/user-attachments/assets/70ba9a11-3987-4e39-9e14-a11bb66703a7" />



<img width="1917" height="846" alt="image" src="https://github.com/user-attachments/assets/704a3fa5-1e88-4a7c-8679-3ad1deb2fb99" />


<img width="1281" height="752" alt="image" src="https://github.com/user-attachments/assets/7867a4c6-7a54-44c4-a7eb-bfeb6d415035" />



<img width="1527" height="712" alt="image" src="https://github.com/user-attachments/assets/5a82a742-0f74-4b28-90a5-09c0d776f9cc" />


<img width="1591" height="847" alt="image" src="https://github.com/user-attachments/assets/c79fec89-b056-49de-a4a6-db74ad2a411b" />


<img width="1897" height="847" alt="image" src="https://github.com/user-attachments/assets/4ff0ccd0-4a52-459b-9383-945a232fa704" />


<img width="1236" height="816" alt="image" src="https://github.com/user-attachments/assets/eea0e235-b805-49ea-9934-23896e397980" />


Power on the **Cisco 4321 ISR**, **PC-A**, and **Server**:

Then click on this button to power On:

<img width="1187" height="812" alt="image" src="https://github.com/user-attachments/assets/5b56a01d-ec24-4703-8001-3620ebde5465" />



Then click on it to make it show yellow leigh:

<img width="1196" height="797" alt="image" src="https://github.com/user-attachments/assets/28ff80d0-e208-44ba-a315-891c3d84d668" />


<img width="1232" height="787" alt="image" src="https://github.com/user-attachments/assets/8a513a8f-f64f-42a0-a8f7-2de63002b03d" />


<img width="1257" height="867" alt="image" src="https://github.com/user-attachments/assets/3d451b06-239b-4976-b329-ddcde3d40239" />


---




### Part 2: Configure Devices and Verify Connectivity

#### Step 1: Configure the PC interfaces.

The router will provide access between two IPv4/IPv6 networks, while Loopback0 will provide the remote SSH destination.

<img width="1252" height="870" alt="image" src="https://github.com/user-attachments/assets/290248dd-a61a-4c46-9fee-c531044c305a" />


##### A. PC-A configuration
Click **PC-A** → **Desktop** → **IP Configuration**, then Configure the IPv4 settings:

| Setting | Value |
|---|---|
| IPv4 address | `192.168.1.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.1.1` |


Configure the IPv6 settings using Static:
| Setting | Value |
|---|---|
| IPv6 address | `2001:db8:acad:1::10` |
| Prefix length | `64` |
| IPv6 default gateway | `fe80::1` |


<img width="875" height="868" alt="image" src="https://github.com/user-attachments/assets/a0d0f1ce-378e-4c7e-9b04-20aad7d71f71" />


##### B. Server configuration

Click **Server** → **Desktop** → **IP Configuration**:
| Setting | Value |
|---|---|
| IPv4 address | `192.168.0.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.0.1` |


Configure IPv6 using Static for the initial connectivity tests:

| Setting | Value |
|---|---|
| IPv6 address | `2001:db8:acad::10` |
| Prefix length | `64` |
| IPv6 default gateway | `fe80::1` |


<img width="1257" height="872" alt="image" src="https://github.com/user-attachments/assets/93bccad0-7243-4bfc-afd5-e25a45c2c7ee" />


<img width="872" height="637" alt="image" src="https://github.com/user-attachments/assets/fed7d592-6870-401b-b26d-95a1c251b10b" />


> Keep the Server IPv6 address static for now. We will change it to automatic configuration later in Part 3.

---


#### Step 2: Configure the router.

##### Open the router CLI

Click **PC-A**:

<img width="1262" height="867" alt="image" src="https://github.com/user-attachments/assets/81ae80c6-f24d-437d-91dc-0dc5a340d8e8" />


Go to **Terminal** -> click **OK**, then press **Enter**:

<img width="870" height="435" alt="image" src="https://github.com/user-attachments/assets/440d4afb-5ea1-4096-8cd4-cfef220e0923" />


````
Router> enable
Router# configure terminal
````


##### Configure the hostname and security settings
Type these commands in the following order:
````
Router(config)# hostname R1
R1(config)# ip domain-name ccna-lab.com
R1(config)# service password-encryption
R1(config)# security passwords min-length 12
R1(config)# username SSHadmin secret 55Hadm!n2020
R1(config)# enable secret $cisco!PRIV*
````

> The command ``security passwords min-length 12`` sets a minimum password length of 12 characters. Configure it before creating the passwords.



##### Next, generate the RSA keys required for SSH:
````
R1(config)# crypto key generate rsa general-keys modulus 1024
````

> **Note**: In this If your Packet Tracer IOS does not accept general-keys, try:

````
R1(config)# crypto key generate rsa modulus 1024
````
The router should create 1024-bit RSA keys using the hostname and domain name we configured.




##### Configure the console line

The console password is ``$cisco!!CON*``. Sessions must disconnect after four minutes of inactivity.
````
R1(config)# line console 0
R1(config-line)# password $cisco!!CON*
R1(config-line)# exec-timeout 4 0
R1(config-line)# login
R1(config-line)# exit
````


##### Configure the VTY lines for SSH only
````
R1(config)# line vty 0 4
R1(config-line)# password $cisco!!VTY*
R1(config-line)# exec-timeout 4 0
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exit
````

> This configuration sets the VTY line password, allows SSH instead of Telnet, sets the four-minute idle timeout, and authenticates remote users using the local username database.

> **Note**: For SSH, log in using username ``SSHadmin`` and password ``55Hadm!n2020``. The VTY line password is not the SSH username password when ``login local`` is configured.


##### E. Configure the banner
````
R1(config)# banner motd $ Unauthorized access is prohibited! $
````
> The banner warns users that unauthorized access is prohibited.




##### Enable IPv6 routing
````
R1(config)# ipv6 unicast-routing
````

> This allows R1 to route IPv6 traffic between its IPv6 networks.


##### Configure the three interfaces

**Interface 1: G0/0/0 - Connection to Server**:
````
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ip address 192.168.0.1 255.255.255.0
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:db8:acad::1/64
R1(config-if)# description Connection to Server
R1(config-if)# no shutdown
R1(config-if)# exit
````


**Interface 2: G0/0/1 - Connection to S1**:
````
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# description Connection to S1
R1(config-if)# no shutdown
R1(config-if)# exit
````

**Interface 3: Loopback0 - SSH destination**:
````
R1(config)# interface loopback 0
R1(config-if)# ip address 10.0.0.1 255.255.255.0
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# description loopback adapter
R1(config-if)# no shutdown
R1(config-if)# exit
````



##### Configure login blocking

The router must block login attempts for two minutes if three failures occur within 60 seconds:
````
R1(config)# login block-for 120 attempts 3 within 60
````


##### Set the router clock

Return to privileged EXEC mode:
````
R1(config)# end
````

Set the clock:
````
R1# clock set 15:20:00 28 Oct 2026
````


##### Save the configuration
````
R1# copy running-config startup-config
````
Press **Enter** if prompted to accept the destination filename.


> This saves the configuration to NVRAM so it can be loaded after a restart.


----



#### Score

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/47998d6c-0aae-466a-9196-98f69deaaaed" />


Now we got full score.


----




#### Step 3: Verify network connectivity.

##### A. Ping Server from PC-A

Click **PC-A** → **Desktop** → **Command Prompt**:
````
ping 192.168.0.10
ping 2001:db8:acad::10
````
<img width="866" height="652" alt="image" src="https://github.com/user-attachments/assets/399fc8b1-685a-499e-8f8d-c9118017566e" />


Now it success.

##### B. Connect to R1 using SSH over IPv4

On **PC-A**, open **Desktop** → **Telnet/SSH Client**:

Use these settings:

| Setting | Value |
|---|---|
| Connection type | SSH |
| Hostname / IP address | `10.0.0.1` |
| Username | `SSHadmin` |
| Password | `55Hadm!n2020` |
| Port | `22` |

<img width="870" height="372" alt="image" src="https://github.com/user-attachments/assets/eb654fd5-a7ea-4592-bc70-4fb9d99d2237" />


<img width="867" height="382" alt="image" src="https://github.com/user-attachments/assets/e4bdaa14-4a43-4472-a05a-41120f86fa2e" />


##### C. Connect to R1 using SSH over IPv6

Open the Telnet/SSH client again and use:
| Setting | Value |
|---|---|
| Connection type | SSH |
| IPv6 address | `2001:db8:acad:2::1` |
| Username | `SSHadmin` |
| Password | `55Hadm!n2020` |
| Port | `22` |

<img width="867" height="337" alt="image" src="https://github.com/user-attachments/assets/cfb0020c-dfd4-42be-aa32-358ff5d6c5d4" />


<img width="875" height="347" alt="image" src="https://github.com/user-attachments/assets/0ec1537c-429e-42ac-bce0-450d7f3bcc74" />


----


### Part 3: Display Router Information

#### Step 1: Establish an SSH session to R1.

From **PC-A**, open the **Telnet/SSH client** and connect to:
````
2001:db8:acad:2::1
````
Log in as ``SSHadmin``, using password ``55Hadm!n2020``.

<img width="872" height="316" alt="image" src="https://github.com/user-attachments/assets/115f73b1-000e-459a-994f-9fe8dd80bfa5" />


<img width="875" height="266" alt="image" src="https://github.com/user-attachments/assets/325e05ed-8de1-4823-bebb-4f86f81661d7" />


At the router prompt, enter:
````
R1> enable
Password: $cisco!PRIV*
R1#
````

> The privileged EXEC password is different from the SSH user password.



#### Step 2: Retrieve important hardware and software information.

##### A. Display IOS information

````
R1# show version
````
**Output**:
````
Cisco IOS XE Software, Version 03.16.05.S - Extended Support Release
Cisco IOS Software, ISR Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version Version 15.5 (3)S5, RELEASE SOFTWARE (fc2)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2017 by Cisco Systems, Inc.
Compiled Thu 19-Jan-17 11:24 by mcpre

Cisco IOS-XE software, Copyright (c) 2005-2017 by cisco Systems, Inc.
All rights reserved.  Certain components of Cisco IOS-XE software are
licensed under the GNU General Public License ("GPL") Version 2.0.  The
software code licensed under GPL Version 2.0 is free software that comes
with ABSOLUTELY NO WARRANTY.  You can redistribute and/or modify such
GPL code under the terms of GPL Version 2.0.  For more details, see the
documentation or "License Notice" file accompanying the IOS-XE software,
or the applicable URL provided on the flyer accompanying the IOS-XE
software.

ROM: IOS-XE ROMMON

Router uptime is 37 minutes, 27 seconds
Uptime for this control processor is 37 minutes, 27 seconds
System returned to ROM by power-on
System image file is "bootflash:/isr4300-universalk9.03.16.05.S.155-3.S5-ext.SPA.bin"
Last reload reason: PowerOn

This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.

Suite License Information for Module:'esg'

--------------------------------------------------------------------------------
Suite                 Suite Current         Type           Suite Next reboot

--------------------------------------------------------------------------------
FoundationSuiteK9     None                  None           None

securityk9
appxk9
	
AdvUCSuiteK9          None                  None           None

uck9
cme - srst
cube

Technology Package License Information:

------------------------------------------------------------------------
Technology    Technology-package                  Technology-package
              Current              Type           Next reboot
------------------------------------------------------------------------
appxk9           None             None             None
uck9             None             None             None
securityk9       securityk9       Permanent        securityk9
ipbase           ipbasek9         Permanent        ipbasek9
security         securityk9       Permanent        securityk9
ipbase           ipbasek9         Permanent        ipbasek9

cisco ISR4321/K9 (1RU) processor with 1687137K/6147K bytes of memory.
Processor board ID FLM2041W2HD
2 Gigabit Ethernet interfaces
32768K bytes of non-volatile configuration memory.
4194304K bytes of physical memory.
3223551K bytes of flash memory at bootflash:.

Configuration register is 0x2102
````

**Look for:**
````
System image file is "bootflash:/isr4300-universalk9.03.16.05.S.155-3.S5-ext.SPA.bin"
32768K bytes of non-volatile configuration memory.
3223551K bytes of flash memory at bootflash:.
````


##### B. Check the configuration register
````
R1# show version | include register
````
**Output:**
````
Configuration register is 0x2102
````

---



#### Step 3: Display the startup configuration.


##### A. Display the startup configuration
````
R1# show startup-config
````
We may need to **press** the Space bar to view additional pages.

> Passwords are encrypted or obfuscated in the saved configuration. Line passwords protected by ``service password-encryption`` commonly appear as type 7 values, while ``enable secret`` and username secrets appear in hashed form. Type 7 is reversible obfuscation, not strong cryptographic protection.


##### B. Display only the VTY section
````
R1# show running-config | section vty
````
**Output**:
````
line vty 0 4
 exec-timeout 4 0
 password 7 08654F471A1A0A56533D383D60
 login local
 transport input ssh
````

---

#### Step 4: Display the IPv4 routing table
````
R1# show ip route
````
**Output**:
````
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       10.0.0.0/24 is directly connected, Loopback0
L       10.0.0.1/32 is directly connected, Loopback0
     192.168.0.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.0.0/24 is directly connected, GigabitEthernet0/0/0
L       192.168.0.1/32 is directly connected, GigabitEthernet0/0/0
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, GigabitEthernet0/0/1
L       192.168.1.1/32 is directly connected, GigabitEthernet0/0/1
````


---


#### Step 5: Display a summary of interfaces


##### A. IPv4 interface summary

````
R1# show ip interface brief
````
**Output:**
````
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0/0   192.168.0.1     YES manual up                    up 
GigabitEthernet0/0/1   192.168.1.1     YES manual up                    up 
Loopback0              10.0.0.1        YES manual up                    up
````



##### B. IPv6 interface summary
````
R1# show ipv6 interface brief
````
**Output:**
````
GigabitEthernet0/0/0       [up/up]
    FE80::1
    2001:DB8:ACAD::1
GigabitEthernet0/0/1       [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
Loopback0                  [up/up]
    FE80::1
    2001:DB8:ACAD:2::1
````

---



#### Change Server IPv6 to automatic configuration

Go to **Server** → **Desktop** → **IP Configuration**:

<img width="872" height="657" alt="image" src="https://github.com/user-attachments/assets/0230d52c-9d4c-4fbc-b303-572ee280fa00" />


##### A. Check the IPv6 address

Open **Server** → **Desktop** → **Command Prompt** and enter:

````
ipconfig
````
**Output:**
````
FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: FE80::207:ECFF:FEA5:6286
   IPv6 Address....................: 2001:DB8:ACAD:0:207:ECFF:FEA5:6286
   IPv4 Address....................: 192.168.0.10
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: FE80::1
                                     192.168.0.1
````

Now we completed Lab.

-----
