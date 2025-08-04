## 🖼️ How to Set Desktop Wallpaper via Group Policy (GPO) in Active Directory

### ✅ **Pre-requisites**

* A domain environment (`xitiztechservices.local`)
* You have a **Domain Controller** (e.g., `DC01`)
* A **.jpg/.bmp** image file stored on a **shared network location** or locally on the domain controller

---

## 🛠️ Step-by-Step Process

---

### ✅ **Step 1: Place the Wallpaper Image in a Shared Folder**

1. On your DC or a network file server:

   * Create a shared folder (e.g., `\\DC01\Wallpapers`)
   * Place your wallpaper image (e.g., `default.jpg`) there
2. Set **permissions** so **all domain users** can read it:

   * Share permissions: `Everyone - Read`
   * NTFS permissions: `Authenticated Users - Read`

📁 Example image path:

```
\\DC01\Wallpapers\default.jpg
```

---

### ✅ **Step 2: Open Group Policy Management**

1. On your Domain Controller:

   * Open **Server Manager**
   * Click **Tools** > **Group Policy Management**

---

### ✅ **Step 3: Create or Edit a GPO**

1. Navigate to the **OU** where the users are located:

   * e.g., `xitiztechservices.local > Users`
2. Right-click the OU > **Create a GPO in this domain, and Link it here**
3. Name it: `Set Desktop Wallpaper`

OR

If you want to apply it domain-wide:

* Right-click on the domain → **Create GPO and Link**

---

### ✅ **Step 4: Configure the GPO Settings**

1. Right-click the GPO → Click **Edit**
2. Go to:

   ```
   User Configuration
   → Policies
   → Administrative Templates
   → Desktop
   → Desktop
   ```
3. Find and **double-click**:
   `Desktop Wallpaper`
4. Set to:

   * **Enabled**
   * Wallpaper Name: `\\DC01\Wallpapers\default.jpg`
   * Wallpaper Style: `Fill` (or `Stretch`, `Center`, etc.)
5. Click **Apply** and **OK**

---

### ✅ **Step 5: Force Group Policy Update**

You can wait for auto-refresh (90 min) or force it manually:

#### On client machine:

```powershell
gpupdate /force
```

---

### ✅ **Step 6: Verify**

* Log in as a domain user
* Check the desktop wallpaper has changed
* If not:

  * Ensure image path is accessible
  * Check GPO is linked to the correct OU
  * Run `gpresult /r` on the client to see applied policies

---

## 📌 Notes

| Item            | Description                                     |
| --------------- | ----------------------------------------------- |
| Image Format    | Best to use `.jpg` or `.bmp`                    |
| File Location   | Use UNC path (e.g., `\\Server\Share\image.jpg`) |
| GPO Scope       | Can apply to users or computers                 |
| Wallpaper Style | `Fill`, `Stretch`, `Center`, `Fit`, `Tile`      |
| Permissions     | Shared folder must be readable by domain users  |

---

## ✅ Optional: Prevent Users from Changing Wallpaper

Add this to the same GPO:

```
User Configuration → Administrative Templates → Control Panel → Personalization → Prevent changing desktop background → Enabled
```

---
