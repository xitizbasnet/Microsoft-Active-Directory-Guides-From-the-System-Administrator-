## 🛠 How To Install AD DS & Create Domain Controller (`xitiztechservices.local`)

### ✅ **Step 1: Rename the Computer (Optional but Recommended)**

1. Open **Server Manager**
2. Click **Local Server** on the left
3. Click on the computer name
4. Click **Change** and give it a name like `DC01`
5. Reboot the server when prompted

---

### ✅ **Step 2: Install AD DS Role**

1. Open **Server Manager**
2. Click **Manage** > **Add Roles and Features**
3. Click **Next** through:

   * **Before You Begin**
   * **Installation Type**: Choose **Role-based or feature-based installation**
   * Click **Next**
   * **Select Destination Server**: Select a server from the Server pool
   * Click **Next**
4. In **Server Roles**:

   * Check **Active Directory Domain Services**
   * Click **Add Features** if prompted
5. Click **Next**
6. Do not change anything and Click **Next**
7.  **Active Directory Domain Services:** Click **Next**
8. **Confirm Installation Selection:** ✅ **Restart the destination server automatically if required**
9. Pop up Option: Select **Yes**
10. Click **Install**
11. Wait for the installation to complete, Click **Close**

---

### ✅ **Step 3: Promote the Server to a Domain Controller**

1. Once installed, click the **flag icon** in Server Manager → Click **Promote this server to a domain controller**
2. Choose:

   * **Add a new forest**
   * **Root domain name**: `xitiztechservices.local`
3. Click **Next**

---

### ✅ **Step 4: Domain Controller Options**

1. Set:

   * **Forest functional level**: Windows Server 2016 or higher
   * **Domain functional level**: Windows Server 2016 or higher
   * Check:

     * ✅ **Domain Name System (DNS) server** 
     * ✅ **Global Catalog (GC)** 
   * Enter a **Directory Services Restore Mode (DSRM) password**
   * Password: **P@ssw)rd@123**
   * Confirm Password: **P@ssw)rd@123**
2. Click **Next**

---

### ✅ **Step 6: DNS Options**

1. You may see a warning about a delegation not being created—this is normal.
   * ❌ **Create DNS delegation**
   * Click **Next**

---

### ✅ **Step 7: Additional Options**

1. NetBIOS domain name should **auto-fill** as `XITIZTECHSERVICES`
2. Click **Next**

---

### ✅ **Step 8: Paths**

1. Leave the default:

   * **Database folder**: `C:\Windows\NTDS`
   * **Log folder**: `C:\Windows\NTDS`
   * **SYSVOL folder**: `C:\Windows\SYSVOL`
2. Click **Next**

---

### ✅ **Step 9: Review and Install**

1. Review settings
2. Click **View Script** (optional) to save PowerShell script
3. Click **Next**,
4. Click **Install**
5. **Signed Out:** Click **Close**
6. After install, server will automatically **reboot**

---

### ✅ **Step 10: Verify the Domain Controller**

After reboot:

1. Log in with:

   * **Username**: `XITIZTECHSERVICES\Administrator`
   * **Password**: `P@ssw)rd@123`
2. Open **Server Manager** > Tools:

   * Confirm **Active Directory Users and Computers**, **DNS**, etc., are available

---

## 📁 Summary

| Step | Task                                     |
| ---- | ---------------------------------------- |
| 1    | Set Static IP                            |
| 2    | Rename Server (e.g., DC01)               |
| 3    | Install AD DS Role                       |
| 4    | Promote to Domain Controller             |
| 5    | Create domain: `xitiztechservices.local` |
| 6    | Reboot & verify                          |

---

