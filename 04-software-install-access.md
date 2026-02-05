# 04 – Software Installation / Access Request

## Ticket overview

Jane Smith from the Finance department reported that she needed SQL Server installed on her workstation in order to perform her job duties. When she attempted to install the software herself, the system prompted her for administrator credentials and would not allow the installation to continue.

Jane is using a Windows 10 client device named CLIENT-1 which is joined to the domain `mydomain.com` and she is logged in using the account `MYDOMAIN\jane`.

---

## User issue

"I need SQL Server installed for my work, but it won’t let me install it and asks for admin credentials."

---

## Initial triage

I verified the user’s identity and confirmed that the issue was isolated to a single device. Jane was logged in correctly and the system itself was functioning normally.

I confirmed that Jane’s account is a standard domain user and does not have local administrator privileges on the machine.

---

## Troubleshooting process

Jane attempted to download SQL Server directly from the Microsoft website and launch the installer. When the installer was opened, Windows displayed a User Account Control prompt requesting administrative credentials.

This indicated that SQL Server requires elevated permissions and cannot be installed by a standard user account.

To proceed, I remotely connected to Jane’s workstation from the domain controller using Remote Desktop.

I re-ran the SQL Server installer, and when prompted by UAC, I entered IT administrator credentials using the account `MYDOMAIN\john.admin`.

---

## Root cause

The user account did not have sufficient privileges to install system-level software. Enterprise applications such as SQL Server require administrative access for installation.

---

## Resolution

SQL Server was installed successfully using IT administrator credentials while connected to the user’s workstation. No changes were made to Jane’s permission level.

---

## Verification

After the installation completed, SQL Server was launched and verified to be working correctly. Jane confirmed that she was able to access the application and continue with her work.

---

## Resolution summary

The issue was caused by restricted user permissions. The software was installed by IT using administrative credentials, following standard enterprise security practices.

---

## Notes

This is a common helpdesk scenario in corporate environments. Users typically do not have administrative access, and IT installs required software on their behalf to maintain system security and prevent unauthorized changes.
