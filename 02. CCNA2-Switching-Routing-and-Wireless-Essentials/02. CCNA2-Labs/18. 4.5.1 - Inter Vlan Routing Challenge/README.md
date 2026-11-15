<h1 align="center"> Inter Vlan Routing Challenge </h1>



---


### Lab Guide



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




























