# 03 – Software Install Access (Admin Required)

## Ticket overview

<img width="1918" height="611" alt="image" src="https://github.com/user-attachments/assets/52a72711-5905-498a-974a-b3aa4881b062" />


**User issue:**  
User needs SQL Server installed but cannot install it due to admin permission prompt.

**Priority:**  
Medium

**Impact:**  
User cannot proceed with required software setup without IT assistance.

---

## Initial triage

- Verified user identity
- Confirmed request is for software installation
- Confirmed user is standard domain account
- Confirmed installer requires admin elevation

---

## Resolution process

### Step 1: Remote into user PC from Domain Controller

From my homelab Domain Controller VM, I opened Remote Desktop and connected to my client VM to simulate a helpdesk support session.

`<img width="400" height="492" alt="image" src="https://github.com/user-attachments/assets/24183bfb-4007-4a83-82ab-35425ea819b0" />


---

### Step 2: Download installer from Microsoft

Opened a browser on the user PC, navigated to the Microsoft SQL Server download page, and downloaded the installer.

<img width="1628" height="854" alt="image" src="https://github.com/user-attachments/assets/17a2e226-c66a-46e0-910e-8a4262f92a53" />


---

### Step 3: Approve with admin credentials

When the installer triggered the UAC prompt, entered domain admin credentials to allow the installation to proceed.

<img width="453" height="500" alt="image" src="https://github.com/user-attachments/assets/c8d11c9e-5170-43c0-bace-015c35ec9953" />


---

### Step 4: Complete installation

Finished the installation process and confirmed setup completed successfully.

<img width="846" height="674" alt="image" src="https://github.com/user-attachments/assets/1e06e227-2af5-4e1b-9373-685f417ff808" />


---

## Root cause

Software installation required administrator privileges that the standard user account does not have.

---

## Resolution summary

Remoted into the user machine from the domain controller, downloaded the installer, approved elevation with admin credentials, and completed the installation successfully.



