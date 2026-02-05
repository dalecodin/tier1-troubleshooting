# 04 – Software Install Access (Admin Required)

## Ticket overview

![ticket-screenshot](ADD_IMAGE_HERE)

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

From the domain controller, opened Remote Desktop and connected to the user’s client machine.

![rdp](ADD_IMAGE_HERE)

---

### Step 2: Download installer from Microsoft

Opened a browser on the user PC, navigated to the Microsoft SQL Server download page, and downloaded the installer.

![download](ADD_IMAGE_HERE)

---

### Step 3: Approve with admin credentials

When the installer triggered the UAC prompt, entered domain admin credentials to allow the installation to proceed.

![uac](ADD_IMAGE_HERE)

---

### Step 4: Complete installation

Finished the installation process and confirmed setup completed successfully.

![install-finished](ADD_IMAGE_HERE)

---

## Root cause

Software installation required administrator privileges that the standard user account does not have.

---

## Resolution summary

Remoted into the user machine from the domain controller, downloaded the installer, approved elevation with admin credentials, and completed the installation successfully.
