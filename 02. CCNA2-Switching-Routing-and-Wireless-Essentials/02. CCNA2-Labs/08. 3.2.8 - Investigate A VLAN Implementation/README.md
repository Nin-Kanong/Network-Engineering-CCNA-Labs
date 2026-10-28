<h1 align="center"> LAB: 3.2.8 - Investigate A VLAN Implementation </h1>


---


### Lab Guide:


[3.2.8 Packet Tracer - Investigate a VLAN Implementation.docx](https://github.com/user-attachments/files/34067801/3.2.8.Packet.Tracer.-.Investigate.a.VLAN.Implementation.docx)


---

### Addressing Table


| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| S1 | VLAN 99 | 172.17.99.31 | 255.255.255.0 | N/A |
| S2 | VLAN 99 | 172.17.99.32 | 255.255.255.0 | N/A |
| S3 | VLAN 99 | 172.17.99.33 | 255.255.255.0 | N/A |
| PC1 | NIC | 172.17.10.21 | 255.255.255.0 | 172.17.10.1 |
| PC2 | NIC | 172.17.20.22 | 255.255.255.0 | 172.17.20.1 |
| PC3 | NIC | 172.17.30.23 | 255.255.255.0 | 172.17.30.1 |
| PC4 | NIC | 172.17.10.24 | 255.255.255.0 | 172.17.10.1 |
| PC5 | NIC | 172.17.20.25 | 255.255.255.0 | 172.17.20.1 |
| PC6 | NIC | 172.17.30.26 | 255.255.255.0 | 172.17.30.1 |
| PC7 | NIC | 172.17.10.27 | 255.255.255.0 | 172.17.10.1 |
| PC8 | NIC | 172.17.20.28 | 255.255.255.0 | 172.17.20.1 |
| PC9 | NIC | 172.17.30.29 | 255.255.255.0 | 172.17.30.1 |

---

### Objectives

**Part 1: Observe Broadcast Traffic in a VLAN Implementation**

**Part 2: Observe Broadcast Traffic without VLANs**


---


## Lab Walkthrough

<img width="1157" height="662" alt="image" src="https://github.com/user-attachments/assets/c5eb5bb2-8423-4152-8be9-8342ead61248" />


---


### Part 1: Observe Broadcast Traffic in a VLAN Implementation

#### Step 1: Ping from PC1 to PC6.

Wait for all link lights to turn green.

Click the **Simulation** tab:

<img width="1922" height="1077" alt="image" src="https://github.com/user-attachments/assets/5c148880-db67-46a3-b147-03fb358df8a2" />


The VLAN membership in this activity is:

| VLAN | Devices | IP Subnet |
|---|---|---|
| VLAN 10 | PC1, PC4, PC7 | `172.17.10.0/24` |
| VLAN 20 | PC2, PC5, PC8 | `172.17.20.0/24` |
| VLAN 30 | PC3, PC6, PC9 | `172.17.30.0/24` |


#### Send a Simple PDU from PC1 to PC6

1. In Simulation mode, click **Add Simple PDU** (the envelope icon on the right toolbar).
2. Click **PC1** as the source.
3. Click **PC6** as the destination.

<img width="1916" height="1076" alt="image" src="https://github.com/user-attachments/assets/31055f9b-1482-4eca-a3b1-db694a52ff97" />


Click **Capture/Forward** repeatedly to follow the packet through the switches.

<img width="1917" height="795" alt="image" src="https://github.com/user-attachments/assets/21489c20-2989-4ac6-8d8c-f5fb62d4f301" />


<img width="1092" height="677" alt="image" src="https://github.com/user-attachments/assets/71ffb41a-d7b7-4974-984e-4ca21b2dfa51" />


<img width="990" height="603" alt="image" src="https://github.com/user-attachments/assets/8083e547-acd8-42cb-808c-bd8dce0d14a9" />


If the **Buffer Full** window appears, click **Clear Event List** to review the recorded events:

<img width="1917" height="761" alt="image" src="https://github.com/user-attachments/assets/847d8471-f0f5-4bf3-ac94-2a841df210fb" />




#### Send a Simple PDU from PC1 to PC4

1. Under the Scenario 0 dropdown, click **New** to create a new scenario.
2. Select **Add Simple PDU**.
3. Click **PC1** as the source, then **PC4** as the destination.
4. Click **Capture/Forward** repeatedly to follow the packet.


<img width="1917" height="942" alt="image" src="https://github.com/user-attachments/assets/9e00eb2a-9960-4c87-a110-a6fbf65c582d" />


<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/76409511-5ba1-40f5-9ad8-832d7ff6d5b5" />


<img width="1917" height="797" alt="image" src="https://github.com/user-attachments/assets/0b95c0fe-c385-4a1a-96cd-57d2d26c6cd7" />


<img width="1033" height="617" alt="image" src="https://github.com/user-attachments/assets/a979923c-4c88-438b-b77b-01d3642af994" />


<img width="1917" height="796" alt="image" src="https://github.com/user-attachments/assets/8e4b234d-e998-40c4-ab07-0d784493c003" />


Now it got success.


If the buffer fills, click **Clear Event List**:

<img width="1917" height="795" alt="image" src="https://github.com/user-attachments/assets/3118cf6c-67db-479e-9b95-3d3fd06e81bc" />


-----



### Part 2: Observe Broadcast Traffic without VLANs

> The following steps erase the switch startup configurations and delete the VLAN database on **S1**, **S2**, and **S3**. Do this only in our Packet Tracer lab. Do not run these commands on a real production switch.

#### Step 1: Clear the configurations on all three switches and delete the VLAN database.


##### Return to Realtime mode

Click **Realtime** before opening the CLI windows.

<img width="1917" height="940" alt="image" src="https://github.com/user-attachments/assets/2799181a-bfc9-4f11-9f25-6783c60c69cc" />


<img width="1917" height="795" alt="image" src="https://github.com/user-attachments/assets/be7ee4bb-fa90-4bfb-9267-bf4ce40a4ead" />


##### Delete the startup configuration

On **S1**, click the **switch**, open its **CLI**, and **Enter**:
````
S1> enable
S1# erase startup-config
````
If prompted to confirm the erase operation, press **Enter**.

**Output**:
````cisco
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
````

> Our switch may display a message that the NVRAM has been erased.


##### Find the VLAN database file
````
S1# dir flash:
````
**Output**:
````cisco
Directory of flash:/

    1  -rw-     4414921           <no date>  c2960-lanbase-mz.122-25.FX.bin
    2  -rw-         796           <no date>  vlan.dat

32514048 bytes total (28098331 bytes free)
````

> the VLAN database file ``vlan.dat``.




##### Delete the VLAN database
````
S1# delete flash:vlan.dat
````
Press `Enter`:

**Output:**

````cisco
Delete filename [vlan.dat]?
Delete flash:/vlan.dat? [confirm]

S1#
````


> This deletes the saved VLAN database. The default **VLAN 1** will remain after the switch reboots.



##### Reload S1
````
S1# reload
````
Then press **Enter**.

And wait until it completed. or press **Enter**.


##### Repeat on S2 and S3

Repeat Steps 2 through 5 on **S2** and **S3**:

| Switch | Erase Startup Config | Delete VLAN Database | Reload |
|---|---|---|---|
| S1 | `erase startup-config` | `delete flash:vlan.dat` | `reload` |
| S2 | `erase startup-config` | `delete flash:vlan.dat` | `reload` |
| S3 | `erase startup-config` | `delete flash:vlan.dat` | `reload` |



On **S2**:
````
Switch> enable
Switch# erase startup-config
Switch# delete flash:vlan.dat
Switch# reload
````

<img width="872" height="773" alt="image" src="https://github.com/user-attachments/assets/2883949b-9b74-4d88-9465-0d0323274aed" />


On **S3**:
````
Switch> enable
Switch# erase startup-config
Switch# delete flash:vlan.dat
Switch# reload
````

<img width="860" height="772" alt="image" src="https://github.com/user-attachments/assets/43a23f93-77da-43dd-be3d-a5bcee90887f" />


#### Step 2: Reload the switches.

After all three switches reboot, click **Fast Forward Time** and wait until the links are green again.

<img width="972" height="620" alt="image" src="https://github.com/user-attachments/assets/59cf2cdf-715d-4e4e-adf1-a3ea18e3d330" />


<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/1f687308-71f8-4946-9231-593b2b70a1f2" />

<img width="1088" height="628" alt="image" src="https://github.com/user-attachments/assets/cff4fa45-4064-4df0-b8fd-1700b96c9297" />



#### Step 3: Click Capture/Forward to send ARP requests and pings.

##### Observe the broadcasts without VLANs

1. Switch to **Simulation** mode.
2. Select **Scenario 0** from the scenario dropdown.
3. Click **Capture/Forward** repeatedly.
4. Observe the ARP requests in the event list and on the topology.



<img width="1917" height="941" alt="image" src="https://github.com/user-attachments/assets/ce718c6a-8842-42c4-9f62-e6fe6bd6565d" />



<img width="1917" height="937" alt="image" src="https://github.com/user-attachments/assets/59788022-4bd1-4a14-9122-7e70dfecb61f" />


<img width="1917" height="940" alt="image" src="https://github.com/user-attachments/assets/63db9776-955f-4eeb-8606-af84be5caf99" />



<img width="956" height="567" alt="image" src="https://github.com/user-attachments/assets/3c7ca9a5-7819-40af-a955-3dc6d93f60f7" />


<img width="933" height="642" alt="image" src="https://github.com/user-attachments/assets/42bd6cbe-3470-4ea2-9715-a1c40375140a" />



<img width="1917" height="792" alt="image" src="https://github.com/user-attachments/assets/57c59d69-5071-496f-8836-87230ee33ebd" />


> Without the previous **VLAN** configuration, the switch ports return to the default **VLAN 1**. The switches now flood Layer 2 broadcasts across the connected switch topology rather than restricting them to the former **VLAN 10**, **VLAN 20**, and **VLAN 30** groups.

> A broadcast is sent out all eligible ports except the port on which it was received. This means devices in the former VLANs can now see broadcasts that previously remained isolated.

> **Note**: Removing VLANs changes Layer 2 broadcast forwarding; it does not change the PCs' IP addresses or create a router. A ping between different IP subnets may still fail if there is no working router or Layer 3 route.


Now we completed lab.

----


### Reflection Questions

1. If a PC in VLAN 10 sends a broadcast message, which devices receive it?

> **Answer**: PC1, PC4, and PC7 belong to VLAN 10. The other VLAN 10 devices receive the broadcast, but the sender does not receive its own transmitted frame.


2. If a PC in VLAN 20 sends a broadcast message, which devices receive it?

> **Answer**: PC2, PC5, and PC8 belong to VLAN 20. The other VLAN 20 devices receive the broadcast, excluding the source.


3. If a PC in VLAN 30 sends a broadcast message, which devices receive it?

> **Answer**: PC3, PC6, and PC9 belong to VLAN 30. The other VLAN 30 devices receive the broadcast, excluding the source.


4. What happens to a frame sent from a PC in VLAN 10 to a PC in VLAN 30?

> **Answer**: The switch does not directly forward the Layer 2 frame from VLAN 10 into VLAN 30. Communication between those VLANs requires inter-VLAN routing through a router or Layer 3 switch.

5. In terms of ports, what are the collision domains on the switch?

> **Answer**: Each switch port is a separate collision domain. A switch does not place every attached device into one shared collision domain.

6. In terms of ports, what are the broadcast domains on the switch?

> **Answer**: With VLANs configured, there are three broadcast domains: VLAN 10, VLAN 20, and VLAN 30. Each VLAN is a separate broadcast domain.

-----
