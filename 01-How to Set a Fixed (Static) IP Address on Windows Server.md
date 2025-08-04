# 🛠 How to Set a Fixed (Static) IP Address on Windows Server

This guide provides a step-by-step walkthrough for configuring a static IP address on a Windows Server.

---

## ✅ Step 1: Open Network Settings

1. Press `Windows + R`  
2. Type `ncpa.cpl` and press **Enter**  
   *(Opens the Network Connections window)*

---

## ✅ Step 2: Choose the Network Adapter

1. Right-click on your active network adapter (e.g., **Ethernet**)  
2. Select **Properties**

---

## ✅ Step 3: Edit IPv4 Settings

1. Scroll to **Internet Protocol Version 4 (TCP/IPv4)**  
2. Click **Properties**

---

## ✅ Step 4: Assign a Static IP

1. Select: **Use the following IP address**
2. Enter your IP settings:
   - **IP address**: `192.168.1.100` *(example)*
   - **Subnet mask**: `255.255.255.0`
   - **Default gateway**: `192.168.1.1`

---

## ✅ Step 5: Set DNS Server

1. Select: **Use the following DNS server addresses**
2. Enter:
   - **Preferred DNS**: `8.8.8.8`
   - **Alternate DNS**: `8.8.4.4` *(or your local DNS)*

---

## ✅ Step 6: Apply and Close

1. Click **OK** to close the IPv4 settings
2. Click **Close** to finish

---

## ✅ Step 7: Verify Configuration

1. Open **Command Prompt** (`cmd`)
2. Run the command:
   ```bash
   ipconfig
   ```

3. Confirm that the static IP is correctly set

---

## 🧪 Optional: Test Connectivity

Use `ping` to test network connectivity:

```bash
ping 8.8.8.8
ping google.com
ping 192.168.1.1
```

---

## 📌 Notes

* Ensure the IP address you assign is not already in use.
* Reboot the server if needed.
* For domain controllers, always use internal DNS servers.

---

📁 **Author**: Xitiz Basnet
📅 **Last Updated**: August 04, 2025

---
