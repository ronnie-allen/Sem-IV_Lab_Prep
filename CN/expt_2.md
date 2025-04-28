# Ex 2: Basic Network Setup with DHCP, DNS, and Web Server

## Aim:
To set up a basic computer network in Cisco Packet Tracer using DHCP, DNS, and Web Server functionalities, ensuring automated IP address assignment and domain name resolution.

---

## Description:
In this exercise, we will cover the following important networking concepts:

1. **Switch**:  
   - A network device that connects multiple devices like PCs and servers within the same network, allowing them to communicate efficiently.

2. **PC (Personal Computer)**:  
   - End-user devices that connect to the network to access resources like websites or shared files.

3. **Server**:  
   - A powerful machine that provides services to client computers, such as managing IP addresses (DHCP), translating domain names (DNS), or hosting web content (Web Server).

4. **DHCP Server**:  
   - Automatically assigns IP addresses to PCs, reducing the need for manual IP configuration and avoiding conflicts.

5. **DNS Server**:  
   - Converts user-friendly domain names like `karunya.com` into IP addresses so computers can locate each other over the network.

6. **Web Server**:  
   - Hosts websites that users can access through their web browsers.

7. **IP Addressing**:  
   - Every device in the network must have a unique IP address to communicate. Proper subnet masks and gateways must be configured.

---

## Steps for Implementation:

---

### 1. Network Topology

![Network Topology](./246b38fc-16de-4a32-8b9c-4ee0b7769a9b.png)

---

### 2. Device List and IP Addressing Table

| Device             | IP Address      | Subnet Mask       | Default Gateway  |
|--------------------|-----------------|-------------------|------------------|
| PC0                | 192.168.1.11     | 255.255.255.0     | 192.168.1.3      |
| PC1                | 192.168.1.12     | 255.255.255.0     | 192.168.1.3      |
| DHCP Server        | 192.168.1.2      | 255.255.255.0     | 192.168.1.1      |
| DNS Server         | 192.168.1.3      | 255.255.255.0     | 192.168.1.1      |
| Karunya Web Server | 192.168.1.10     | 255.255.255.0     | 192.168.1.3      |

---

### 3. Network Setup (Cisco Packet Tracer)

1. Open **Cisco Packet Tracer**.
2. Add the following devices:
   - **2 PCs** (PC0, PC1)
   - **1 Switch** (Switch0)
   - **3 Servers** (DHCP Server, DNS Server, Karunya Web Server)
3. Connect all devices to the switch using **Copper Straight-Through Cables**.

---

### 4. Server Configuration

---

#### 4.1 DHCP Server Configuration

- Go to the **Desktop** tab → Open **IP Configuration**.
  - IP Address: 192.168.1.2
  - Subnet Mask: 255.255.255.0
  - Default Gateway: 192.168.1.1
  - DNS Server: 192.168.1.3
- Go to the **Services** tab → Select **DHCP**.
- Configure DHCP settings:
  - Pool Name: (Example) `pool1`
  - Default Gateway: 192.168.1.1
  - Start IP Address: 192.168.1.10
  - Subnet Mask: 255.255.255.0
  - DNS Server: 192.168.1.3
- Turn the DHCP Service **ON**.

---

#### 4.2 DNS Server Configuration

- Go to the **Desktop** tab → Open **IP Configuration**.
  - IP Address: 192.168.1.3
  - Subnet Mask: 255.255.255.0
  - Default Gateway: 192.168.1.1
- Go to the **Services** tab → Select **DNS**.
- Turn the DNS Service **ON**.
- Add a DNS Record:
  - Name: `karunya.com`
  - Address: 192.168.1.3
- Click **Save**.

##### To check Dhcp server
- Go to the **Desktop** tab → Open **IP Configuration**.
    - select DHCP ( For dynamic ip addressing through dhcp server)

---

#### 4.3 Web Server Configuration

- Go to the **Desktop** tab → Open **IP Configuration**.
    - select DHCP ( For dynamic ip addressing through dhcp server)

---

### 5. Testing the Setup

---

#### 5.1 Testing with Ping

- On **PC0**:
  - Open **Command Prompt** → Type: `ping 192.168.1.10` (Testing Web Server connectivity).
- Similarly, ping:
  - `192.168.1.2` (DHCP Server)
  - `192.168.1.3` (DNS Server)
- Repeat the steps on **PC1**.

---

#### 5.2 Testing with Web Browser

- On **PC0**:
  - Open **Web Browser** → In the address bar, type: `http://karunya.com`
- If setup is correct, the web page hosted on the Karunya Web Server should display.
- Repeat the same on **PC1**.

---

## Conclusion:
You have successfully configured a basic network setup with DHCP, DNS, and Web Server in Cisco Packet Tracer, ensuring automatic IP address assignment and domain name resolution.

---

✅ **Congratulations! Your network is live and working!**

---