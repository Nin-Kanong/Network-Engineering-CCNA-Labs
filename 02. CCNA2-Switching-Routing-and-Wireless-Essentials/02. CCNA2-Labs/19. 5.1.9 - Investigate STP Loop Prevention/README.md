<h1 align="center"> LAB: 5.1.9 - Investigate STP Loop Prevention </h1>




---



### Lab Guide:

[5.1.9 Packet Tracer - Investigate STP Loop Prevention.docx](https://github.com/user-attachments/files/35463549/5.1.9.Packet.Tracer.-.Investigate.STP.Loop.Prevention.docx)


---



### Part 1: Observe a Converged Spanning-Tree Instance


#### Step 1: Verify Connectivity

First in this click on **PC2** -> **Desktop** -> **Command Prompt**:

```cmd
ipconfig
```  
**Output:**
```cmd
FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Link-local IPv6 Address.........: FE80::260:2FFF:FE2B:6952
   IPv6 Address....................: ::
   IPv4 Address....................: 192.168.1.101
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     0.0.0.0
```



Then click **PC1** -> Select the **Desktop** tab -> Open **Command Prompt**:
```
ping 192.168.1.101
```
**Output:**

```cmd
Pinging 192.168.1.101 with 32 bytes of data:

Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.101:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

---


#### Step 2: View spanning-tree status on each switch.


In this first click on **S1** -> **CLI**, then press **Enter**:
````
S1> enable
S1# show spanning-tree vlan 1
````
**Output:**
````cmd
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Gi0/1            Desg FWD 4         128.25   P2p
Gi0/2            Root FWD 4         128.26   P2p
Fa0/1            Desg FWD 19        128.1    P2p
````



Then repeat it all Switch.

---



### Part 2: Observe spanning-tree convergence

#### Step 1: Remove the connection between S1 and S2.

In this click on **S3** -> **CLI**, then press **Enter**:

````
S3> enable
S3# show spanning-tree vlan 1
````

**Output:**
````
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Gi0/2            Altn BLK 4         128.26   P2p
Gi0/1            Root FWD 4         128.25   P2p
````


So in this it loop switch.

And we need to remove cable from **S1** to **S2**.


In this first click button **Delete**, then click on cable from **S1** to **S2**:

<img width="1917" height="895" alt="image" src="https://github.com/user-attachments/assets/a9a191b6-15b6-4808-9931-f07bf0991d23" />


<img width="1162" height="676" alt="image" src="https://github.com/user-attachments/assets/b9cbd354-92ee-49ff-ae9b-6e446f36e1b3" />


<img width="915" height="532" alt="image" src="https://github.com/user-attachments/assets/f3742c0a-cc8e-47fd-bba5-ef5f7fe5c90c" />


Now it ready deleted.


---


#### Step 2: Observe spanning-tree convergence.

In this back to our **S3**:

````
S3# show spanning-tree vlan 1
````
**Output:**

````
VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     0001.6448.C6E7
             Cost        4
             Port        25(GigabitEthernet0/1)
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     000C.CF45.7534
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Gi0/2            Desg FWD 4         128.26   P2p
Gi0/1            Root FWD 4         128.25   P2p
````

Now we got successful.

---


Then test it.

Just click on **PC1** -> Select **Desktop** -> **Command Prompt**, then enter:
````cmd
ping 192.168.1.101
````
**Output:**

````
Pinging 192.168.1.101 with 32 bytes of data:

Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128
Reply from 192.168.1.101: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.101:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
````

Now we completed the lab.

------      
