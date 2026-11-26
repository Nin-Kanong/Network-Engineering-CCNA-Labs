<h1 align="center"> 5.1.9 - Investigate STP Loop Prevention </h1>




---



### Lab Guide:



---



### Part 1: Observe a Converged Spanning-Tree Instance


#### Step 1: Verify Connectivity

First in this click on **PC2** -> **Desktop** -> **Command Prompt**:

```cmd
ipconfig
```  
**Output:**
```
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
````
Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Gi0/1            Desg FWD 4         128.25   P2p
Gi0/2            Root FWD 4         128.26   P2p
Fa0/1            Desg FWD 19        128.1    P2p
````



























































