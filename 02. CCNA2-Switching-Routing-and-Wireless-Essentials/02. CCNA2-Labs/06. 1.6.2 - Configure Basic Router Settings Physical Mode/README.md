<h1 align="center"> 1.6.2 - Configure Basic Router Settings Physical Mode </h1>



---

### Lab Guide:




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

Part 1: Set Up the Topology and Initialize Devices

Part 2: Configure Devices and Verify Connectivity

Part 3: Display Router Information



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


Keep the Server IPv6 address static for now. We will change it to automatic configuration later in Part 3.





























