# 🔐 AMTECHLab — Microsoft Entra & M365 Security Lab

> Identity & Access Management | Monitoring & Alerting  
> Tenant: `AMTECHLab.onmicrosoft.com`

---

## 🧰 Prerequisites

- Access to [entra.microsoft.com](https://entra.microsoft.com) as Global Administrator
- Microsoft 365 Business Premium trial (active)

---

## 👥 Lab Users

| User | Email | License |
|------|-------|---------|
| Alice Adams | alice@AMTECHLab.onmicrosoft.com | M365 Business Premium |
| Bob Baker | bob@AMTECHLab.onmicrosoft.com | Unlicensed |
| Carol Chen | carol@AMTECHLab.onmicrosoft.com | M365 Business Premium |
| Jamie Randle | jamie.randle@AMTECHLab.onmicrosoft.com | Unlicensed |
| Pablo Marquez | pablo.marquez@AMTECHLab.onmicrosoft.com | Unlicensed |
| support | support@AMTECHLab.onmicrosoft.com | Unlicensed |
| Tracy Dalhousie | tracy.dalhousie@AMTECHLab.onmicrosoft.com | Unlicensed |

<img width="943" height="303" alt="1 user-list" src="https://github.com/user-attachments/assets/ed91bb57-4b7e-4322-8e07-bfa466e4f7d7" />


---

## 🔷 Part 1 — Microsoft Entra (`entra.microsoft.com`)

### Task 1 — Assign Roles (RBAC / Least Privilege)


**Steps:**
1. Sign in to [entra.microsoft.com](https://entra.microsoft.com)
2. Navigate to `Identity → Users`
3. Assign the following roles:

| User | Role | Reason |
|------|------|--------|
| Alice Adams | Security Reader | Read-only security visibility |
| Carol Chen | Helpdesk Administrator | Scoped IT support, no over-privilege |
| Jamie Randle | Guest Inviter | Minimal role, no license required |

<img width="1275" height="213" alt="2 Alice_assigned-role" src="https://github.com/user-attachments/assets/0c7ffe32-bb4a-4cd2-9590-850096264dae" />

<img width="1283" height="209" alt="3 Carol_assigned-role" src="https://github.com/user-attachments/assets/d7dd594a-7163-46e9-bb4a-253dd6c21815" />

<img width="1212" height="216" alt="4 Jamie_assigned-role" src="https://github.com/user-attachments/assets/a7e4786d-0927-4231-89a8-036b3b468ef4" />



4. For each user: click their name → **Assigned roles** → **+ Add assignment** → search and select the role → click **Add**


<img width="1613" height="101" alt="5 all_assigned-roles" src="https://github.com/user-attachments/assets/46688c79-8049-4be4-9ba3-09fd8de07725" />


---

### Task 2 — Disable the `support` Account

**Concept:** Accountability — shared/generic accounts cannot be tied to a single individual, violating audit and non-repudiation principles.

**Steps:**
1. Navigate to `Identity → Users → support`
2. Click **Edit properties** (pencil icon)
3. Under **Settings**, toggle **Block sign-in** to `Yes`
4. Click **Save**

> ✅ **Expected result:** `support@AMTECHLab.onmicrosoft.com` can no longer sign in.

> ⚠️ **Note:** In a real environment, shared accounts like `support` should be replaced with individual accounts and a shared mailbox.

---

### Task 3 — Review Sign-in Logs

**Concept:** Log analysis — identifying authentication events, failures, and conditional access results.

**Steps:**
1. Navigate to `Identity → Monitoring & health → Sign-in logs`
2. Filter by user: `alice@AMTECHLab.onmicrosoft.com`
3. Click any sign-in entry and review:
   - **Basic info** tab — IP address, location, client app used
   - **Conditional Access** tab — which policies applied and their result
4. Repeat for `carol@AMTECHLab.onmicrosoft.com`
5. Change filter to **Status: Failure** — note any failed attempts

> ✅ **Expected result:** You can identify where, when, and how users are signing in and whether any policies are enforcing controls.

---

## 🟠 Part 2 — M365 Admin Center (`admin.microsoft.com`)

### Task 4 — Create an Alert Policy for Role Assignments

**Concept:** Monitoring & alerting — detecting unauthorized privilege escalation.

**Steps:**
1. Sign in to [admin.microsoft.com](https://admin.microsoft.com)
2. Navigate to `Security → Alert policies`
3. Click **+ New alert policy**
4. Fill in:
   - **Name:** `Alert - Admin Role Assigned`
   - **Description:** Triggers when any user is added to a directory role
   - **Activity:** Added member to role
   - **Threshold:** Every time this activity occurs
   - **Recipients:** your admin email address
5. Click **Save**

> ✅ **Expected result:** You receive an email any time a user in AMTECHLab is assigned an admin role.

---

### Task 5 — Review Microsoft Secure Score

**Concept:** Risk management — understanding your current security posture and prioritizing improvements.

**Steps:**
1. Navigate to `Security → Microsoft Secure Score`
2. Review your current score
3. Click the **Recommended actions** tab
4. Find and read through these two actions (common for new tenants):
   - *Require MFA for all users*
   - *Block legacy authentication protocols*
5. Note what your score would be if you implemented them

> ✅ **Expected result:** You understand what Microsoft considers the highest-priority security gaps in your tenant.

---

## ✅ Completion Checklist

- [ ] Task 1 — Roles assigned to Alice, Carol, and Jamie
- [ ] Task 2 — `support` account blocked
- [ ] Task 3 — Sign-in logs reviewed for Alice and Carol
- [ ] Task 4 — Alert policy created for role assignments
- [ ] Task 5 — Secure Score reviewed and top actions noted

---

## 🔗 Resources

- [Microsoft Entra Admin Center](https://entra.microsoft.com)
- [Microsoft 365 Admin Center](https://admin.microsoft.com)
- [Entra ID Role Descriptions](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference)
- [Microsoft Secure Score](https://learn.microsoft.com/en-us/microsoft-365/security/defender/microsoft-secure-score)
