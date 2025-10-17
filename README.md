# 🧩 Module 1 — Environment Setup and Identity Provisioning (Identity Security Hygiene Lab)

## 📘 Project Goal
Establish a functional identity environment that supports **Identity Security Posture Management (ISPM)** operations.  
This module focuses on **directory configuration, identity provisioning, and data source preparation** between **Okta** and **Microsoft Entra ID** to enable lifecycle and hygiene monitoring.

---

## 🎯 Objectives
- Configure primary and secondary identity directories  
- Perform user provisioning from Okta → Entra ID  
- Establish role-based groups and simulate common identity hygiene issues  
- Export identity data for analysis in later modules  

---

## ⚙️ Tools and Platforms
| Tool | Purpose |
|------|----------|
| **Okta Developer Org** | Identity Provider and provisioning source |
| **Microsoft 365 Developer Tenant (Entra ID)** | Cloud directory and application target |
| **Microsoft Graph API** | Interface used by Okta for automated provisioning |
| **Local Folder (C:\\Labs)** | Stores exported identity data and documentation |

---

## 🏗️ Step 1 — Configure Identity Platforms
**Action:**  
- Registered a **free Okta Developer Org** at [developer.okta.com](https://developer.okta.com).  
- Created a **Microsoft 365 Developer Tenant** (includes Entra ID) via the [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program).  

**Result:**  
Two active tenants ready for integration — Okta as the source, Entra ID as the target directory.

---

## 👥 Step 2 — Create Identities in Okta Directory
**Action:**  
Added three identities within Okta (**Directory → People → Add Person**):

| User | Department | Role/Notes |
|------|-------------|------------|
| **Alice Admin** | IT | Administrator (MFA disabled) |
| **Bob Analyst** | Finance | Standard user |
| **Charlie Contractor** | Vendor | Suspended (inactive) |

![Image Alt](https://github.com/joshua-agyapong/identity-security-lab-ISPM-environment-setup/blob/6a77391c09a3ce25a5410df88c8409ea9cd96e52/Screenshot%202025-10-17%20030139.png)

**Result:**  
Base user population created in the Okta directory for provisioning and lifecycle testing.

---

## 🧩 Step 3 — Establish Group Structure
**Action:**  
Created two groups under **Directory → Groups**:
- `Admins-Global`  
- `All-Employees`

Assigned:
- Alice → *Admins-Global* and *All-Employees*  
- Bob → *All-Employees*  
- Charlie → *All-Employees*
<img width="1906" height="1504" alt="image" src="https://github.com/user-attachments/assets/9e04b1e9-01a5-4f75-a208-022258e7f335" />
<img width="3839" height="1543" alt="image" src="https://github.com/user-attachments/assets/d0461d94-bff7-439c-954a-2818ded7f6df" />
<img width="3827" height="1369" alt="image" src="https://github.com/user-attachments/assets/e3717981-d609-4257-a74c-8b5629e7d271" />
<img width="3839" height="1585" alt="image" src="https://github.com/user-attachments/assets/394fded1-06a0-4a54-bbed-c5c9dce62d5c" />


**Result:**  
Defined baseline role-based access model, supporting privilege and membership management.

---

## 🔗 Step 4 — Configure Okta → Entra ID Provisioning Integration
**Action:**  
1. In Okta, added the **Microsoft 365 App** from the Integration Network.  
2. Enabled **API Integration** using Microsoft Graph.  
3. Turned on:  
   - *Create Users*  
   - *Update User Attributes*  
   - *Deactivate Users*  
4. Assigned group **All-Employees** to the application for automatic provisioning.

# Okta → Entra ID Provisioning (Microsoft Graph) — Step 4

This guide shows how to configure **Okta** to provision identities into **Microsoft Entra ID** using **Microsoft Graph**.  
---
## ✅ Outcome
- Okta can **create**, **update**, and **deactivate** users in **Entra ID**.
- This delivers **“Configure ISPM tool data sources and integrations.”**

---

## A) Add the Microsoft 365 app in Okta

1. Okta Admin → **Applications → Applications**  
2. **Browse App Catalog** → search **“Microsoft 365”** (aka *Office 365*)  
3. **Add Integration** → keep defaults → **Done**

**Result:** The Microsoft 365 app appears in Okta.

<img width="3832" height="850" alt="image" src="https://github.com/user-attachments/assets/483a987e-2eda-4834-bd41-1f35462df50b" />
<img width="3835" height="1146" alt="image" src="https://github.com/user-attachments/assets/1fd5289c-3533-4be8-9f46-48fb9a03e7c6" />
<img width="3838" height="1368" alt="image" src="https://github.com/user-attachments/assets/57ee43de-e462-49ed-9f79-6fb6a871f432" />
<img width="3832" height="1392" alt="image" src="https://github.com/user-attachments/assets/214e5bb9-cfbe-45b0-8c31-113c11fd278c" />



<img width="1609" height="1551" alt="Screenshot 2025-10-17 052311" src="https://github.com/user-attachments/assets/ab3fe170-b5d3-4870-b390-c2fe374ee68f" />

<img width="1633" height="1496" alt="Screenshot 2025-10-17 052747" src="https://github.com/user-attachments/assets/ddfe68ca-f472-4cc9-ae2a-8d51b5c110ff" />

---

## B) Enable API Integration (Microsoft Graph)

1. Open the new **Microsoft 365** app in Okta  
2. **Provisioning → Integration → Configure API Integration**  
3. Check **Enable API Integration**  
4. **Authenticate with Microsoft 365** → sign in as **Entra Global Administrator**  
5. **Accept** the consent screen
   
<img width="3832" height="1392" alt="image" src="https://github.com/user-attachments/assets/d7e76513-57d6-467b-b4e2-b58246f80e96" />

<img width="3771" height="1608" alt="Screenshot 2025-10-17 053557" src="https://github.com/user-attachments/assets/0ad719ea-5f4d-4b5a-8aaf-e3bc56bc8dec" />

<img width="3829" height="1825" alt="Screenshot 2025-10-17 053214" src="https://github.com/user-attachments/assets/85aa5e4a-d7c6-4340-b163-cc22b40d0345" />

<img width="3839" height="2083" alt="Screenshot 2025-10-17 053220" src="https://github.com/user-attachments/assets/9ecd8e30-8c70-4896-aaa6-2c5315f07965" />

**Result:** Okta now has Graph API permissions to manage Entra users.

---

## C) Turn on Provisioning Features (To App)

1. **Provisioning → To App → Edit**  
2. Enable: **Create Users**, **Update User Attributes**, **Deactivate Users**  
3. **Save**

<img width="3777" height="1671" alt="image" src="https://github.com/user-attachments/assets/56482a39-77a4-437a-93d8-1cfe2ea9448e" />
<img width="3839" height="2004" alt="image" src="https://github.com/user-attachments/assets/de5fb4f4-bd46-45e2-8140-0fe19d0c4406" />
<img width="3832" height="1843" alt="image" src="https://github.com/user-attachments/assets/ed9e6834-9dc4-433a-bbfc-e5d958751a93" />



**Result:** Lifecycle actions will sync from Okta into Entra.

![Provisioning – To App Toggles](images/okta_prov_toapp_toggles.png)

## E) (Optional) Assign Licenses via Okta
1. Open **Applications → Microsoft Office 365 (Microsoft Graph API integration)**  
2. Go to **General → Licenses** *(if available in your tenant)*  
3. Select a license SKU (e.g., **Exchange Online Plan 1**)  
4. Click **Save**
   ( I DIDN'T ASSIGN LICENSES YET )
   
**Result:** Users can receive a Microsoft 365 license during provisioning.

> Tip: If you don’t see license options, assign licenses in the Microsoft 365 Admin Center instead.

---

## F) Assign Who Gets Provisioned
1. Open the app → **Assignments** tab  
2. Click **Assign → Assign to Groups** (recommended) or **Assign to People**  
3. Select your group (e.g., **All-Employees**) → **Assign**  
<img width="3834" height="1482" alt="image" src="https://github.com/user-attachments/assets/5f374262-fed6-458a-add5-0c866b9e6a48" />

4. **Save and Go Back → Done**

**Result:** Okta starts provisioning all members of that group to Entra ID.

---

## G) Force a Provisioning Push (Quick Test)
1. Go to **Provisioning → To App**  
2. Click **Force Sync** (or **Refresh App Users** if present)  
3. Wait **1–5 minutes** and refresh the Entra Users list

   (SKIPPED THIS , I DIDN'T HAVE TO DO THAT IN MY SITUATION)
   
**Result:** New accounts appear in **Azure Portal → Microsoft Entra ID → Users**.

---

## 🔍 Optional: Verify in Shell
Use **Microsoft Graph PowerShell** to confirm the users exist in Entra.

```powershell
# Install once:
# Install-Module Microsoft.Graph -Scope CurrentUser

Import-Module Microsoft.Graph.Users
Connect-MgGraph -Scopes "User.Read.All"

# Replace with your tenant domain (the verified one)
$domain = "playjtech.onmicrosoft.com"

# Look up the three test users
$names = @("alicerafa", "bobsmith", "charliedion")
foreach ($n in $names) {
    $upn = "$n@$domain"
    try {
        $u = Get-MgUser -UserId $upn -ErrorAction Stop
        "{0}  |  {1}  |  Enabled={2}" -f $u.DisplayName, $u.UserPrincipalName, $u.AccountEnabled
    } catch {
        "NOT FOUND  |  $upn"
    }
}
```

---

## 🧯 Common Issues (Fast Fixes)
- **Users not created** → Check `userPrincipalName` mapping and domain (must be a **verified** domain, e.g., `@tenant.onmicrosoft.com`)  
- **No license applied** → Assign in Okta **or** M365 Admin Center  
- **Still pending** → Click **Force Sync** and wait a few minutes  
- **Errors** → App → **Provisioning → View Logs** (details show the failing attribute/domain)

---

## 📸 Screenshot Checklist
- `okta_general_licenses.png` — App **General → Licenses**  
- `okta_assign_group.png` — **Assignments** with the group selected  
- `okta_force_sync.png` — **Provisioning → To App** (Force Sync)  
- `entra_users_after_sync.png` — **Entra ID → Users** showing provisioned accounts

## H) Verify in Entra ID

1. Azure Portal → **Microsoft Entra ID → Users**  
2. Search **Alice**, **Bob**, **Charlie**  
3. Open a user → confirm **User type = Member** and attributes look correct

**Result:** Users from Okta exist in Entra.

![Entra – Users List](images/entra_users_list.png)
![Entra – User Profile](images/entra_user_profile.png)

---

## I) Test Deprovisioning (leaver flow)

1. Okta → **Directory → People → Charlie**  
2. **More Actions → Suspend**  
3. Wait **2–5 minutes**  
4. Entra **Users → Charlie** → confirm **Block sign-in = Yes** (or account disabled)

**Result:** Deprovisioning works end-to-end.

---

## J) Check Okta Provisioning Logs

1. App → **Provisioning → View Logs**  
2. Look for **User Created / Updated / Deactivated**  
3. Click any entry to see Graph call details

**Result:** Evidence for audits and troubleshooting.

![Okta – View Logs (User Created)](images/okta_view_logs_user_created.png)

---

##  Common Errors and Quick Fixes
The error faced was that the domains didn't match with my Entra ID domain. I changed the users' emails to match it
Before that, I unassigned the group and re-assigned it after fixing the issue 

---

### Notes
- This flow is **provisioning (lifecycle)** via Graph, not SAML/OIDC.  
- Add SSO later if needed; it’s a separate configuration.


**Result:**  
Automatic provisioning established — Okta can now create, update, and deactivate Entra ID accounts via Microsoft Graph.

---

## ✅ Step 5 — Verify Identity Provisioning in Entra ID
**Action:**  
Opened **Microsoft Entra ID → Users** to confirm user synchronization.

<img width="3820" height="1264" alt="image" src="https://github.com/user-attachments/assets/0160887b-04b8-4479-9ed2-cd8754aa8b0a" />


**Result:**  
All three Okta users successfully provisioned into Entra ID as *Members*.  
Lifecycle automation confirmed between Okta and Entra ID.

---

## 🔒 Step 6 — Simulate Identity Hygiene Conditions
**Action:**  
- Suspended *Charlie Contractor* in Okta to represent an inactive identity.  
- Left *Alice Admin* without MFA and within a broad group (*All-Employees*) to simulate privilege risk.

**Result:**  
Environment seeded with realistic hygiene defects for ISPM analysis:  
inactive user / missing MFA / over-privileged admin.

---

## 🧾 Step 7 — Export ISPM Data Sources
**Action:**  
- Okta → Reports → People → Export CSV → `Okta_Users.csv`  
- Entra ID → Users → Download CSV → `Entra_Users.csv`  
- Stored both under `C:\Labs\`.

**Result:**  
Baseline identity datasets collected for integration into the ISPM analysis pipeline (Module 2).

---

## 🗂️ Deliverables
