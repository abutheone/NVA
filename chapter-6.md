### **Chapter 6: Web Server & Application Security - Detailed Notes**  

---

## **1. Web Server Basics**  
### **Types of Web Servers**  
| **Server** | **Platform** | **Common Use** |  
|------------|-------------|----------------|  
| **Apache** | Cross-platform (Linux) | PHP websites |  
| **IIS** | Windows | ASP/.NET websites |  
| **Tomcat** | Cross-platform | Java (JSP) applications |  
| **Nginx** | Linux/Windows | High-performance sites |  

### **Common Web Server Vulnerabilities**  
- **Default Configs**: Default passwords (e.g., `admin:admin`), open ports.  
- **Misconfigurations**:  
  - Directory listing enabled.  
  - Unnecessary services (FTP, Telnet).  
- **Unpatched Software**: Bugs in OS/web server (e.g., Apache Struts RCE).  

---

## **2. Web Server Attacks**  
| **Attack** | **How It Works** | **Impact** |  
|------------|----------------|------------|  
| **Directory Traversal** | `../../` to access restricted files (e.g., `/etc/passwd`). | Sensitive data leaks, RCE. |  
| **Defacement** | Replace website content (e.g., homepage hacked). | Reputation damage. |  
| **DNS Hijacking** | Redirect traffic to fake sites (e.g., phishing). | Data theft, malware spread. |  
| **Pharming** | Modify DNS/hosts file to redirect legit domains. | Credential theft. |  
| **DoS/DDoS** | Flood server with traffic (e.g., SYN floods). | Service downtime. |  

### **Sniffing Attacks**  
- **Risk**: Intercept unencrypted traffic (HTTP, FTP).  
- **Tool**: Wireshark, tcpdump.  
- **Defense**: Use **HTTPS/TLS**, disable plaintext protocols.  

---

## **3. Web Application Attacks (OWASP Top 10 Focus)**  
### **A. SQL Injection (SQLi)**  
- **Payload Example**:  
  ```sql
  ' OR 1=1 -- 
  ```  
  - Bypasses login, dumps databases.  
- **Defense**:  
  - **Parameterized queries** (prepared statements).  
  - Input validation (block `'`, `;`, `--`).  

### **B. Cross-Site Scripting (XSS)**  
| **Type** | **Description** |  
|----------|----------------|  
| **Stored XSS** | Malicious script saved on server (e.g., blog comment). |  
| **Reflected XSS** | Script via URL (e.g., phishing link). |  
| **DOM XSS** | Client-side script manipulation. |  

**Defense**:  
- Escape user input (`<script>` → `&lt;script&gt;`).  
- Use **Content Security Policy (CSP)** headers.  

### **C. Session Hijacking**  
- **Methods**:  
  - Stealing cookies (e.g., via XSS).  
  - Session fixation (force victim to use attacker’s session ID).  
- **Defense**:  
  - Use **HttpOnly** and **Secure** flags for cookies.  
  - Regenerate session IDs post-login.  

### **D. File Upload Attacks**  
- **Risk**: Upload malicious files (e.g., `.php` shell).  
- **Defense**:  
  - Restrict file extensions (e.g., allow only `.jpg`, `.png`).  
  - Scan files for malware.  

---

## **4. Countermeasures**  
### **For Web Servers**  
1. **Patch Management**: Update OS/web server (e.g., Apache, IIS).  
2. **Disable Unused Services**: FTP, Telnet, SSH (if not needed).  
3. **Firewall Rules**: Block unnecessary ports (e.g., close port 21 if FTP is unused).  
4. **Log Monitoring**: Detect brute-force attempts, unusual traffic.  

### **For Web Applications**  
1. **WAF (Web Application Firewall)**: Block SQLi/XSS payloads.  
2. **Input Validation**: Sanitize user inputs (e.g., strip `<>`, `'`).  
3. **Least Privilege**: DB users should have minimal permissions.  

---

## **5. Key Tools**  
| **Tool** | **Purpose** |  
|----------|------------|  
| **Nikto** | Web server vulnerability scanner. |  
| **Burp Suite** | Intercept/modify HTTP requests (testing XSS/SQLi). |  
| **SQLMap** | Automated SQL injection tool. |  
| **OWASP ZAP** | Open-source web app security scanner. |  

---

### **Question for You**  
*How does a **Directory Traversal** attack exploit web servers, and what’s the simplest defense against it?*  

**Answer**:  
It uses `../` sequences to access files outside the web root (e.g., `http://site.com/../../etc/passwd`).  
**Defense**: Disable directory listing; sanitize user input (block `../`).  

---
