# identity-security-lab-ISPM-environment-setup
Environment Setup (Identity Security Hygiene Lab)
# Module 1 – Environment Setup (Identity Security Hygiene Lab)

## Objective
Set up a small enterprise-style IAM environment to support Identity Security Posture Management (ISPM) activities using **Okta** and **Microsoft Entra ID**.

## Overview
This module establishes the foundation for identity hygiene analysis by integrating Okta and Entra ID.  
It mirrors a real corporate IAM setup where Okta acts as the identity source and Entra ID manages downstream resources.

---

## Steps Performed

### 1. Create Tenants
- Registered a **free Okta Developer Org** at [developer.okta.com](https://developer.okta.com/).  
- Created a **Microsoft 365 Developer Tenant** (includes Entra ID) via the [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program).

### 2. Build User Directory
Added three sample users in Okta:  
| Name | Department | Notes |
|------|-------------|-------|
| **Alice Admin** | IT | Admin privileges, MFA disabled |
| **Bob Analyst** | Finance | Standard user |
| **Charlie Contractor** | Vendor | Suspended (inactive) |

Groups created:  
- `Admins-Global`  
- `All-Employees`

### 3. Configure Integration (Okta → Microsoft 365)
- Added the **Microsoft 365 App** in Okta.  
- Enabled provisioning through **Microsoft Graph API** (create, update, deactivate).  
- Assigned group `All-Employees` for automatic user creation in Entra ID.  
- Verified new users appeared under **Entra ID → Users**.

### 4. Simulate Hygiene Issues
- Suspended *Charlie Contractor* to represent an inactive account.  
- Left *Alice Admin* without MFA and with broad group access to simulate common risks.

### 5. Export Data Sources
- **Okta:** Reports → People → Export CSV → `Okta_Users.csv`  
- **Entra ID:** Users → Download Users → `Entra_Users.csv`  
- Stored files in `C:\Labs\`.

---

## Deliverables
