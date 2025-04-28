# Ex 2: IPv4 Addressing and Subnetting

## Aim:
To implement IPv4 addressing and subnetting, which includes binary, decimal, class identification, network and host identification, and subnetting.

## Description:
IPv4 addressing is a critical concept in computer networking, where every device on a network is assigned a unique 32-bit address. In this exercise, we will cover the following key topics:

1. **Binary-to-Decimal and Decimal-to-Binary Conversion**:
   - Learn how to convert IP addresses between binary and decimal forms. IPv4 addresses are typically represented in decimal but operate in binary on networking devices.

2. **Addressing Class Identification**:
   - Understand the five IPv4 address classes (A, B, C, D, E), which are determined by the first octet's range. The class identifies the network and host portions of the address.

3. **Host Identification**:
   - Learn how to identify the network and host portions of an IPv4 address using a subnet mask. This also includes determining the range of addresses available for devices in a subnet.

4. **Network Addresses**:
   - Learn how to determine the network address, which is the network's unique identity. This is calculated by performing a bitwise AND operation between the IP address and the subnet mask.

5. **Host Addresses**:
   - Learn how to identify valid host addresses within a subnet, excluding the network address and broadcast address, to assign to devices.

6. **Subnetting**:
   - Learn how to divide a larger network into smaller sub-networks (subnets) for more efficient network management, security, and better utilization of IP addresses.

---

## Steps for Implementation with Examples:

### 1. **Binary to Decimal Conversion**:

   **Explanation**: 
   - To convert an IPv4 address from binary to decimal, break it down into 8-bit groups (octets). Each octet is then converted to its decimal equivalent.

   **Example**:
   - Binary: `11000000.10101000.00000001.00000001`
   - Step 1: Convert each octet:
     - `11000000` = 192
     - `10101000` = 168
     - `00000001` = 1
     - `00000001` = 1
   - Decimal Result: `192.168.1.1`

---

### 2. **Decimal to Binary Conversion**:

   **Explanation**: 
   - To convert an IPv4 address from decimal to binary, convert each of the four decimal numbers into 8-bit binary numbers.

   **Example**:
   - Decimal: `192.168.1.1`
   - Step 1: Convert each octet:
     - `192` = `11000000`
     - `168` = `10101000`
     - `1` = `00000001`
     - `1` = `00000001`
   - Binary Result: `11000000.10101000.00000001.00000001`

---

### 3. **Address Class Identification**:

   **Explanation**: 
   - IPv4 addresses are divided into classes (A, B, C, D, E) based on the first octet (the first 8 bits of the address). The class determines the size of the network and the range of possible host addresses.

   **Example**:
   - IP: `192.168.1.1`
   - Step 1: Identify the first octet: `192`
   - Step 2: Check the address class:
     - Class A: `0.0.0.0` to `127.255.255.255`
     - Class B: `128.0.0.0` to `191.255.255.255`
     - Class C: `192.0.0.0` to `223.255.255.255`
     - Class D: `224.0.0.0` to `239.255.255.255`
     - Class E: `240.0.0.0` to `255.255.255.255`
   - The first octet `192` falls in Class C (`192.0.0.0` to `223.255.255.255`).

---

### 4. **Network and Host Identification**:

   **Explanation**: 
   - The network and host portions of an IP address are separated by the subnet mask. The subnet mask is used to determine which part of the address refers to the network and which part refers to the host.

   **Example**:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
   - Step 1: Convert both the IP and subnet mask to binary:
     - IP: `11000000.10101000.00000001.00001010`
     - Subnet Mask: `11111111.11111111.11111111.00000000`
   - Step 2: Perform a bitwise AND operation to determine the network address:
     - `11000000.10101000.00000001.00001010` AND `11111111.11111111.11111111.00000000`
     - Result: `11000000.10101000.00000001.00000000` (Network Address: `192.168.1.0`)
   - The **network portion** is the first three octets (`192.168.1`), and the **host portion** is the last octet (`10`).

---

### 5. **Network Addresses**:

   **Explanation**: 
   - The network address represents the entire network. It is calculated using a bitwise AND operation between the IP address and the subnet mask.

   **Example**:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
   - Step 1: Use the bitwise AND operation as done above.
   - Network Address Result: `192.168.1.0`

---

### 6. **Host Addresses**:

   **Explanation**: 
   - Host addresses refer to the addresses assigned to individual devices in the network. These addresses fall between the network address and the broadcast address.

   **Example**:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
   - Network Address: `192.168.1.0`
   - Broadcast Address: `192.168.1.255`
   - Valid Host Range: `192.168.1.1` to `192.168.1.254` (excluding `192.168.1.0` and `192.168.1.255`).

---

### 7. **Default Subnet Mask**:

   **Explanation**: 
   - The default subnet mask is the subnet mask assigned based on the class of the address. This is used for network division without custom subnetting.

   **Example**:
   - Class A: `255.0.0.0`
   - Class B: `255.255.0.0`
   - Class C: `255.255.255.0`

---

### 8. **Custom Subnet Mask**:

   **Explanation**: 
   - Custom subnet masks allow you to divide a network into smaller subnets by borrowing bits from the host portion.

   **Example**:
   - Given network: `192.168.1.0/24` (with subnet mask `255.255.255.0`)
   - Subnetting it into 4 subnets requires borrowing 2 bits, resulting in a new subnet mask: `255.255.255.192` (or `/26`).
   - Subnet Breakdown:
     - Subnet 1: `192.168.1.0/26`
     - Subnet 2: `192.168.1.64/26`
     - Subnet 3: `192.168.1.128/26`
     - Subnet 4: `192.168.1.192/26`

---

### 9. **Subnetting**:

   **Explanation**: 
   - Subnetting involves dividing a network into smaller subnetworks. This allows for efficient use of IP addresses and better network management.

   **Example**:
   - IP Address: `192.168.1.0/24`
   - Subnet Mask: `255.255.255.192` (or `/26`), which divides the network into 4 subnets.

   - Resulting Subnets:
     - Subnet 1: `192.168.1.0/26` → Usable range: `192.168.1.1` to `192.168.1.62`
     - Subnet 2: `192.168.1.64/26` → Usable range: `192.168.1.65` to `192.168.1.126`
     - Subnet 3: `192.168.1.128/26` → Usable range: `192.168.1.129` to `192.168.1.190`
     - Subnet 4: `192.168.1.192/26` → Usable range: `192.168.1.193` to `192.168.1.254`

---

## Conclusion:
The program for IPv4 Addressing and Subnetting has been successfully implemented and tested. It demonstrates how to manage and allocate IP addresses effectively using subnetting techniques. By mastering these concepts, one can design and manage optimized and secure networks.

---

### **Cheatsheet**:

| Key Term                | Definition                                                                 | Importance/Function                                      | Example                                |
|-------------------------|---------------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| **IPv4 Address**         | A 32-bit unique identifier assigned to devices on a network.               | Identifies devices in a network for communication.       | `192.168.1.1`                         |
| **Subnet Mask**          | Defines the boundary between the network and host portions of an IP address. | Allows proper routing by separating network and host.    | `255.255.255.0`                        |
| **Network Address**      | The address that identifies the network itself.                           | Used to represent the entire network.                    | `192.168.1.0`                          |
| **Host Address**         | The address assigned to devices in the network (excluding network/broadcast). | Identifies individual devices in the network.            | `192.168.1.10`                         |
| **Subnetting**           | The process of dividing a larger network into smaller subnets.            | Enh
