## 🔐 Standard Password Change Policy for Active Directory (AD)

### 1. **Password Complexity Requirements**

Enforce users to create strong passwords:

* Minimum length: **8 to 14 characters** (some recommend 12+)
* Must contain at least **3 of the 4 categories**:

  * Uppercase letters (A-Z)
  * Lowercase letters (a-z)
  * Numbers (0-9)
  * Special characters (!, @, #, \$, %, etc.)
* No passwords based on username or full name

---

### 2. **Password Expiration**

* Passwords should **expire every 30 to 90 days** depending on organizational policy.
* Typical: **90 days** is common in many enterprises.
* Users must change passwords **before expiry** (e.g., notify 14 days before expiry).

---

### 3. **Password History**

* Remember last **24 passwords** to prevent reuse.
* Prevents users from cycling through old passwords.

---

### 4. **Account Lockout Policy**

* Lock account after **3 to 5 failed login attempts**.
* Lockout duration: **15 minutes** or until admin unlocks.
* Helps protect against brute-force attacks.

---

### 5. **User Password Change Rights**

* Allow users to **change their password at any time**.
* Enforce **minimum password age** (e.g., 1 day) to prevent immediate password cycling.

---

## 🛠️ How to Configure These in Active Directory

---

### Step 1: Open **Group Policy Management**

* Run `gpmc.msc` on your Domain Controller.

---

### Step 2: Edit Default Domain Policy (or create a new GPO linked to the domain)

* Navigate to:

```
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Password Policy
```

---

### Step 3: Set Password Policies

| Policy                                      | Recommended Setting     |
| ------------------------------------------- | ----------------------- |
| Enforce password history                    | 24 passwords remembered |
| Maximum password age                        | 90 days (or 30-90)      |
| Minimum password age                        | 1 day                   |
| Minimum password length                     | 12 characters           |
| Password must meet complexity               | Enabled                 |
| Store passwords using reversible encryption | Disabled (default)      |

---

### Step 4: Set Account Lockout Policies (under **Account Lockout Policy**)

| Policy                              | Recommended Setting |
| ----------------------------------- | ------------------- |
| Account lockout threshold           | 5 invalid attempts  |
| Account lockout duration            | 15 minutes          |
| Reset account lockout counter after | 15 minutes          |

---

### Step 5: Set User Notification for Password Expiry

You can enable notification through Windows or custom scripts to notify users **14 days before password expiry**.

---

## 📌 Additional Recommendations

* Consider implementing **Multi-Factor Authentication (MFA)** alongside password policies.
* Use **Azure AD Password Protection** to block commonly used or compromised passwords.
* Educate users on secure password creation and phishing risks.

---

## Summary Table

| Setting                   | Value      |
| ------------------------- | ---------- |
| Min password length       | 12         |
| Password complexity       | Enabled    |
| Password history          | 24         |
| Max password age          | 90 days    |
| Min password age          | 1 day      |
| Account lockout threshold | 5 attempts |
| Lockout duration          | 15 minutes |
| Reset lockout counter     | 15 minutes |

---
