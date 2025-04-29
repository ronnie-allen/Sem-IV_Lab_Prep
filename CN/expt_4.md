
# EXP-4 Static Routing (Updated for Serial Topology)

🎯 **AIM:**  
To establish communication between two PCs connected via two routers by configuring IP addressing and static routing, and verifying successful packet transmission.

📚 **DESCRIPTION:**

In this setup:

- PC4 is connected to **Router0**.
- PC5 is connected to **Router1**.
- The routers are connected through **Serial interfaces** (`Se0/0` and `Se2/0`).

🧠 **What Are We Doing?**
- Assign correct IPs to PCs and routers.
- Configure static routes on each router.
- Ensure PCs can ping each other through the routers.

🎯 **Why We Are Doing This:**

| Without Static Routing | With Static Routing |
|:----------------------|:---------------------|
| Routers don't know how to forward packets. ❌ | Routers forward packets correctly. ✅ |

---

🔵 **Step-by-Step Configuration (According to Your Topology)**

## 1. Connect the Devices
- PC4 → Router0 (FastEthernet0/0)
- PC5 → Router1 (FastEthernet0/0)
- Router0 ↔ Router1 (Serial0/0 on Router0 to Serial2/0 on Router1)

## 2. Assign IP Addresses

| Device | Interface | IP Address | Subnet Mask |
|:-------|:----------|:-----------|:------------|
| PC4 | NIC | 192.168.1.2 | 255.255.255.0 |
| Router0 | Fa0/0 | 192.168.1.1 | 255.255.255.0 |
| Router0 | Se0/0 | 192.168.2.1 | 255.255.255.0 |
| Router1 | Se2/0 | 192.168.2.2 | 255.255.255.0 |
| Router1 | Fa0/0 | 192.168.3.1 | 255.255.255.0 |
| PC5 | NIC | 192.168.3.2 | 255.255.255.0 |

Default Gateways:
- PC4 ➔ `192.168.1.1`
- PC5 ➔ `192.168.3.1`

---

## 3. Router Configurations

**Router0 (Left Router) Configuration:**
```bash
Router> enable
Router# configure terminal
Router(config)# interface fastethernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config)# interface serial 0/0
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# clock rate 64000
Router(config-if)# no shutdown
Router(config-if)# exit
```

**Router1 (Right Router) Configuration:**
```bash
Router> enable
Router# configure terminal
Router(config)# interface fastethernet 0/0
Router(config-if)# ip address 192.168.3.1 255.255.255.0
Router(config-if)# no shutdown
Router(config)# interface serial 2/0
Router(config-if)# ip address 192.168.2.2 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

✅ **Note:** Clock rate must be set on DCE side (usually Router0).

---

## 4. Configure Static Routes

**Router0:**
```bash
Router0(config)# ip route 192.168.3.0 255.255.255.0 192.168.2.2
```

**Router1:**
```bash
Router1(config)# ip route 192.168.1.0 255.255.255.0 192.168.2.1
```

---

## 5. Verify Setup

✨ **Useful Commands:**
| Command | Purpose |
|:--------|:--------|
| show ip route | View the routing table |
| show running-config | View current configuration |
| ping [IP Address] | Test connectivity |
| show ip interface brief | View all interfaces and their status |

🛜 **Testing:**
- Ping from Router0 to Router1.
- Ping from PC4 to Router0.
- Ping from PC5 to Router1.
- **Ping PC5 (192.168.3.2) from PC4 (192.168.1.2)**.

---

📦 **Components Required (Packet Tracer)**

| Component | Quantity | Notes |
|:---------|:---------|:------|
| Router | 2 | Example: Router-PT |
| PC | 2 | |
| Serial DCE Cable | 1 | Between routers |
| Copper Straight-through Cable | 2 | PC-to-Router connections |

---

✅ **RESULT:**  
Thus, the communication between two PCs through two interconnected routers using static routing was successfully achieved according to the updated topology.


---
