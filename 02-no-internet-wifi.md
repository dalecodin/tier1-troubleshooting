# 02 – No Internet / DNS Issue

## Ticket overview

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dfe3a2d1-3231-4485-91b4-bdea809cfab9" />


**User issue:**   
I’m not able to access the internet on my computer. Websites are not loading and I can’t connect to any online services even though my network shows as connected.

**Priority:**  
Medium

**Impact:**   
User unable to perform web based tasks.

---

## Initial triage  
- Verified user identity  
- Confirmed issue isolated to a single device  
- Confirmed network adapter was enabled  
- Confirmed IP address did not start with 169.254 (device was on a network)  
- Confirmed default gateway was present  

---

## Troubleshooting process  

### Step 1: Check IP configuration  

```powershell
ipconfig /all
```

<img width="1272" height="617" alt="image" src="https://github.com/user-attachments/assets/3c720990-b5eb-4ce9-b14f-9b7bce386672" />


Confirmed valid IPv4 address  
Confirmed default gateway present  
Observed DNS server listed as 10.10.10.10(flag)  

---

### Step 2: Test raw connectivity  

```powershell
ping 8.8.8.8
```

<img width="848" height="260" alt="image" src="https://github.com/user-attachments/assets/573f2694-4a47-4dd1-a2c8-372cd30cc683" />


**Result:**    
Ping successful. Network connectivity confirmed.

---

### Step 3: Test DNS resolution  

```powershell
ping google.com
```

<img width="1209" height="69" alt="image" src="https://github.com/user-attachments/assets/7e425ba6-8398-48b1-b173-be2e7c94856a" />


**Result:**     
Ping failed. Domain name could not be resolved. This confirmed a DNS issue.

---

### Step 4: Identify root cause  

<img width="1083" height="530" alt="image" src="https://github.com/user-attachments/assets/93ae6e56-a126-44b7-a4dc-75b27469a0b5" />

Reviewing ipconfig output showed the DNS server was set to an invalid address (10.10.10.10), which was not a real DNS server.

---

## Root cause  
Client device had an invalid DNS server, preventing domain name resolution.

---

## Resolution  

Reset DNS configuration to use automatic DNS assignment.

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ResetServerAddresses
```  

Verified fix:  

```powershell
ping google.com
```

<img width="903" height="388" alt="image" src="https://github.com/user-attachments/assets/e6b6dbb1-adb5-406c-8d75-7dc16a7f00bd" />


Result:  
Ping successful. DNS resolution restored.

---

## Final step: Clear DNS cache  

```powershell
ipconfig /flushdns
```  

This ensured no stale DNS records remained on the system.


<img width="620" height="127" alt="image" src="https://github.com/user-attachments/assets/5ec957d5-5aea-4a55-bd0d-98514c1485c1" />

---

## Resolution summary  
DNS configuration reset  
DNS cache cleared  
User able to access websites and online services again  

---

## Takeaways  
Valid IP with failed domain resolution indicates DNS issues  
`ping 8.8.8.8` confirms network connectivity  
`ping google.com` tests DNS resolution  
DNS misconfiguration can fully disrupt internet access even when the network is functioning  

