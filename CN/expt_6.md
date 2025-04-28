
# 💥 Exp-6 Configuration, testing and troubleshooting of Dynamic routing protocols - OSPF

---

## AIM:  
- Configure a WAN with serial connections.
- Enable OSPF to communicate between two PCs.

---

## ⚙ Devices Needed:
- **3 Routers** (Router0, Router1, Router2)
- **2 PCs** (PC0, PC1)
- **Serial cables** and **copper straight-through cables**

---

## 🛠 Step 1: Connect the Devices
- PC0 → Router0 (FastEthernet0/0) ➡️ using **copper straight-through** cable.
- Router0 (Serial2/0) → Router1 (Serial2/0) ➡️ using **serial DCE cable**.
- Router1 (Serial3/0) → Router2 (Serial2/0) ➡️ using **serial DCE cable**.
- Router2 (FastEthernet0/0) → PC1 ➡️ using **copper straight-through** cable.

---

## 🛠 Step 2: Configure IP Addressing on PCs

### On PC0:
1. Click PC0 ➔ Desktop ➔ IP Configuration:
   - IP Address: `192.168.1.2`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: `192.168.1.1`

### On PC1:
1. Click PC1 ➔ Desktop ➔ IP Configuration:
   - IP Address: `192.168.4.2`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: `192.168.4.1`

---

## 🛠 Step 3: Configure Router Interfaces

> Go to each router CLI and type these commands:

### Router0:
```bash
enable
configure terminal
interface FastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit
interface Serial2/0
 ip address 10.1.1.1 255.255.255.252
 clock rate 64000
 no shutdown
exit
```

### Router1:
```bash
enable
configure terminal
interface Serial2/0
 ip address 10.1.1.2 255.255.255.252
 no shutdown
exit
interface Serial3/0
 ip address 10.1.2.1 255.255.255.252
 no shutdown
exit
```

### Router2:
```bash
enable
configure terminal
interface FastEthernet0/0
 ip address 192.168.4.1 255.255.255.0
 no shutdown
exit
interface Serial2/0
 ip address 10.1.2.2 255.255.255.252
 clock rate 64000
 no shutdown
exit
```

---

## 🛠 Step 4: Configure OSPF Routing on All Routers

### Router0:
```bash
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.1.1.0 0.0.0.3 area 0
exit
```

### Router1:
```bash
router ospf 1
 network 10.1.1.0 0.0.0.3 area 0
 network 10.1.2.0 0.0.0.3 area 0
exit
```

### Router2:
```bash
router ospf 1
 network 192.168.4.0 0.0.0.255 area 0
 network 10.1.2.0 0.0.0.3 area 0
exit
```

---

## 🛠 Step 5: Verify OSPF Status

> On all routers, type:

```bash
show ip ospf neighbor
```
✅ If everything's fine, you should see your neighbors listed.

---

## 🛠 Step 6: Test the Network
1. Go to PC0 ➔ Desktop ➔ Command Prompt:
   - Type: `ping 192.168.4.2`
   
✅ You should get successful replies!

---

## 🎯 OUTPUT Expected:
- **OSPF neighbors formed** between routers.
- **PC0 and PC1 can ping each other**.
- **Dynamic routing working automatically** (no need for static routes).

---

## 📜 RESULT:
You have successfully configured and tested OSPF dynamic routing across multiple routers in a WAN setup, enabling communication between two remote PCs. 🔥

---