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

https://github.com/joshua-agyapong/identity-security-lab-ISPM-environment-setup/blob/6a77391c09a3ce25a5410df88c8409ea9cd96e52/Screenshot%202025-10-17%20030139.png

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
