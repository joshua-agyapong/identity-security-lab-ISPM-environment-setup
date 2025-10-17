# 🧩 Module 1 – Environment Setup (Identity Security Hygiene Lab)

## 📘 Project Overview
This module establishes a mini enterprise environment for **Identity Security Posture Management (ISPM)** training.  
It integrates **Okta** (as the Identity Provider) and **Microsoft Entra ID** (as the cloud directory) to simulate how identity data flows, how hygiene issues appear, and how remediation begins.

---

## ⚙️ Lab Objectives
✅ Configure Okta and Entra ID tenants  
✅ Create and group sample users  
✅ Enable automatic provisioning from Okta → Entra ID via Microsoft Graph  
✅ Simulate identity hygiene issues (inactive user, admin without MFA)  
✅ Export identity data for ISPM analysis  

---

## 🏗️ Environment Architecture

| Component | Purpose |
|------------|----------|
| **Okta Developer Org** | Primary Identity Provider and provisioning source |
| **Microsoft 365 Developer Tenant (Entra ID)** | Cloud directory target for synchronization |
| **Local Lab Folder (C:\\Labs)** | Stores exported identity datasets |
| **Groups:** Admins-Global / All-Employees | Represent common enterprise roles |

![Architecture Diagram](images/okta_m365_integration.png)
*Okta ↔ Microsoft 365 Integration using Microsoft Graph API*

---

## 🧱 Step-by-Step Implementation

### 1️⃣ Create Tenants
- Register **Okta Developer Org** → [developer.okta.com](https://developer.okta.com/)  
- Create **Microsoft 365 Developer Tenant** → [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program)

### 2️⃣ Add Users and Groups in Okta
| User | Department | Notes |
|------|-------------|-------|
| **Alice Admin** | IT | Admin privileges, MFA disabled |
| **Bob Analyst** | Finance | Standard user |
| **Charlie Contractor** | Vendor | Suspended (inactive) |

Groups created:  
`Admins-Global`, `All-Employees`

![Okta Users](images/okta_users.png)
*User directory and group membership in Okta*

### 3️⃣ Configure Okta → Microsoft 365 Integration
- Add **Microsoft 365 App** from Okta Integration Network  
- Enable provisioning via **Microsoft Graph API**  
- Turn on Create/Update/Deactivate options  
- Assign **All-Employees** group for automatic provisioning  
- Verify new users appear in **Entra ID → Users**

![Entra Users](images/entra_users.png)
*Users synced to Entra ID through Okta provisioning*

### 4️⃣ Simulate Identity Hygiene Issues
- Suspend *Charlie Contractor* to represent inactive account  
- Leave *Alice Admin* without MFA and in broad group to mimic real risks

### 5️⃣ Export Data Sources
- Okta → Reports > People > Export CSV → `Okta_Users.csv`  
- Entra ID → Users > Download CSV → `Entra_Users.csv`  
- Store both in `C:\Labs\`

![Export Files](images/export_files.png)
*Local data exports used as ISPM data sources*

---

## 🗂️ Deliverables

