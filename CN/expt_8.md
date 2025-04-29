# 📄 EXP8.md — Simulation of LAN using IPv6

---

## 1. Key Concepts (Simple Definitions)

- **LAN (Local Area Network)**: A group of devices connected in a limited area like a home, school, or office.
- **IPv6**: The latest version of IP addressing with longer addresses (128 bits) compared to IPv4 (32 bits). Example: `2001:1::1`
- **Unicast Routing**: Sending data from one device directly to another.
- **Router**: A device that connects different networks and forwards data.
- **Switch**: A device that connects multiple devices within the same network.

---

## 2. Step-by-Step Configuration Using Cisco Packet Tracer

### 🖧 Network Topology:
- PC0 → Switch0 → Router0 (Gig0/0)
- PC1 → Switch1 → Router0 (Gig0/1)

---

### 🔧 Step 1: Connect the Devices
- Use **Copper Straight-Through cables** to connect:
  - PC0 to Switch0
  - Switch0 to Router0 (GigabitEthernet0/0)
  - PC1 to Switch1
  - Switch1 to Router0 (GigabitEthernet0/1)

---

### 🌐 Step 2: Assign IPv6 Addresses to PCs

- **PC0:**
  - IPv6 Address: `2001:1::2/64`
  - Default Gateway: `2001:1::1`

- **PC1:**
  - IPv6 Address: `2001:2::2/64`
  - Default Gateway: `2001:2::1`

---

### 🚦 Step 3: Configure IPv6 on Router Interfaces

```bash
Router> en
Router# configure t
Router(config)# ipv6 unicast-routing

Router(config)# interface GigabitEthernet0/0
Router(config-if)# ipv6 address 2001:1::1/64
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface GigabitEthernet0/1
Router(config-if)# ipv6 address 2001:2::1/64
Router(config-if)# no sh
Router(config-if)# exit
```

---

### ✅ Step 4: Test Connectivity

- From **PC0**, ping `2001:2::2`
- From **PC1**, ping `2001:1::2`
- If ping succeeds, IPv6 LAN is working!

---

## 3. Practical Analogy

🧠 Think of **IPv6 LAN** like a **neighborhood with smart homes**:
- Each house (PC) has a long, unique address.
- The router is the **mail sorter**, knowing which letter (data) goes where.
- Unicast is like sending a letter **directly** to one house instead of the whole block.

---

## 4. Cheatsheet Table

| Key Term             | Definition                                   | Importance/Function                        | Example           |
|----------------------|----------------------------------------------|---------------------------------------------|-------------------|
| IPv6 Address          | 128-bit address format                      | More devices, better security               | 2001:1::2         |
| LAN                   | Local device network                        | Enables local communication                 | Home/Office setup |
| Unicast Routing       | One-to-one communication                    | Direct communication                        | Router to PC      |
| ipv6 unicast-routing  | Enables IPv6 on router                      | Required to route IPv6 traffic              | Cisco CLI         |
| ping (IPv6)           | Tests IPv6 connection                       | Verifies connectivity                       | `ping 2001:2::2`  |

---

## ✅ Conclusion

This experiment shows how to **set up a basic LAN using IPv6**.  
After configuration, the devices can successfully communicate using their unique IPv6 addresses.