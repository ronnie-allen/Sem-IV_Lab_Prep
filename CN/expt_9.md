
# 📄 EXP9.md — Configuration of RIPng (IPv6 Dynamic Routing)

---
## Topology
> Topology for Configuration of RIPng

### ![Topology](./assets/IPV6%20exp9.png)

## 1. Key Concepts (Simple Definitions)

- **RIPng (Routing Information Protocol Next Generation)**: A dynamic routing protocol that supports IPv6. It lets routers share routing information automatically.
- **IPv6**: The latest version of IP addresses (128 bits), used for more devices and better routing.
- **Router**: A device that connects networks and decides the best path for sending data.
- **Gigabit Ethernet**: A fast cable connection used between routers and other devices.

---

## 2. Step-by-Step Configuration in Cisco Packet Tracer

---

### 🖧 Topology Setup
- **Router3** connected to:
  - PC0 via Switch0 through `Gig0/1`
  - Router4 via `Gig0/0`

- **Router4** connected to:
  - PC1 via Switch1 through `Gig0/1`
  - Router3 via `Gig0/0`

---

### 🔧 Step 1: Enable IPv6 Routing on Both Routers

```bash
Router(config)# ipv6 unicast-routing
```

---

### 🌐 Step 2: Assign IPv6 Addresses

#### Router3:
```bash
Router(config)# interface gig0/1
Router(config-if)# ipv6 address 2001:1::1/64
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface gig0/0
Router(config-if)# ipv6 address 2001:2::1/64
Router(config-if)# no shutdown
Router(config-if)# exit
```

#### Router4:
```bash
Router(config)# interface gig0/0
Router(config-if)# ipv6 address 2001:2::2/64
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface gig0/1
Router(config-if)# ipv6 address 2001:3::1/64
Router(config-if)# no shutdown
Router(config-if)# exit
```

---

### 🔄 Step 3: Configure RIPng on Both Routers

#### Start RIPng:
```bash
Router(config)# ipv6 router rip cisco
Router(config-router)# exit
```

#### Enable RIPng on Interfaces:

```bash
Router(config)# interface gig0/0
Router(config-if)# ipv6 rip cisco enable
Router(config-if)# exit

Router(config)# interface gig0/1
Router(config-if)# ipv6 rip cisco enable
Router(config-if)# exit
```

---

### ✅ Step 4: Test the Connection

- Ping from **PC0 to PC1** using IPv6 address (e.g., `ping 2001:3::1`)
- Use `show ipv6 route` on routers to confirm route propagation.

---

## 3. Practical Analogy

📦 **Think of RIPng like a delivery service**:
- Each router is a post office.
- They talk to each other and share updated routes.
- If a road (network) changes, they notify each other and re-route the mail (data).

---

## 4. Cheatsheet Table

| Key Term           | Definition                          | Function/Importance                   | Example              |
|--------------------|-------------------------------------|----------------------------------------|----------------------|
| RIPng              | Routing protocol for IPv6           | Shares routes dynamically              | `ipv6 router rip`    |
| ipv6 unicast-routing | Enables IPv6 on router             | Required for IPv6 to work              | Cisco CLI            |
| ipv6 address       | 128-bit unique device address       | Identifies each device                 | `2001:2::1/64`       |
| ipv6 rip enable    | Starts RIPng on interface           | Allows route updates on that port      | `ipv6 rip cisco enable` |
| show ipv6 route    | Displays IPv6 routing table         | Verify routing configuration           | Cisco CLI            |

---

## ✅ Conclusion

This experiment demonstrates how **RIPng allows IPv6 routers to learn and share routes automatically**, making network communication efficient and dynamic.

