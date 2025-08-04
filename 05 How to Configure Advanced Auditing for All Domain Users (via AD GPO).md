## 🛡️ How to Configure Advanced Auditing for All Domain Users (via AD GPO)

### ✅ **Step 1: Open Group Policy Management**

1. On your Domain Controller:

   * Go to **Start > Server Manager**
   * Click **Tools > Group Policy Management**

---

### ✅ **Step 2: Create or Edit a GPO**

* Right-click your domain (e.g., `xitiztechservices.local`) or an OU → Click **Create a GPO in this domain, and Link it here**
* Name the GPO something like:
  `Advanced Auditing Policy`
* Right-click the new GPO → Click **Edit**

---

### ✅ **Step 3: Enable Audit Policy Settings**

Navigate to:

```
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Advanced Audit Policy Configuration
→ Audit Policies
```

You’ll see categories such as:

| Category                     | Common Use                                  |
| ---------------------------- | ------------------------------------------- |
| **Account Logon**            | Logon attempts with domain credentials      |
| **Account Management**       | User/group/computer account changes         |
| **Directory Service Access** | AD object access logs                       |
| **Logon/Logoff**             | User logons, session locking, remote logins |
| **Object Access**            | File, folder, registry, and printer access  |
| **Policy Change**            | Changes to audit policy, trust, user rights |
| **Privilege Use**            | Use of admin rights like SeBackupPrivilege  |
| **System**                   | System restarts, shutdowns                  |

---

### ✅ **Step 4: Configure Audit Subcategories**

For each category you want to audit:

1. Click on the category (e.g., **Logon/Logoff**)
2. Double-click a subcategory (e.g., **Logon**)
3. Set it to:

   * **Configure the following audit events**
   * Check **Success** and/or **Failure** based on your needs

🔒 Recommended auditing examples:

* **Logon/Logoff > Logon** → Success & Failure
* **Account Management > User Account Management** → Success & Failure
* **Object Access > File System** → Success
* **Directory Service Access > Directory Service Changes** → Success

---

### ✅ **Step 5: Apply & Close the GPO Editor**

Once your desired categories are configured:

* Close the Group Policy Editor

---

### ✅ **Step 6: Link GPO to Domain or OU**

Ensure the GPO is **linked** to:

* The entire domain: `xitiztechservices.local`
* Or a specific OU where the computers or users exist

---

### ✅ **Step 7: Force Group Policy Update**

On target computers (or remotely via PowerShell):

```powershell
gpupdate /force
```

Or reboot them to apply the new audit policy.

---

### ✅ **Step 8: Enable Object Access Auditing (Optional but Required for File/Folder Auditing)**

1. Open **Local Security Policy** or use a GPO:

   ```
   Computer Configuration
   → Policies
   → Windows Settings
   → Security Settings
   → Local Policies
   → Audit Policy
   ```
2. Enable **Audit object access** → Success and/or Failure

---

### ✅ **Step 9: Configure SACLs on Objects (Like Files/Folders)**

To audit **specific files/folders**:

1. Right-click the file/folder → Properties
2. Go to **Security > Advanced**
3. Click **Auditing** tab → **Add**
4. Select a principal (e.g., `Everyone`)
5. Choose **Successful** or **Failed** access types (e.g., Read, Write)
6. Apply settings

Now, file/folder access will generate **Event ID 4663** in the **Security log**

---

### ✅ **Step 10: View Audit Logs**

1. On any domain-joined computer or DC:

   * Open **Event Viewer**
   * Navigate to:

     ```
     Windows Logs → Security
     ```

Look for key **Event IDs**:

| Event ID | Description                                     |
| -------- | ----------------------------------------------- |
| 4624     | Successful Logon                                |
| 4625     | Failed Logon                                    |
| 4634     | Logoff                                          |
| 4670     | Permission change on object                     |
| 4662     | Operation performed on directory service object |
| 4663     | Access to an object (files/folders)             |

---

## 🧠 Tip: Centralize Logging (Optional)

If you manage many users, consider:

* **Forwarding logs** to a **SIEM** (e.g., Splunk, Azure Sentinel)
* Using **Windows Event Forwarding (WEF)** to a central collector

---

## ✅ Summary

| Task                             | Description                      |
| -------------------------------- | -------------------------------- |
| Create GPO                       | Named `Advanced Auditing Policy` |
| Enable Advanced Audit Categories | Use fine-grained controls        |
| Apply to Domain or OU            | Link the GPO accordingly         |
| Enable Object Access Auditing    | For file/folder tracking         |
| Configure SACLs                  | Audit specific files, AD objects |
| Review Logs                      | Use Event Viewer on client or DC |

---
