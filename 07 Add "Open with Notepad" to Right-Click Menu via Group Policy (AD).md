## 🛠️ Step-by-Step: Add "Open with Notepad" to Right-Click Menu via Group Policy (AD)

---

### ✅ **Option 1: Using Group Policy to Deploy Registry Setting**

---

### ✅ **Step 1: Open Group Policy Management**

1. On your Domain Controller:

   * Open **Server Manager**
   * Go to **Tools > Group Policy Management**

---

### ✅ **Step 2: Create or Edit a GPO**

* Right-click your domain or OU → **Create a GPO in this domain, and Link it here**
* Name it: `Add Notepad to Right-Click`
* Right-click the GPO → **Edit**

---

### ✅ **Step 3: Navigate to Registry Settings**

Go to:

```
User Configuration
→ Preferences
→ Windows Settings
→ Registry
```

> You can also use **Computer Configuration** if you want this to apply machine-wide (for all users on a device).

---

### ✅ **Step 4: Create the Registry Key**

1. Right-click **Registry** > **New > Registry Item**
2. Use the following values:

#### 📄 **Registry Key Settings**

| Field          | Value                               |
| -------------- | ----------------------------------- |
| **Action**     | Create                              |
| **Hive**       | HKEY\_CLASSES\_ROOT                 |
| **Key Path**   | `*\shell\Open with Notepad\command` |
| **Value name** | *(leave blank)*                     |
| **Value type** | REG\_SZ                             |
| **Value data** | `notepad.exe "%1"`                  |

✔ This tells Windows to run `notepad.exe` and open the selected file (`%1`) when the user right-clicks.

---

### ✅ **Step 5: Apply the GPO**

1. Link the GPO to your **target OU or domain**
2. Run the following on client machines or wait for auto-refresh:

```powershell
gpupdate /force
```

---

### ✅ **Step 6: Test the Context Menu**

1. Log in as a domain user
2. Right-click on **any file**
3. You should see a new option:
   ➤ **Open with Notepad**

---

## 📝 Want to Use Notepad++ Instead?

Use this in **Step 4** as the Value data (assuming Notepad++ is installed):

```
"C:\Program Files\Notepad++\notepad++.exe" "%1"
```

Make sure Notepad++ is installed on all machines (deploy via GPO or manually).

---

## 🔐 Optional: Apply via Computer Configuration

If you want the option available for **all users on a PC**, repeat the steps under:

```
Computer Configuration
→ Preferences
→ Windows Settings
→ Registry
```

---

## ✅ Summary

| Task             | Description                                     |
| ---------------- | ----------------------------------------------- |
| Add Context Menu | Deploy registry key via GPO                     |
| Location         | `HKEY_CLASSES_ROOT\*\shell`                     |
| Action           | Runs `notepad.exe "%1"`                         |
| Applies To       | All users or all computers (based on GPO scope) |

---
