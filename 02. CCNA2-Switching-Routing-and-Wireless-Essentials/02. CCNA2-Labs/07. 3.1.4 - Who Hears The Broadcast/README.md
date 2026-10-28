<h1 align="center"> LAB: 3.1.4 - Who Hears The Broadcast </h1>


---


### Lab Guide

[3.1.4 Packet Tracer - Who Hears the Broadcast.docx](https://github.com/user-attachments/files/34065196/3.1.4.Packet.Tracer.-.Who.Hears.the.Broadcast.docx)


---

### Objectives

**Part 1: Observe Broadcast Traffic in a VLAN Implementation**

**Part 2: Complete Review Questions**



---


## Lab Walkthrough


<img width="1175" height="692" alt="image" src="https://github.com/user-attachments/assets/a2fe4113-1863-4e0c-8d9f-fbc2f0bef8c5" />



---


### Step 1: Use ping to generate traffic.

#### A. Open PC0

Click **PC0** → **Desktop** → **Command Prompt**:



#### B. Run the ping command

````
ping 192.168.1.8
````
**Output:**
````cisco
Pinging 192.168.1.8 with 32 bytes of data:

Reply from 192.168.1.8: bytes=32 time<1ms TTL=128
Reply from 192.168.1.8: bytes=32 time<1ms TTL=128
Reply from 192.168.1.8: bytes=32 time<1ms TTL=128
Reply from 192.168.1.8: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
````



---


### Step 2: Generate and examine broadcast traffic in a VLAN implementation.


#### Switch to Simulation mode
Click **Simulation** in the bottom-right area of Packet Tracer:

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/c78a10d0-d67f-47d9-8809-63db3485ac60" />


Click **Edit Filters**:

<img width="1252" height="755" alt="image" src="https://github.com/user-attachments/assets/df5734f2-a66c-4a92-8462-6999bbe7b530" />


Uncheck **Show All/None** to clear the selections, then Select only **ICMP**:

<img width="551" height="647" alt="image" src="https://github.com/user-attachments/assets/181c6173-2902-4a88-973c-bc2351533e3c" />


The we can Close the filter window.




#### Create a broadcast PDU from PC0

Select **Add Complex PDU**, Then select **PC0** as the source:

Move our cursor over the topology and click **PC0**. The **Create Complex PDU** dialog opens.

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/5400550a-f155-4c72-b56a-6fa389837a09" />


Enter the following values:
| Setting | Value |
|---|---|
| Destination IP Address | `255.255.255.255` |
| Sequence Number | `1` |
| One Shot Time | `0` |
| Select Application | `PING` |

After complete click **Create PDU**:

<img width="391" height="670" alt="image" src="https://github.com/user-attachments/assets/84d36f67-34c0-461e-8117-660867da33ef" />


Click on **Capture/Forward** twice or click on **Capture then forward**:

<img width="1907" height="1076" alt="image" src="https://github.com/user-attachments/assets/7ff9c232-d8c6-4da0-830c-d692f53fcc18" />


Then click it again:

<img width="1911" height="796" alt="image" src="https://github.com/user-attachments/assets/12b6588f-1d49-4b6c-9b36-25e0ff4a8cc6" />


Now we see it sending:
<img width="1907" height="757" alt="image" src="https://github.com/user-attachments/assets/cfe188f7-12c8-403a-9a53-81d6ad4cd22f" />


And now it finished:

<img width="1907" height="762" alt="image" src="https://github.com/user-attachments/assets/b70dd26b-b4d8-4bb1-b9f5-463740823419" />


Then click on it again:

<img width="1907" height="800" alt="image" src="https://github.com/user-attachments/assets/9eb0ed07-75ca-47c3-9b98-d47963bd111f" />


<img width="1902" height="757" alt="image" src="https://github.com/user-attachments/assets/4ea9a063-c4df-49d8-90b4-9ccfbe8406b8" />

Then click on it until it show **buffer full**:

<img width="1907" height="762" alt="image" src="https://github.com/user-attachments/assets/ce02dbb1-c94e-454f-aa36-6747767c3080" />


In this just click on `Clea Even List`.

> Observe the events on the topology. We should see the packet move from PC0 to the switch, and then the switch forwards the broadcast to the other PCs in PC0's VLAN.

> In this version of the activity, **PC0** belongs to **VLAN 30**. The broadcast reaches the other end devices in **VLAN 30,** but not the PCs in **VLAN 10** or **VLAN 20**.



#### Repeat the broadcast from PC8 and PC16

Repeat Steps 3 and 4 for each source.

For each new test, use **Add Complex PDU**, click the required source PC, and enter the same destination, sequence number, time, and application. Clear or remove the previous PDU if needed so you can clearly identify the current test.

| Source PC | VLAN | Expected Recipients |
|---|---|---|
| PC0 | VLAN 30 | Other PCs in VLAN 30 |
| PC8 | VLAN 10 | Other PCs in VLAN 10 |
| PC16 | VLAN 20 | Other PCs in VLAN 20 |


The switch limits each broadcast to the VLAN where it originated. This is the central observation for this.


##### Repeat the broadcast from PC8

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/b5212771-fd1e-4570-bdce-7f660283ac1a" />


<img width="1917" height="942" alt="image" src="https://github.com/user-attachments/assets/3150f18d-80d5-4234-968c-095b219fb952" />


Then click on **Capture then forward** until completed:

<img width="1917" height="797" alt="image" src="https://github.com/user-attachments/assets/5e5e9580-55bd-435a-ad42-d2b4b11e5d1b" />


Click on it until it show **Buffer Full**.


##### Repeat the broadcast from PC16

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/5be98f35-da2e-407c-ad9b-6e73f39a692a" />



<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/50bb6c4f-5858-4730-90f8-53f130eaaed6" />


<img width="1901" height="760" alt="image" src="https://github.com/user-attachments/assets/aa6009ac-1394-4abc-a4b7-35ae2f01989c" />

Then we can also click on **Capture then forward** until completed:



**Now we completed.**


-----



### Reflection Questions

1. If a PC in VLAN 10 sends a broadcast message, which devices receive it?

> All other end devices in **VLAN 10** - **PC8** through **PC15**, excluding the sending PC from receiving its own transmitted frame.


2. If a PC in VLAN 20 sends a broadcast message, which devices receive it?

> All other end devices in **VLAN 20** - **PC16** through **PC23**, excluding the sender.


3. If a PC in VLAN 30 sends a broadcast message, which devices receive it?

> All other end devices in **VLAN 30** - **PC0** through **PC7**, excluding the sender.


4. What happens to a frame sent from a PC in VLAN 10 to a PC in VLAN 30?

> The frame is not forwarded directly into **VLAN 30**. The switch keeps Layer 2 traffic within its VLAN. Communication between **VLAN 10** and **VLAN 30** requires a router or Layer 3 switch configured for inter-VLAN routing.

5. Which ports on the switch light up if a PC connected to port 11 sends a unicast message to a PC connected to port 13?

> **Ports 11 and 13**. Both ports are in the same VLAN, so the switch can forward the unicast frame directly to the destination port.

6. Which ports on the switch light if a PC connected to port 2 sends a unicast message to a PC connected to port 23?

> The frame is **not delivered to port 23**, because the two ports belong to different VLANs. The expected worksheet answer is that the packet is dropped rather than forwarded directly between the VLANs.

7. In terms of ports, what are the collision domains on the switch?

> Each switch port is its own collision domain. With 24 active switch ports, there are **24 collision domains** - one per port.

8. In terms of ports, what are the broadcast domains on the switch?

Each VLAN is a separate broadcast domain. There are 3 broadcast domains:
| Broadcast Domain | Switch Ports |
|---|---|
| VLAN 30 | `Fa0/1–Fa0/8` |
| VLAN 10 | `Fa0/9–Fa0/16` |
| VLAN 20 | `Fa0/17–Fa0/24` |

----
