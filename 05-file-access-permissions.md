# 05 – File Access Permission Issue

---

## Lab Setup

To simulate a real-world file access scenario, I first configured a basic department based folder structure in my domain lab environment.

### 1. Created Department Folders

On the file server:

C:\Departments

Created folders:
- Finance
- Marketing
- Sales

<img width="617" height="298" alt="image" src="https://github.com/user-attachments/assets/370a1996-9a23-4089-b484-dd21936d8817" />


---

### 2. Created Organizational Unit (OU)

In Active Directory Users and Computers:

Created an OU named:

Departments

---

### 3. Created Security Groups

Inside the Departments OU, created the following security groups:

- FINANCE (Security Group)
- MARKETING (Security Group)
- SALES (Security Group)

Scope: Global  
Type: Security  

<img width="859" height="356" alt="image" src="https://github.com/user-attachments/assets/ef548540-77a2-400a-8368-77b891bcbcaf" />


---

### 4. Added Users to Security Groups

Added test users to their respective department groups.

Example:
- Added my test user to the SALES security group.

This allows group based permission management instead of assigning permissions directly to individual users.

<img width="394" height="453" alt="image" src="https://github.com/user-attachments/assets/44fb5945-3fcc-4246-b568-4cd447cb7d41" />


---

### 5. Configured Folder Permissions

For each department folder:

Right-click folder → Properties → Sharing 

Granted each security group access only to its corresponding folder.

Example:

Sales folder:
- SALES group → Read 

Finance folder:
- FINANCE group → Read

Marketing folder:
- MARKETING group → Read

Result:
Members of each department group can access only their assigned folder and not others.

<img width="602" height="301" alt="image" src="https://github.com/user-attachments/assets/0eecc78e-59bc-46e3-b9d8-29415742dd17" />


---

## Ticket overview

**User issue:**  
User reports they cannot access the Sales department shared folder.  
When attempting to open the folder, they receive an access denied message.

**Priority:**  
Medium  

**Impact:**  
User unable to access department resources required for daily work.

<img width="1441" height="605" alt="image" src="https://github.com/user-attachments/assets/6844ce26-f79a-41fd-80b6-ae2dd2d97a46" />


---

## Initial triage

- Verified user identity  
- Confirmed issue is isolated to Sales folder only  
- Confirmed folder permissions are assigned via security group  
- Confirmed other Sales users can access the folder  
- Suspected group membership issue  

---

## Investigation

### Step 1 — Verify folder permissions
Checked folder security settings and confirmed access is granted to:

**Sales security group**

Permissions were configured correctly.

---

### Step 2 — Check user group membership
Opened Active Directory Users and Computers.

Reviewed membership of Sales security group.

Observed:

➡ User was NOT a member of the Sales group

This explains why access was denied.

<img width="399" height="457" alt="image" src="https://github.com/user-attachments/assets/dd970d46-cefd-4aa7-9291-8f97798775eb" />


---

### Step 3 — Confirm with department owner
Verified with the responsible party whether the removal was intentional.

Confirmed removal was accidental.

---

## Root cause

User was not a member of the Sales security group that controls access to the Sales folder.

Because access is group based, the user inherited no permissions.

---

## Resolution

### Step 1 — Restore proper group membership
Added user back to Sales security group in Active Directory.

---

### Step 2 — Verify access
User reopened Sales folder.

Access restored successfully.

User able to open files and work normally.

<img width="687" height="358" alt="image" src="https://github.com/user-attachments/assets/705f06ac-430d-44e8-af1a-6b585f936376" />


---

## Verification

- User can open Sales folder  
- User can view and access files  
- No access errors remain  

Issue resolved.
