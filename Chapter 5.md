### **Chapter 5: Exploitation**  
#### **1. Introduction to Exploitation**  
- **Definition**:  
  - The process of leveraging vulnerabilities to gain control over a system.  
  - Not all exploits lead to full compromise (some grant limited access).  

- **Key Terms**:  
  - **Exploit**: Code that takes advantage of a bug/vulnerability.  
  - **Payload**: Malicious code executed post-exploit (e.g., backdoor, ransomware).  
  - **Example Tools**: Metasploit, SQLMap, John the Ripper.  

---

#### **2. Password Attacks**  
| **Type** | **Method** | **Tools** | **Defenses** |  
|----------|------------|-----------|--------------|  
| **Guessing** | Dictionary attacks (common passwords). | Brutus, Cain | Strong password policies (length > complexity). |  
| **Cracking** | Reverse-engineers hashes (MD5, SHA). | John the Ripper, Hashcat | Use salted hashes; protect password files. |  
| **Hybrid** | Dictionary + brute-force (e.g., `password123`). | Rainbow tables | Multi-factor authentication (MFA). |  

**Steps in Password Cracking**:  
1. **Steal hashes** (e.g., from `/etc/shadow` or SAM database).  
2. **Choose attack** (dictionary, brute-force, hybrid).  
3. **Compare hashes** until match is found.  

**Note**:  
- **Linux Protection**: Store hashes in `/etc/shadow` (readable only by root).  
- **Windows Protection**: Use SYSKEY to encrypt SAM database.  

---

#### **3. Web Application Attacks**  
##### **A. Session Hijacking**  
- **Session Cloning**: Attacker steals/copies a valid session ID.  
  - **Methods**:  
    - URL manipulation (`?sid=1234`).  
    - Cookie tampering (via browser/proxy tools like Burp Suite).  
  - **Defense**: Bind sessions to IP addresses; use HTTPS.  

##### **B. SQL Injection**  
- **How It Works**: Input malicious SQL queries (e.g., `' OR 1=1 --`).  
  - **Impact**: Bypass logins, dump databases, execute commands.  
  - **Defense**: Input sanitization; parameterized queries.  

##### **C. Cross-Site Scripting (XSS)**  
- **Types**:  
  - **Stored XSS**: Malicious script saved on server (e.g., forum post).  
  - **Reflected XSS**: Script reflected via URL (e.g., phishing).  
- **Defense**: Escape user input; CSP headers.  

---

#### **4. Metasploit Framework**  
- **Purpose**: Automated exploitation and payload delivery.  
- **Workflow**:  
  1. **Choose Exploit** (e.g., `exploit/windows/smb/ms17_010_eternalblue`).  
  2. **Set Payload** (e.g., `windows/x64/meterpreter/reverse_tcp`).  
  3. **Execute** (`exploit`).  
- **Post-Exploitation**:  
  - Privilege escalation, lateral movement, data exfiltration.  

---

#### **5. Defenses Against Exploitation**  
- **Patch Management**: Regularly update OS/software.  
- **Least Privilege**: Limit user permissions.  
- **Network Segmentation**: Isolate critical systems.  
- **Logging/Monitoring**: Detect unusual activity (e.g., repeated login failures).  

---

### **Question for You**  
*Why is a hybrid password attack (dictionary + brute-force) more effective than pure dictionary attacks?*  

**Answer**:  
Hybrid attacks append/prepend characters (e.g., `password123`) to dictionary words, cracking complex passwords that slight modifications of common words. Pure dictionary attacks fail against such variants.  

---

### **Key Tools Cheat Sheet**  
| **Tool** | **Purpose** |  
|----------|------------|  
| **Metasploit** | Exploit development/execution. |  
| **John the Ripper** | Password cracking. |  
| **Burp Suite** | Web app manipulation (session hijacking). |  
| **SQLMap** | Automated SQL injection. |  

