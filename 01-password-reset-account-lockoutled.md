# Ticket 01: Password Reset / Account Lockout

## Ticket overview

<img width="1919" height="1079" alt="Pasted image 20260112085321" src="https://github.com/user-attachments/assets/534dadc0-e563-4c6d-8eab-b2daa562b7ed" />



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

<img width="850" height="374" alt="Pasted image 20260117114651" src="https://github.com/user-attachments/assets/91e8985a-85ba-4635-a331-aada498d7374" />



## Step 2: Unlock account
Unlocked the user account in Active Directory

```powershell
Unlock-ADAccount -Identity jsmith01
```

Or you can use the GUI

<img width="413" height="538" alt="Pasted image 20260117114819" src="https://github.com/user-attachments/assets/2827ddee-3fcf-4447-aa7d-319ecf705486" />


## Step 3: Reset password

Reset the password per security policy and required password change at next login
Temporary password communicated securely to the user

```powershell
Set-ADAccountPassword -Identity jsmith01 -Reset
```

<img width="711" height="97" alt="Pasted image 20260117115140" src="https://github.com/user-attachments/assets/f60dd370-d608-4977-8105-4b26da182256" />


<img width="375" height="114" alt="Pasted image 20260117115259" src="https://github.com/user-attachments/assets/5b336bba-fe93-4a89-a2d5-f88654591505" />


## Step 4: Document and Close the ticket


<img width="1263" height="229" alt="Pasted image 20260117120157" src="https://github.com/user-attachments/assets/bffc8a3c-1de8-4355-b064-ed4fa2d36ecd" />


---

## Root cause
- Multiple incorrect password attempts triggered the account lockout policy.

## Resolution
- Account unlocked
- Password reset completed
- User successfully logged in and confirmed access


