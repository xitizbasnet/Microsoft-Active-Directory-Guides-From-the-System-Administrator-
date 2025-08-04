## 🧑‍💼 Add Users, Groups, and Organize by Company & Department in Active Directory

### ✅ Step 1: Plan Your AD Structure (Organizational Units - OUs)

Organize your directory like this:

```
xitiztechservices.local
├── Users
│   ├── CompanyA
│   │   ├── HR
│   │   ├── IT
│   │   └── Sales
│   └── CompanyB
│       ├── HR
│       ├── IT
│       └── Finance
└── Groups
    ├── HR_Group
    ├── IT_Admins
    └── Sales_Team
```

---

### ✅ Step 2: Create Organizational Units (OUs)

1. Open **Active Directory Users and Computers**
2. Right-click the domain (`xitiztechservices.local`) > **New > Organizational Unit**
3. Create:

   * `CompanyA`, `CompanyB`
   * Inside them: `HR`, `IT`, `Sales`, etc.

---

### ✅ Step 3: Create Security Groups

1. Right-click `Groups` OU > **New > Group**
2. Use:

   * Group name: `HR_Group_CompanyA`
   * Group scope: **Global**
   * Group type: **Security**

Repeat for each department.

---

### ✅ Step 4: Create User Accounts

1. Right-click the department OU (e.g., `CompanyA > HR`) > **New > User**
2. Fill in:

   * First name, last name
   * User logon name: `jane.doe`
3. Set password policy:

   * Require password change on next logon: ✅ (Recommended)
4. Click **Finish**

---

### ✅ Step 5: Add Users to Groups

1. Open user properties → **Member Of** tab
2. Add the user to their appropriate group (e.g., `HR_Group_CompanyA`)

---

## 🔒 2. Add a Local Admin Account on All Domain Computers (Backup Access)

If the **Domain Administrator account becomes inaccessible**, it’s good to have a **local administrator** account on all domain computers.

---

### ✅ Option 1: Use Group Policy to Create a Local User on All Machines

---

#### 🛠 Step 1: Open Group Policy Management

1. On the Domain Controller:

   * Open **Server Manager** > Tools > **Group Policy Management**

---

#### 🛠 Step 2: Create GPO to Add Local User

1. Right-click the domain or OU (e.g., `xitiztechservices.local`) > **Create GPO**
2. Name it: `Create Local Admin Account`
3. Right-click the GPO → **Edit**

---

#### 🛠 Step 3: Navigate to User Creation Setting

Go to:

```
Computer Configuration
→ Preferences
→ Control Panel Settings
→ Local Users and Groups
```

---

#### 🛠 Step 4: Add a New Local User

1. Right-click **Local Users and Groups** > **New > Local User**
2. Action: **Create**
3. Name: `LocalAdmin`
4. Full name: `Backup Admin Account`
5. Password: *(Set a strong password and confirm it)*
6. Check **Password never expires**
7. Check **User cannot change password**

---

#### 🛠 Step 5: Add to Administrators Group

1. Right-click **Local Users and Groups** > **New > Local Group**
2. Group name: `Administrators`
3. Action: **Update**
4. Add member: `LocalAdmin` (or whatever username you chose)

---

### 🔄 Step 6: Apply the GPO

Run the following on target machines (or reboot):

```powershell
gpupdate /force
```

---

### ✅ Option 2: Use PowerShell to Create Local Users (Advanced)

You can also deploy a script using a **startup GPO script**.

```powershell
net user LocalAdmin P@ssw0rd123 /add
net localgroup administrators LocalAdmin /add
```

> Be cautious—scripts expose passwords in plain text. Use **Group Policy Preferences** with encryption instead.

---

## 🧪 Step 7: Test the Local Account

1. Log out of the domain
2. Click **Other User**
3. Type:

   * Username: `.\LocalAdmin`
   * Password: *(your set password)*

It should log in **locally**, even if the domain is offline.

---

## 🛡️ Security Recommendations

| Task                              | Action                                                  |
| --------------------------------- | ------------------------------------------------------- |
| Hide LocalAdmin from login screen | Use registry or GPO to hide user                        |
| Audit LocalAdmin usage            | Enable audit policy for logon events                    |
| Rotate local passwords            | Use LAPS (Local Admin Password Solution) from Microsoft |
| Limit permissions                 | Do not overuse local admin rights                       |

---

## ✅ Summary

| Task                   | Tool/Location              |
| ---------------------- | -------------------------- |
| Create OUs             | ADUC                       |
| Create Users/Groups    | ADUC                       |
| Assign Users to Groups | ADUC (Member Of tab)       |
| Deploy Local Admin     | GPO → Local Users & Groups |
| Test Backup Access     | Login as `.\LocalAdmin`    |

---

