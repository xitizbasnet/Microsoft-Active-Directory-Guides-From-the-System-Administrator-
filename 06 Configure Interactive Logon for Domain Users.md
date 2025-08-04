## 🧑‍💻 What is "Interactive Logon"?

**Interactive Logon** means users log in directly at a machine (local or RDP) using their credentials. These logon policies **affect the experience at the Windows login screen**.

---

## 🛠️ Step-by-Step: Configure Interactive Logon for Domain Users

---

### ✅ **Step 1: Open Group Policy Management**

1. On your Domain Controller:

   * Open **Server Manager**
   * Go to **Tools** → **Group Policy Management**

---

### ✅ **Step 2: Create or Edit a GPO**

* Right-click your domain (`xitiztechservices.local`) or a specific **OU**
* Click **Create a GPO in this domain, and Link it here**
* Name it:
  `Interactive Logon Policy`
* Right-click the GPO → Click **Edit**

---

### ✅ **Step 3: Navigate to Interactive Logon Settings**

Go to:

```
Computer Configuration
→ Windows Settings
→ Security Settings
→ Local Policies
→ Security Options
```

Look for policies starting with:

```
Interactive logon:
```

---

### ✅ **Step 4: Configure the Desired Policies**

Here's a list of commonly used **Interactive Logon settings** and what they do:

| Policy                                                                  | Description                             | Suggested Setting                    |
| ----------------------------------------------------------------------- | --------------------------------------- | ------------------------------------ |
| **Interactive logon: Message title**                                    | Displays a custom title before login    | "Welcome to XitizTechServices"       |
| **Interactive logon: Message text**                                     | Legal notice or message to users        | "Unauthorized access is prohibited." |
| **Interactive logon: Do not display last user name**                    | Hides last logged-in user               | Enabled *(for security)*             |
| **Interactive logon: Require smart card**                               | Enforce smart card login                | Disabled (unless required)           |
| **Interactive logon: Number of previous logons to cache**               | Offline logon attempts allowed          | 10 (default)                         |
| **Interactive logon: Prompt user to change password before expiration** | Warn before password expiry             | 14 days                              |
| **Interactive logon: Smart card removal behavior**                      | What happens when smart card is removed | Lock Workstation                     |

To configure:

1. Double-click the policy
2. Set to **Enabled/Disabled** as required
3. Click **Apply**, then **OK**

---

### ✅ **Step 5: Link the GPO to Target Users or Computers**

* If you want to apply the policy to **all users**, link the GPO to the **domain root**
* If targeting specific users/computers, link it to the appropriate **OU**

---

### ✅ **Step 6: Apply the GPO**

On client machines:

```powershell
gpupdate /force
```

Or reboot the machine.

---

### ✅ **Step 7: Test the Configuration**

1. Log out and attempt an **interactive logon**
2. Confirm that:

   * Any message text/title appears
   * Usernames are/aren’t shown (based on policy)
   * Password expiration prompts work

---

## ✅ Example: Set Legal Notice on Login

Set these policies:

* **Interactive logon: Message title** = "XitizTechServices Notice"
* **Interactive logon: Message text** = "Only authorized users may access this system. Activity may be monitored."

This displays a warning before users enter their credentials.

---

## 📌 Summary Table

| Setting                | Path             | Purpose                              |
| ---------------------- | ---------------- | ------------------------------------ |
| Message Title/Text     | Security Options | Legal or welcome message             |
| Do Not Show Username   | Security Options | Increases security                   |
| Smart Card Requirement | Security Options | Enforces 2FA                         |
| Logon Cache            | Security Options | Offline logon attempts               |
| Password Warning       | Security Options | Reminds user before password expires |

---
