<h1 align="center"> Auto-MDIX - Cisco Switch Cheat Sheet </h1>


**Auto-MDIX (Automatic Medium-Dependent Interface Crossover)** automatically detects whether a Straight-through or Crossover cable is needed.

## **1. Configuration Commands**

| Command              | Function                        |
| -------------------- | ------------------------------- |
| `enable`             | Enter privileged EXEC mode      |
| `configure terminal` | Enter global configuration mode |
| `interface fa0/1`    | Select switch port              |
| `mdix auto`          | Enable Auto-MDIX                |
| `no mdix auto`       | Disable Auto-MDIX               |
| `speed auto`         | Automatically negotiate speed   |
| `duplex auto`        | Automatically negotiate duplex  |
| `no shutdown`        | Enable the interface            |
| `exit`               | Exit current configuration mode |
| `end`                | Return to privileged EXEC mode  |

## **2. Enable Auto-MDIX**

```
enable
configure terminal
interface fa0/1
speed auto
duplex auto
mdix auto
no shutdown
end
```

## **3. Disable Auto-MDIX**

```
enable
configure terminal
interface fa0/1
no mdix auto
end
```

## **4. Verification Commands**

| Command                                                           | Function                        |
| ----------------------------------------------------------------- | ------------------------------- |
| `show controllers ethernet-controller fa0/1 phy`                  | Check Auto-MDIX information     |
| `show controllers ethernet-controller fa0/1 phy \\| include MDIX` | Display only MDIX information   |
| `show interfaces fa0/1 status`                                    | Check port status               |
| `show interfaces fa0/1`                                           | Check interface details         |
| `show running-config interface fa0/1`                             | Check interface configuration   |
| `show running-config`                                             | View full running configuration |

**Expected output:**

```
Auto-MDIX : On
```



``On`` = Enabled

``Off`` = Disabled



## **5. Configure Multiple Switch Ports**

You can enable Auto-MDIX on multiple ports at once.

```
enable
configure terminal
interface range fa0/1- fa0/5
speed auto
duplex auto
mdix auto
no shutdown
end
```

This configures ports FastEthernet 0/1 through 0/5.

## **6. Ethernet Cable Types**

<img width="550" height="468" alt="image" src="https://github.com/user-attachments/assets/0d6c52d9-77b7-4e63-b770-b221dc45fe82" />


**Straight-through**

Traditionally used for different device types.

<img width="1200" height="895" alt="image" src="https://github.com/user-attachments/assets/c59cf490-c743-4b70-be9e-47719dd339eb" />


**Crossover**

Traditionally used for similar device types.

| Connection      | Traditional Cable |
| --------------- | ----------------- |
| PC ↔ Switch     | Straight-through  |
| Server ↔ Switch | Straight-through  |
| Router ↔ Switch | Straight-through  |
| Switch ↔ Switch | Crossover         |
| PC ↔ PC         | Crossover         |

With Auto-MDIX enabled, either cable type can be used.

## **7. Troubleshooting**

| Problem                 | Solution                               |
| ----------------------- | -------------------------------------- |
| Wrong cable type        | Enable `mdix auto`                     |
| Auto-MDIX not working   | Check `speed auto`                     |
| Duplex mismatch         | Configure `duplex auto`                |
| Port is disabled        | Use `no shutdown`                      |
| Cannot verify Auto-MDIX | Check switch model and command support |


**Most important commands to memorize**

```
interface fa0/1
speed auto
duplex auto
mdix auto
```

**Remember:** Auto-MDIX = Automatically detects and adjusts the Ethernet cable connection.
