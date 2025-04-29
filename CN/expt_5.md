
# EXP-5 Dynamic Routing using RIP v1

🎯 **AIM:**  
To establish communication between six PCs connected via three routers by configuring IP addressing and routing, and verifying successful packet transmission.

📚 **DESCRIPTION:**

Dynamic routing is a networking technique where routers automatically learn and maintain routing information using routing protocols.  
It enables routers to adapt to network changes, such as link failures or topology updates, without manual intervention.

---

### RIP Overview:

**Routing Information Protocol (RIP)** is a distance-vector routing protocol used in small to medium-sized networks.

#### RIP Version 1 (RIP v1)
- **Classful Routing**: Does not support subnetting (no subnet mask in updates).
- **Broadcast Updates**: Sent every 30 seconds (broadcast address 255.255.255.255).
- **No Authentication**: RIP v1 does not support authentication.
- **Supports Only IPv4**: No support for IPv6.

#### RIP Version 2 (RIP v2)
- **Classless Routing**: Supports VLSM (includes subnet mask).
- **Multicast Updates**: Sent to 224.0.0.9 (reduces congestion).
- **Authentication Support**: Supports MD5/plain-text authentication.
- **Route Tagging**: Allows distinguishing routes.
- **Supports Only IPv4**: (For IPv6, RIPng is used.)

---

🛠 **CONFIGURATION STEPS:**

### 1. Connect the Devices
- Connect PC0 and PC1 to Switch0.
- Connect PC2 and PC3 to Switch1.
- Connect PC4 and PC5 to Switch2.
- Connect Switch0 to Router0, Switch1 to Router1, and Switch2 to Router2.
- Connect Router0 to Router1 using Serial link.
- Connect Router1 to Router2 using Serial link.

---

### 2. Assign IP Addresses to PCs

| PC | IP Address | Subnet Mask | Default Gateway |
|:--|:------------|:------------|:----------------|
| PC0 | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC1 | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |
| PC2 | 192.168.3.2 | 255.255.255.0 | 192.168.3.1 |
| PC3 | 192.168.3.3 | 255.255.255.0 | 192.168.3.1 |
| PC4 | 192.168.5.2 | 255.255.255.0 | 192.168.5.1 |
| PC5 | 192.168.5.3 | 255.255.255.0 | 192.168.5.1 |

---

### 3. Assign IP Addresses to Routers

| Router | Interface | IP Address | Connected To |
|:------|:----------|:-----------|:-------------|
| Router0 | FastEthernet 0/0 | 192.168.1.1 | Switch0 |
| Router0 | Serial 2/0 | 192.168.2.1 | Router1 |
| Router1 | Serial 2/0 | 192.168.2.2 | Router0 |
| Router1 | FastEthernet 0/0 | 192.168.3.1 | Switch1 |
| Router1 | Serial 3/0 | 192.168.4.2 | Router2 |
| Router2 | Serial 2/0 | 192.168.4.1 | Router1 |
| Router2 | FastEthernet 0/0 | 192.168.5.1 | Switch2 |

---

### 4. Enable Routing (RIP v1) on Routers

**Router0 Configuration:**
```bash
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 1
Router(config-router)# network 192.168.1.0
Router(config-router)# network 192.168.2.0
Router(config-router)# exit
Router(config)# exit
```

**Router1 Configuration:**
```bash
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 1
Router(config-router)# network 192.168.2.0
Router(config-router)# network 192.168.3.0
Router(config-router)# network 192.168.4.0
Router(config-router)# exit
Router(config)# exit
```

**Router2 Configuration:**
```bash
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 1
Router(config-router)# network 192.168.4.0
Router(config-router)# network 192.168.5.0
Router(config-router)# exit
Router(config)# exit
```

---

### 5. Activate Router Interfaces

For each router interface:
```bash
Router(config)# interface FastEthernet 0/0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface Serial 2/0
Router(config-if)# no shutdown
Router(config-if)# exit
```
(Do the same for Serial 3/0 where needed.)

---

### 6. Verify Routing Table

Use the following command:
```bash
Router# show ip route
```
✅ Check if all networks (192.168.1.0, 192.168.2.0, 192.168.3.0, 192.168.4.0, 192.168.5.0) are visible in each router's routing table.

---

📷 **OUTPUT:**
_(Add screenshots of successful pings or routing tables here.)_

---

✅ **RESULT:**  
Thus, the experiment successfully establishes communication between six PCs through three interconnected routers that use dynamic routing (RIP v1).

```