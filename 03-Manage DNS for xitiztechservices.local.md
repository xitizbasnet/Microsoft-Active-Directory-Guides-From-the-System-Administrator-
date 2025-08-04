## 🛠 Step-by-Step: Manage DNS for `xitiztechservices.local`

### ✅ **Assumptions**

* Your Domain Controller has a **static IP**, e.g., `192.168.1.10`
* You've installed **AD DS**, which auto-installs **DNS**
* The domain name is: `xitiztechservices.local`

---

### ✅ **Step 1: Open DNS Manager**

1. Open **Server Manager**
2. Click **Tools** (top-right)
3. Select **DNS**

---

### ✅ **Step 2: Verify Forward Lookup Zone**

1. In DNS Manager, expand your server name **xitiztechservicesdc01**
2. Expand **Forward Lookup Zones**
3. You should see a zone named `xitiztechservices.local`

If it's missing:

* Right-click **Forward Lookup Zones** > **New Zone**
* Select:

  * ✅ **Primary zone**
  * ✅ Zone name: `xitiztechservices.local`
  * Store in AD: ✅ (if prompted)
  * Allow secure dynamic updates ✅

---

### ✅ **Step 3: Check Host (A) Records**

In the `xitiztechservices.local` zone:

* You should see a record like:

  ```
  Name:     (same as parent)
  Type:     A
  Data:     192.168.1.10
  ```

This means the domain (`xitiztechservices.local`) points to your DC IP.

---

### ✅ **Step 4: Configure Reverse Lookup Zone (Optional but Recommended)**

1. In DNS Manager, right-click **Reverse Lookup Zones** > **New Zone**
2. Select:

   * ✅ **Primary Zone**
   * ✅ **To all DNS servers running on domain controllers in the domain: xitiztechservices.local**
   * ✅ **IPv4 Reverse Lookup Zone**
3. ✅ For Network ID, if your DC IP is `192.168.1.10`, enter `192.168.1`
4. ✅ Allow secure dynamic updates (recommended for Active Directory)
5. Complete the wizard.

###  ✅ Configure PRT

6. Click **Reverse Lookup Zones** > **0.0.10.in-addr.arpa**
7.  right-click **0.0.10.in-addr.arpa** > New Pointer (PTR)....
8.  Host Name : Click **Browse**
9.  **Records:** Double-Click on your server name: **xitiztechservicesdc01**
10.  Double-Click on **Forward Lookup**
11.  Double-Click on **xitiztechservices.local**
12.  Double-Click on last details **xitiztechservicesdc01** which has the timestamp **static**
13.  Click **OK**
14.  Again Click **OK** after verify

This enables reverse DNS: resolving IPs back to names.

---

### ✅ **Step 5: Configure Clients to Use the DC as DNS**

On client PCs (or DHCP Server), set **Preferred DNS** to:

```
192.168.1.10  ← your DC's IP
```

Do **not** use public DNS like 8.8.8.8 on clients in a domain.

---

### ✅ **Step 6: Test DNS Functionality via Powershell**

#### ✅ From the Domain Controller:

```powershell
nslookup xitiztechservices.local
```

Expected output:

* Name: `xitiztechservices.local`
* Address: `192.168.1.10`

#### ✅ From a domain-joined client:

```powershell
ping xitiztechservices.local
```

It should resolve to your DC’s IP.

---

### ✅ **Step 7: Add Custom DNS Records (Optional)**

In DNS Manager:

* Right-click your zone > **New Host (A or AAAA)**
* Add servers, web hosts, printers, etc., with specific IPs

Example:

* **Name**: `intranet`
* **IP**: `192.168.1.25`
  ➡️ Result: `intranet.xitiztechservices.local → 192.168.1.25`

---

## ✅ Summary Table

| Task               | Description                           |
| ------------------ | ------------------------------------- |
| DNS Role Installed | Auto-installed with AD DS             |
| Domain Zone Exists | `xitiztechservices.local`             |
| A Record           | Points domain to DC IP                |
| Reverse Zone       | Optional but good for reverse lookups |
| Client DNS         | Must point to DC IP                   |
| Public DNS         | Avoid on domain clients               |

---
