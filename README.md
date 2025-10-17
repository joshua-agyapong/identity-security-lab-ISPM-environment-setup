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

<img width="3839" height="1543" alt="Screenshot 2025-10-17 042516" src="https://github.com/user-attachments/assets/ddcf9de9-d68c-47a3-a42a-44d11168771d" />
png)

<img width="1633" height="1496" alt="Screenshot 2025-10-17 052747" src="https://github.com/user-attachments/assets/ddfe68ca-f472-4cc9-ae2a-8d51b5c110ff" />

---

## B) Enable API Integration (Microsoft Graph)

1. Open the new **Microsoft 365** app in Okta  
2. **Provisioning → Integration → Configure API Integration**  
3. Check **Enable API Integration**  
4. **Authenticate with Microsoft 365** → sign in as **Entra Global Administrator**  
5. **Accept** the consent screen


<img width="3771" height="1608" alt="Screenshot 2025-10-17 053557" src="https://github.com/user-attachments/assets/0ad719ea-5f4d-4b5a-8aaf-e3bc56bc8dec" />

<img width="3829" height="1825" alt="Screenshot 2025-10-17 053214" src="https://github.com/user-attachments/assets/85aa5e4a-d7c6-4340-b163-cc22b40d0345" />

**Result:** Okta now has Graph API permissions to manage Entra users.

---

## C) Turn on Provisioning Features (To App)

1. **Provisioning → To App → Edit**  
2. Enable: **Create Users**, **Update User Attributes**, **Deactivate Users**  
3. **Save**

**Result:** Lifecycle actions will sync from Okta into Entra.

![Provisioning – To App Toggles](images/okta_prov_toapp_toggles.png)

---

## D) Configure User Matching and Mappings (important)

1. **Provisioning → To App → Attribute Mappings**  
2. Map **Okta `userName` → Entra `userPrincipalName` (UPN)**  
3. Optional: **Okta `primaryEmail` → `mail`**  
4. Map **givenName**, **familyName**, **displayName** as needed  
5. **Save Mappings**

**Tip:** If your UPN domain differs, add a transformation to append `@yourtenant.onmicrosoft.com`.

**Result:** Okta knows how to populate Entra fields correctly.

![Attribute Mappings](images/okta_attribute_mappings.png)

---

## E) (Optional) Assign Licenses via Okta

1. App **General → Licenses** (if available)  
2. Select an M365 license SKU → **Save**

**Result:** Users can get a Microsoft 365 license during provisioning.

---

## F) Assign Who Gets Provisioned

1. **Assignments** tab → **Assign → Assign to Groups**  
2. Select **All-Employees** (or pick test users) → **Assign → Done**

**Result:** Okta starts provisioning those identities into Entra.

---

## G) Force a Provisioning Push (quick test)

1. **Provisioning → To App**  
2. **Force Sync** or **Refresh App Users** (if shown)  
3. Wait **1–5 minutes**

**Result:** New accounts appear in **Entra ID → Users**.

---

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

## K) Common Errors and Quick Fixes

- **User not created:** UPN domain mismatch → fix mapping to **userPrincipalName**  
- **No license:** Assign license SKU in app or in M365 admin center  
- **Stuck “Pending”:** Click **Force Sync**, then refresh Entra Users  
- **Wrong user matched:** Match on **UPN** or **email** consistently  
- **Consent failed:** Re-run **Authenticate with Microsoft 365** as Global Admin

---

## 📸 Screenshot Checklist (for your repo)

- Okta **Provisioning → Integration** (API enabled)  
- Okta **Provisioning → To App** (three toggles on)  
- Okta **Attribute Mappings** screen  
- Entra **Users** list showing the three users  
- Entra **User → Profile** with attributes populated  
- Okta **View Logs** showing “User Created”

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
