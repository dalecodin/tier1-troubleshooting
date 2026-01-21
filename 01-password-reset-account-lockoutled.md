# Ticket 01: Password Reset / Account Lockout

## Ticket overview

![[Pasted image 20260112085321.png]]

**User issue:**  
“I put my password in wrong too many times and now I'm locked out.”

**Priority:**  
Medium

**Impact:**  
User unable to access workstation and email.

---

## Initial triage
- Verified user identity
- Confirmed account lockout error
- Confirmed issue affects login to multiple services

 Found out her Active Directory identity is ``jsmith01``

---

## Step 1: Check account status
Confirmed the account was locked due to multiple failed login attempts

```powershell
Get-ADUser jsmith01 -Properties LockedOut, PasswordExpired
```

![[Pasted image 20260117114651.png]]


## Step 2: Unlock account
Unlocked the user account in Active Directory

```powershell
Unlock-ADAccount -Identity jsmith01
```

Or you can use the GUI

![[Pasted image 20260117114819.png]]

## Step 3: Reset password

Reset the password per security policy and required password change at next login
Temporary password communicated securely to the user

```powershell
Set-ADAccountPassword -Identity jsmith01 -Reset
```

![[Pasted image 20260117115140.png]]

![[Pasted image 20260117115259.png]]

## Step 4: Document and Close the ticket


![[Pasted image 20260117120157.png]]

---

## Root cause
- Multiple incorrect password attempts triggered the account lockout policy.

## Resolution
- Account unlocked
- Password reset completed
- User successfully logged in and confirmed access


