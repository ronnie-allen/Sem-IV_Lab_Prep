Yes! ✅  
# 📄 EXP1.md - Network Troubleshooting Commands
---

# Network Troubleshooting Commands

---

## Key Concepts (Simple Definitions)

Network troubleshooting means using simple commands to find and fix problems with your network connection — just like using basic tools to fix a car.

---

## Step-by-Step Commands with Sample Outputs

---

### 1. `ipconfig`
**Shows** basic IP address, subnet mask, and gateway.

```bash
C:\> ipconfig

Ethernet adapter Ethernet:

   IPv4 Address. . . . . . . . . . . : 192.168.1.2
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

---

### 2. `ipconfig /all`
**Shows** detailed network information.

```bash
C:\> ipconfig /all

Host Name . . . . . . . . . . . . : Laptop
Physical Address. . . . . . . . . : 00-14-22-01-23-45
DHCP Enabled. . . . . . . . . . . : Yes
IPv4 Address. . . . . . . . . . . : 192.168.1.2
DNS Servers . . . . . . . . . . . : 8.8.8.8
```

---

### 3. `hostname`
**Shows** your computer's name.

```bash
C:\> hostname

Laptop-PC
```

---

### 4. `cls`
**Clears** the screen.

(No output — screen gets cleared)

---

### 5. `ipconfig /displaydns`
**Shows** cached websites visited recently.

```bash
C:\> ipconfig /displaydns

Record Name . . . . . : www.google.com
Record Type . . . . . : 1
Data Length . . . . . : 4
Section . . . . . . . : Answer
```

---

### 6. `ipconfig /flushdns`
**Clears** the DNS cache.

```bash
C:\> ipconfig /flushdns

Successfully flushed the DNS Resolver Cache.
```

---

### 7. `getmac`
**Shows** MAC address.

```bash
C:\> getmac

Physical Address    Transport Name
=================== ==========================================================
00-14-22-01-23-45   \Device\Tcpip_{...}
```

---

### 8. `arp -a`
**Shows** IP-to-MAC mappings.

```bash
C:\> arp -a

Internet Address      Physical Address      Type
192.168.1.1            00-14-22-01-23-45     dynamic
```

---

### 9. `ping www.google.com`
**Tests** if you can reach Google.

```bash
C:\> ping www.google.com

Reply from 142.250.180.68: bytes=32 time=20ms TTL=118
```

---

### 10. `ping -n 10 www.google.com`
**Sends 10 pings** instead of 4.

```bash
C:\> ping -n 10 www.google.com

Ping statistics for 142.250.180.68:
    Packets: Sent = 10, Received = 10, Lost = 0 (0% loss)
```

---

### 11. `ping -l 64 www.google.com`
**Sends ping** with 64 bytes payload.

```bash
C:\> ping -l 64 www.google.com

Reply from 142.250.180.68: bytes=64 time=22ms TTL=118
```

---

### 12. `tracert www.google.com`
**Traces** the path to Google.

```bash
C:\> tracert www.google.com

 1     1 ms    1 ms    1 ms  192.168.1.1
 2    10 ms   11 ms   10 ms  ISP-Gateway
 3    20 ms   22 ms   21 ms  Google-Server
```

---

### 13. `pathping www.google.com`
**Shows** delay and packet loss at each hop.

```bash
C:\> pathping www.google.com

Computing statistics for 50 seconds...
Hop 0: Laptop-PC
Hop 1: 192.168.1.1
Hop 2: ISP Gateway
Hop 3: google.com
```

---

### 14. `netstat`
**Shows** current network connections.

```bash
C:\> netstat

Proto  Local Address          Foreign Address        State
TCP    192.168.1.2:50123       142.250.180.68:443      ESTABLISHED
```

---

### 15. `nslookup www.google.com`
**Finds** IP address of a domain.

```bash
C:\> nslookup www.google.com

Server:  dns.google
Address:  8.8.8.8

Non-authoritative answer:
Name:    www.google.com
Address: 142.250.180.68
```

---

### 16. `net user`
**Shows** all user accounts.

```bash
C:\> net user

User accounts for \\Laptop-PC

------------------------------------------------------
Administrator    Guest    User1
```

---

### 17. `ping -i 2 www.google.com`
**Sets TTL** (Time to Live) to 2 hops.

```bash
C:\> ping -i 2 www.google.com

TTL expired in transit.
```

---

## Practical Example (Analogy)

- **ipconfig** = Checking your home address (where you are)
- **ping** = Sending a letter to check if someone is home
- **tracert** = Tracking how the letter travels to a friend
- **netstat** = Checking who is talking to you right now

---

## Cheatsheet Table

| Key Term | Definition | Importance/Function | Example |
|:---------|:-----------|:--------------------|:--------|
| ipconfig | Shows IP info | Basic network diagnosis | `ipconfig` |
| hostname | Shows device name | Identify your system | `hostname` |
| cls | Clears command screen | Cleaner view | `cls` |
| displaydns | Shows cached DNS entries | Check recent sites | `ipconfig /displaydns` |
| flushdns | Clears DNS cache | Solve browsing issues | `ipconfig /flushdns` |
| getmac | Shows MAC address | Device identity | `getmac` |
| arp -a | Shows IP-MAC mapping | Local network discovery | `arp -a` |
| ping | Tests connection | Check server reachability | `ping www.google.com` |
| tracert | Trace route to a server | Identify bottlenecks | `tracert www.google.com` |
| pathping | Shows loss & delay | Deeper network diagnosis | `pathping www.google.com` |
| netstat | Lists active connections | Monitor network traffic | `netstat` |
| nslookup | Find IP from domain | DNS troubleshooting | `nslookup www.google.com` |
| net user | Lists users | See local accounts | `net user` |

---

# ✅ Conclusion

These commands help **quickly find and fix** basic network problems.  
Mastering them makes you ready for any networking issue!

---