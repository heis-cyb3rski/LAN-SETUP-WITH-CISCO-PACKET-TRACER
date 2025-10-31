# LAN Setup with Cisco Packet Tracer

A practical Cisco Packet Tracer project demonstrating how to build and configure a Local Area Network (LAN) for a small branch office.  
This project covers connecting devices, assigning IPv4 addresses (DHCP and static), verifying connectivity, and using key network diagnostic commands such as `ipconfig`, `ping`, and `tracert`.

---

## 🚀 Objectives
- Connect network devices and hosts  
- Configure devices with IPv4 addressing  
- Verify end device configuration and connectivity  
- Use networking commands to view host information  

---

## 🧩 Scenario
A new branch office is opening, and you’ve been tasked with setting up the LAN.  
The devices (router, switch, PCs, printer, and ISP cloud) are already installed.  
Your job is to connect them, configure addressing, verify connectivity, and ensure hosts can reach both local and remote resources.

---

## 🖼 Network Topology
![LAN Topology](topology.png)

> You can explore the full lab by downloading the Packet Tracer file: [LAN-Setup.pkt](LAN-Setup.pkt)

---

## 🧰 Tools and Technologies
- Cisco Packet Tracer  
- Ethernet (Copper Straight-Through) Cables  
- Router, Switch, PCs, Printer  
- DHCP Configuration, Static IPs, and ICMP Tools  

---

## 📋 Addressing Table (Example)

| Device         | Interface      | IP Address        | Subnet Mask       | Default Gateway  |
|----------------|----------------|-------------------|-------------------|------------------|
| Office Router  | G0/1 (LAN)     | 192.168.1.1       | 255.255.255.0     | —                |
| Admin PC       | NIC (F0)       | DHCP (192.168.1.100) | 255.255.255.0 | 192.168.1.1      |
| Manager PC     | NIC (F0)       | DHCP (192.168.1.101) | 255.255.255.0 | 192.168.1.1      |
| Printer        | F0/0           | 192.168.1.10      | 255.255.255.0     | (optional) 192.168.1.1 |

---

## 🪜 Step-by-Step Configuration

### **Part 1: Connect Network Devices and Hosts**

**Step 1:** Power on all devices  
1. Open each device in Cisco Packet Tracer → *Physical Tab*.  
2. Locate the power switch and toggle it on.  
3. Confirm the green power light is on.  
   > Note: The switch model used here does not have a power switch.

**Step 2:** Connect devices using the following table  

| Device        | Interface/Port | Connected To | Connection Interface/Port |
|----------------|----------------|---------------|-----------------------------|
| Office Router  | G0/0           | ISP1          | G0/0                        |
| Office Router  | G0/1           | Switch        | G0/1                        |
| Admin PC       | NIC (F0)       | Switch        | F0/1                        |
| Manager PC     | NIC (F0)       | Switch        | F0/2                        |
| Printer        | NIC (F0)       | Switch        | F0/24                       |

- Use **Copper Straight-Through Cables** for all LAN connections.  
- Wait a few seconds for **green link lights** to appear — this indicates successful connectivity.

---

### **Part 2: Configure Devices with IPv4 Addressing**

**Step 1:** Configure PCs to obtain IP via DHCP  
1. Click each PC → *Desktop Tab* → *IP Configuration*.  
2. Select **DHCP**.  
3. The PCs should receive IP addresses from the router’s DHCP pool.

**Step 2:** Configure the Printer with a Static IP  
1. Click the printer → *Config Tab* → *FastEthernet0*.  
2. Enter:
   - IP Address: `192.168.1.10`
   - Subnet Mask: `255.255.255.0`
   - Default Gateway: (optional) `192.168.1.1`
3. This ensures the printer always keeps the same address.

**Explanation:**  
- PCs have **different IP addresses** but share the **same subnet mask and gateway** because they are on the same network.  
- The **printer** doesn’t need a gateway unless it must communicate outside the LAN.

---

### **Part 3: Verify End Device Configuration and Connectivity**

#### **Step 1: Verify IP Configuration**
On each PC:
1. Open **Command Prompt** → type: ipconfig
 You should see:
IPv4 Address. . . . . . . . . . . : 192.168.1.100
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.1.1
2. For full details: ipconfig /all
   This includes the MAC address, DHCP server IP, and DNS info.

---

#### **Step 2: Test Local Connectivity (Ping Tests)**
From the Admin PC:
ping 192.168.1.10 # Ping the printer
ping 192.168.1.101 # Ping the Manager PC
If replies are successful (`Reply from...`), the LAN is functioning correctly.

---

#### **Step 3: Test Internet Connectivity**
1. On each PC, open the **Web Browser**.  
2. Enter the IP address of the external web server (e.g., `10.0.0.2`).  
3. You should see a webpage appear.  
4. Then test using the **URL** (e.g., `http://example-server`).  
   - If you can connect using IP but not URL, it indicates a **DNS issue** (PCs may not have a DNS server assigned).

---

### **Part 4: Use Networking Commands**

#### **Command: `ipconfig`**
Displays IP configuration of a host.  
- Shows IPv4 address, subnet mask, and gateway.  
- The `/all` flag shows additional info like MAC address, DHCP server, and DNS.

#### **Command: `ping`**
Tests reachability between two devices.  
Example:
ping 192.168.1.10

If replies are successful, connectivity is confirmed at Layer 3.

#### **Command: `tracert`**
Traces the path packets take from your PC to a destination.

Example:
tracert www.cisco.pt

**Interpretation:**
- Each line (hop) represents a router along the path.
- In this case:
  - Hop 1: Office Router  
  - Hop 2: ISP Router  
  - Hop 3: Destination Server  
- 2 routers were passed before reaching the destination.

---

## 🔎 Troubleshooting

| Problem | Likely Cause | Fix |
|----------|---------------|-----|
| PC gets IP `169.254.x.x` | DHCP failed | Check cable connections and DHCP configuration on the router |
| Ping fails | Wrong interface or IP | Verify cabling and IP addressing |
| Can ping IP but not URL | DNS misconfiguration | Check DNS server address in `ipconfig /all` |
| tracert shows “* * *” | Router blocks ICMP | Ignore unless connectivity actually fails |

---

## ✅ Expected Results
- All devices (PCs and printer) powered and connected with green link lights.  
- PCs receive IPs from DHCP and can ping each other.  
- Printer responds to pings from both PCs.  
- PCs can access the external web server by IP and (if DNS configured) by name.  
- `tracert` shows the correct router path to the destination.

---

## 🧠 Reflection
Setting up a LAN in a new office requires more than just IP configurations — physical layout, cable management, and labeling are crucial.  
Always plan the IP addressing scheme before deployment, ensure DHCP and DNS are properly configured, and verify connectivity step by step to isolate any issues.

---

## 📂 Files Included
- `LAN-Setup.pkt` — Cisco Packet Tracer project file  
- `topology.png` — Network topology screenshot  
- `README.md` — Documentation and project guide  

---

## 👨‍💻 Author
**Skie**  
Networking Enthusiast | Cisco Learner | IT Support & Cybersecurity Focused  

---


