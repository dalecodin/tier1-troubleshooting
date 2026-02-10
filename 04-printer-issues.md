# Printer Troubleshooting Workflow Summary

## Preface

To demonstrate printer troubleshooting skills for IT support scenarios, I created this summary based on my research on printer troubleshooting. I don’t own a printer  to make a project, so this document captures the core troubleshooting workflow, diagnostic steps, and resolution methods . The goal is to show printer troubleshooting knowledge and process, not just single fixes. 


## 1. USB or Network Printer

Figure out how the printer is connected.

Open:
Control Panel → Devices and Printers → Printer Properties → Ports tab

Check port type:
- USB → local printer
- TCP/IP address → network printer
- WSD → auto-discovered network printer
- \\PrintServer\PrinterName → print server shared printer

Troubleshooting depends on which type.

---

## 2. USB Printer Troubleshooting

Goal: Confirm the computer sees the printer and has a good driver.

Steps:
- Restart computer
- Try different USB ports
- Open Device Manager
- Check if printer appears under devices / USB
- Update or reinstall driver

---

## 3. Network Printer — Connectivity Check

Goal: Verify the PC can reach the printer on the network.

Steps:
- Find printer IP from Ports tab
- Open Command Prompt
- Run ping <printer IP>
- If ping fails:
  - verify user network (Wi-Fi vs wired vs wrong network)
  - confirm printer IP from printer network config 
- Compare printer IP settings:
  - subnet mask
  - default gateway
  - DNS
- Make sure printer is on same subnet as PC
- Access printer embedded web page via browser using printer IP


---

## 4. Print Server Printers

If printer is shared from a print server:

It appears as:
\\PrintServerName\PrinterName

Troubleshooting steps:
- Test printing from another PC
- If others work → user/PC specific issue
- If nobody works → server-side issue
- Log into print server
- Open Print Management
- Check printer properties, port, queue, status
- Verify printer IP is still correct on server

---

## 5. Driver Verification (USB or Network)

Always make sure the driver matches printer model.

Check:
Printer Properties → Advanced → Driver

- Use vendor driver
- Avoid wrong model driver
- Replace generic driver when possible
- Reinstall driver if corruption suspected

---

## 6. Physical Printer Checks

If software and network checks pass:

Check hardware:
- paper loaded
- toner/ink level
- jams
- error codes
- offline status
- printer display messages

Test:
- printer test page
- vs document print
- vs app-specific print

---

## Core Helpdesk Printer Method

Always isolate:

- USB vs Network
- User vs All users
- PC vs Printer vs Server
- Driver vs Port vs IP vs Queue
- Logical vs Physical problem
