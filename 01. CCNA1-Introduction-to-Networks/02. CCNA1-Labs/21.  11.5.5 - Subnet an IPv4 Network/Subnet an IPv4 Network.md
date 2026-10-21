<h1 align="center"> Lab11.5.5 - Subnet an IPv4 Network </h1>


---

## Lab Guide:
[11.5.5 Packet Tracer - Subnet an IPv4 Network.docx](https://github.com/user-attachments/files/29248058/11.5.5.Packet.Tracer.-.Subnet.an.IPv4.Network.docx)


## Lab
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/fd567cd2-04f9-45a4-81f6-3d54f5604ebb" />



### Config Router

Click on `CustomRouter`:

<img width="767" height="377" alt="image" src="https://github.com/user-attachments/assets/6ca9a032-072b-4c78-bcae-0bd196211071" />


After just press `Enter`:
<img width="871" height="882" alt="image" src="https://github.com/user-attachments/assets/97024874-b5f0-459a-908b-c94a81c526ad" />




````
en
conf t
enable secret Class123
line console 0
password Cisco123
login
exit
hostname CustomerRouter
int g0/0
ip add 192.168.0.1 255.255.255.192
no shut
int g0/1
ip add 192.168.0.65 255.255.255.192
no shut
exit
exit
copy run start
````
<img width="1111" height="979" alt="image" src="https://github.com/user-attachments/assets/5af9ef41-bb8b-4938-b5f5-1bb4e592ea91" />

Now we complete to config on router.

---


### Config LAN-A (Switch)
Click `LAN-A`:
<img width="933" height="412" alt="image" src="https://github.com/user-attachments/assets/74e87aeb-41f4-4546-865b-194d112ec07d" />

<img width="871" height="886" alt="image" src="https://github.com/user-attachments/assets/99b74d6c-94cd-4f54-a3dd-33e3fdd2b542" />

````
en
conf t
interface vla 1
ip address 192.168.0.2 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.1
exit
copy running-config startup-config
````
<img width="877" height="886" alt="image" src="https://github.com/user-attachments/assets/24540d41-fd8e-4929-857e-321cdb9effe8" />


---


### Config on LAN-B
<img width="897" height="431" alt="image" src="https://github.com/user-attachments/assets/ccca36c0-9b7b-431e-80c1-932377c4ee88" />


<img width="875" height="883" alt="image" src="https://github.com/user-attachments/assets/8a5b443e-4b5d-4c39-a164-ae32135e67fa" />


````
en
conf t
interface vlan 1
ip address 192.168.0.66 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.65
exit
copy running-config startup-config
````
<img width="872" height="885" alt="image" src="https://github.com/user-attachments/assets/a587f709-06b8-4f28-bb79-f3e21e3eba21" />

---




### Set static IP on PC-A
<img width="827" height="360" alt="image" src="https://github.com/user-attachments/assets/5a79b515-6805-41c4-87d8-4a3b63620b64" />

<img width="875" height="885" alt="image" src="https://github.com/user-attachments/assets/82eeb11b-ca83-48ef-bcc0-654bc7aa77b5" />

<img width="867" height="720" alt="image" src="https://github.com/user-attachments/assets/af173e4c-82e0-43cf-940d-a66c99558e4e" />



### Set Static IP on PC-B

<img width="922" height="422" alt="image" src="https://github.com/user-attachments/assets/845db97c-b658-40db-860f-22cecea0218b" />

<img width="863" height="887" alt="image" src="https://github.com/user-attachments/assets/084ee7ac-51d9-48dc-a227-a375b62a6ef9" />

<img width="874" height="722" alt="image" src="https://github.com/user-attachments/assets/9e8de686-187e-4e75-98e1-370e8d9bab4a" />


Now we finished our lab.

---


### Check Result:
<img width="1006" height="1079" alt="image" src="https://github.com/user-attachments/assets/810919f3-4412-4699-a34f-55368058b68a" />


Now we got full score:


<img width="652" height="513" alt="image" src="https://github.com/user-attachments/assets/89ef22a0-0712-4206-a9e3-a19eed5fd5e8" />


---
