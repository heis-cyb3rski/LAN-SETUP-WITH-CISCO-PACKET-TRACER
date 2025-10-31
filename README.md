# LAN-SETUP-WITH-CISCO-PACKET-TRACER
A practical Cisco Packet Tracer project demonstrating how to create a functional Local Area Network (LAN) for a small office. The project covers connecting network devices, configuring IPv4 addressing, verifying connectivity, and using network diagnostic commands.


---

## 📘 Objectives
- Connect network devices and hosts  
- Configure devices with IPv4 addressing  
- Verify end device configuration and connectivity  
- Use networking commands to view host information  

---

## 🧩 Scenario
A new branch office is opening, and you have been tasked with setting up the LAN. The network devices are already installed, but you must connect them, configure IPv4 addressing, and ensure that hosts can reach both local and remote resources.

---

## ⚙️ Project Steps

### **Part 1: Connect Network Devices and Hosts**

**Step 1: Power on the devices**
1. Click each device and open its **Physical Tab** in Cisco Packet Tracer.  
2. Locate and toggle the **power switch** for each device (Router and PCs).  
3. Confirm the **green power light** appears, indicating the device is on.  
   *Note: The switch model used here has no power button.*

**Step 2: Connect all devices**
Use the following connection table to create the physical network:

| Device        | Interface/Port | Connected To | Connection Interface/Port |
|----------------|----------------|---------------|-----------------------------|
| Office Router  | G0/0           | ISP1          | G0/0                        |
| Office Router  | G0/1           | Switch        | G0/1                        |
| Admin PC       | NIC (F0)       | Switch        | F0/1                        |
| Manager PC     | NIC (F0)       | Switch        | F0/2                        |
| Printer        | NIC (F0)       | Switch        | F0/24                       |

**Actions:**
- Use **Ethernet Copper Straight-Through cables** for all LAN connections.  
- Connect the **router to the ISP** using the cloud device’s interface dropdown.  
- Wait for **green link lights** to confirm active connections.

---

### **Part 2: Configure Devices with IPv4 Addressing**

**Step 1: Configure host devices**
- Open each PC → **Desktop Tab → IP Configuration**.  
- Set **Admin PC** and **Manager PC** to **DHCP mode** to receive automatic IP addresses from the router.  

**Step 2: Configure the printer**
1. Open the **Printer → Config Tab → FastEthernet0 Interface.**  
2. Assign a **static IP address** based on the Addressing Table (e.g., `192.168.1.10`).  
3. Leave the default gateway empty since the printer is only accessed locally.  

**Concept Check:**  
- PCs have **different IPs** but **same subnet mask and gateway** because they share the same network.  
- The printer can use the **router’s LAN interface IP** as its gateway if needed.

---

### **Part 3: Verify End Device Configuration and Connectivity**

**Step 1: Test LAN connectivity**
- On each PC, open **Command Prompt → type `ipconfig`** to view assigned IP.  
- Use the **`ping`** command to test communication:
  ```bash
  ping 192.168.1.10   # Example: Printer IP
