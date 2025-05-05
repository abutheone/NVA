### **Chapter 4: Scanning**  
#### **1. Introduction to Scanning**  
- **Purpose**:  
  - Identify live hosts, open ports, services, and vulnerabilities after reconnaissance.  
  - Analogous to a burglar checking doors/windows before breaking in.  

- **Key Questions Answered**:  
  - Which hosts are alive?  
  - What services are running?  
  - What OS/platform is used?  
  - Are there exploitable vulnerabilities?  

---

#### **2. Port Scanning Basics**  
- **Port States**:  
  - **Open**: Service is listening (potential attack surface).  
  - **Closed**: Port is accessible but no service running.  
  - **Filtered**: Firewall/proxy blocks access (no response).  

- **Well-Known Ports (0–1023)**:  
  - E.g., `80 (HTTP)`, `443 (HTTPS)`, `25 (SMTP)`, `53 (DNS)`.  
  - Full list: [IANA.org](https://www.iana.org/).  

---

#### **3. TCP vs. UDP Scans**  
| **TCP** | **UDP** |  
|---------|---------|  
| Connection-oriented (three-way handshake). | Connectionless (no handshake). |  
| Reliable (acknowledgments). | Unreliable (no ACKs). |  
| Used for HTTP, FTP, SSH. | Used for DNS, DHCP, SNMP. |  
| Scans: SYN, Connect, FIN. | Scans: ICMP response for closed ports. |  

**Three-Way Handshake**:  
1. Client → SYN → Server.  
2. Client ← SYN/ACK ← Server.  
3. Client → ACK → Server.  

---

#### **4. Types of Port Scans**  
| **Scan Type** | **Command** | **Stealth** | **Use Case** |  
|--------------|------------|------------|-------------|  
| **TCP Connect** | `nmap -sT` | Low (logs full handshake) | Basic scan, no firewall evasion. |  
| **SYN (Half-Open)** | `nmap -sS` | High (no completed handshake) | Stealthy scan; avoids logs. |  
| **FIN/XMAS/NULL** | `nmap -sF/-sX/-sN` | High (abnormal flags) | Bypass firewalls (fails on Windows). |  
| **Ping Sweep** | `nmap -sP` | N/A | Check live hosts (ICMP echo). |  
| **UDP Scan** | `nmap -sU` | Slow (no response = open) | DNS, DHCP services. |  

**Note**: Windows ignores FIN/XMAS/NULL scans (non-RFC compliant).  

---

#### **5. Key Tools**  
- **Nmap**:  
  - Features: OS detection (`-O`), service version (`-sV`), scripting (`--script`).  
  - Example: `nmap -sS -p 1-1000 -A 192.168.1.1`.  
- **Nessus/OpenVAS**:  
  - Vulnerability scanners (checks CVE databases).  

---

#### **6. Defenses Against Scanning**  
- **Firewalls**: Block unsolicited probes (drop SYN packets).  
- **IDS/IPS**: Detect scan patterns (e.g., rapid connection attempts).  
- **Port Knocking**: Hide services until a secret knock sequence is used.  
- **Limit Services**: Close unused ports (reduce attack surface).  

---

#### **7. Practical Considerations**  
- **Ethical Hacking**: Always get permission before scanning.  
- **False Positives**: Filtered ports may appear closed.  
- **Network Noise**: Scans can trigger alarms (use `-T` for timing control).  

---

### **Question for You**  
*How does a SYN scan (`-sS`) avoid detection in log files compared to a TCP Connect scan (`-sT`)?*  

**Answer**:  
A SYN scan never completes the TCP handshake (sends SYN, receives SYN/ACK, then sends RST instead of ACK), leaving no full connection log. A Connect scan completes the handshake, leaving entries in application logs.  

---
