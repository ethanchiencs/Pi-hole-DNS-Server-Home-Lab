# Pi-hole DNS Server Home Lab  

**Project Date:** November 2025    
**Platform:** Ubuntu Server 24.04 LTS on Hyper-V  
**Purpose:** Learn DNS fundamentals, network-wide ad blocking, and Linux server administration

## Project Overview  

Deployed Pi-hole DNS server in a virtual machine environment to gain hands-on experience with DNS configuration, network traffic monitoring, and ad blocking at the network level. This project provided practical experience with DNS troubleshooting, Linux server management, and understanding how DNS queries work in real-world networks.  

---

## Technologies Used

- **Operating System:** Ubuntu Server 24.04 LTS  
- **Virtualization:** Hyper-V on Windows 11  
- **DNS Server:** Pi-hole 5.x
- **Web Server:** Lighttpd (included with Pi-hole)
- **Networking:** Virtual network with DHCP

---

## Learning Objectives

Through this project, I gained hands-on experience with:

1. **DNS Fundamentals**
   - DNS query resolution process
   - Upstream DNS server configuration
   - DNS forwarding and caching
   - DNS troubleshooting techniques

2. **Linux Server Administration**
   - Ubuntu Server installation and configuration
   - Command-line navigation and system management
   - Service management (systemctl)
   - Basic networking configuration

3. **Network Security**
   - Network-wide ad blocking
   - DNS filtering and blocklists
   - Query logging and analysis
   - Understanding DNS-based security

4. **Troubleshooting Skills**
   - DNS resolution testing (nslookup, dig)
   - Service status checking
   - Log file analysis
   - Network connectivity diagnostics

---

## Installation Steps

### 1. Environment Setup

**Created Ubuntu Server VM in Hyper-V:**
- 2GB RAM
- 20GB virtual hard disk
- Connected to virtual network switch
- Generation 1 VM  
<img width="1027" height="871" alt="Screenshot (30)" src="https://github.com/user-attachments/assets/11361c89-2b6a-4998-8c19-8cace4e3d0bf" />

### 2. Ubuntu Server Installation

Installed Ubuntu Server 24.04 LTS with:
- Minimal installation (no GUI)
- Default disk partitioning
- SSH server (optional)
- Created administrative user account
<img width="1027" height="869" alt="Screenshot (32)" src="https://github.com/user-attachments/assets/e4613909-e98c-415f-907f-74bdb9c555f4" />
<img width="1029" height="875" alt="Screenshot (33)" src="https://github.com/user-attachments/assets/279f7801-fdf8-495b-93d0-4969ced6290d" />

### 3. System Preparation

Updated system packages:
```bash
sudo apt update
sudo apt upgrade -y
```
<img width="1029" height="875" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/b4b41ffc-61fa-440a-a3f7-5fbb83272708" />


### 4. Pi-hole Installation

Installed Pi-hole using official installation script:
```bash
curl -sSL https://install.pi-hole.net | bash
```
<img width="1035" height="877" alt="Screenshot (35)" src="https://github.com/user-attachments/assets/2f3cb01f-7a41-4107-ae86-9aba903a02e9" />

**Configuration Choices:**
- Interface: eth0 (default network interface)
- Upstream DNS: OpenDNS
- Blocklists: Enabled default lists
- Web Interface: Enabled
- Web Server: Lighttpd (installed automatically)
- Query Logging: Enabled
- Privacy Mode: Show everything (for learning purposes)
<img width="1035" height="872" alt="Screenshot (37)" src="https://github.com/user-attachments/assets/7ffc71f2-b7b1-4806-acc5-1b2864dae408" />

---

## Configuration

### DNS Server Setup

**IP Address:** Static IP assigned via DHCP reservation in virtual network

**Upstream DNS Providers:**
- Primary: OpenDNS

**Blocklists Enabled:**
- Default Pi-hole blocklists (ads and tracking domains)
- Automatically updated weekly

### Web Interface Access

**Admin Panel:** `http://[PI-HOLE-IP]/admin`
- Configured secure admin password
- Enabled query logging for monitoring
- Dashboard shows real-time statistics
<img width="1924" height="1030" alt="Screenshot (40)" src="https://github.com/user-attachments/assets/b53d11a6-10d0-46b5-9edc-1c6749ffed1b" />

---

## Testing & Validation

### DNS Resolution Testing

**Command-line testing from Windows host:**
```cmd
nslookup google.com [PI-HOLE-IP]
```
<img width="979" height="512" alt="Screenshot (41)" src="https://github.com/user-attachments/assets/0c60c3e2-8a36-4223-8891-1c6fe2c03867" />

**Verified:**
- Successful DNS query resolution
- Response time within acceptable range
- Proper upstream DNS forwarding

### Ad Blocking Validation

**Testing methodology:**
1. Configured test machine to use Pi-hole as DNS server
2. Browsed ad-heavy websites (news sites, blogs)
3. Monitored Pi-hole query logs for blocked domains
4. Verified ads were blocked at DNS level
<img width="1121" height="607" alt="Screenshot (42)" src="https://github.com/user-attachments/assets/73135092-0904-47a5-a600-141e935d9e5f" />

**Results:**
- Successfully blocked advertising domains found on "cnn.com"
- Reduced page load times (fewer resources loaded)
- Query logs showed clear distinction between allowed and blocked domains
- Average block rate: 15-30% of queries on typical websites
<img width="959" height="1037" alt="Screenshot (43)" src="https://github.com/user-attachments/assets/0e6ac337-d0ea-4733-97b5-4f295f4d4118" />

### Query Log Analysis

**Monitored DNS queries showing:**
- Source IP of requesting device
- Domain being queried
- Query type (A, AAAA, PTR, etc.)
- Response status (allowed/blocked)
- Response time

---

## Troubleshooting Scenarios

### Issue 1: DNS Resolution Failure

**Problem:** Client unable to resolve domain names

**Troubleshooting Steps:**
1. Checked Pi-hole service status:
   ```bash
   pihole status
   ```
2. Verified network connectivity:
   ```bash
   ping 8.8.8.8
   ```
3. Reviewed DNS query logs for errors
4. Tested DNS resolution directly:
   ```bash
   dig @127.0.0.1 google.com
   ```

**Resolution:** Service restart resolved the issue
```bash
pihole restartdns
```

### Issue 2: Web Interface Inaccessible

**Problem:** Could not access admin dashboard

**Troubleshooting Steps:**
1. Verified web server status:
   ```bash
   sudo systemctl status lighttpd
   ```
2. Checked if port 80 was open:
   ```bash
   sudo netstat -tulpn | grep :80
   ```
3. Reviewed web server logs:
   ```bash
   sudo tail -f /var/log/lighttpd/error.log
   ```

**Resolution:** Restarted web server
```bash
sudo systemctl restart lighttpd
```

### Issue 3: High Query Volume from Unknown Source

**Problem:** Excessive DNS queries from specific IP

**Troubleshooting Steps:**
1. Reviewed query log in web interface
2. Identified source IP making excessive requests
3. Analyzed query patterns (domains being requested)
4. Determined if behavior was normal or anomalous

**Resolution:** Identified as normal behavior from automated service (Windows telemetry)

---

## Key Learnings

### DNS Concepts Mastered

**DNS Query Flow:**
1. Client requests domain resolution
2. Pi-hole receives query
3. Checks if domain is in blocklist
   - If blocked: Returns null IP (0.0.0.0)
   - If allowed: Forwards to upstream DNS
4. Caches response for faster future lookups
5. Returns result to client

**DNS Record Types:**
- A records (IPv4 addresses)
- AAAA records (IPv6 addresses)
- CNAME records (aliases)
- PTR records (reverse DNS)

### Linux Administration Skills

**Command-Line Operations:**
- System status monitoring (`systemctl`, `pihole status`)
- Log file review (`tail`, `grep`)
- Network diagnostics (`ping`, `nslookup`, `dig`)
- Service management (start, stop, restart services)

### Network Troubleshooting

**Systematic Approach:**
1. Verify service is running
2. Check network connectivity
3. Test DNS resolution
4. Review logs for errors
5. Isolate problem (server vs. client vs. network)

---

## Skills Demonstrated

**Technical Skills:**
- DNS server configuration and management
- Linux server administration (Ubuntu)
- Network troubleshooting and diagnostics
- Query log analysis and pattern recognition
- Service monitoring and maintenance

**Problem-Solving Skills:**
- Systematic troubleshooting methodology
- Root cause analysis
- Documentation of issues and resolutions
- Proactive monitoring and maintenance

**Documentation Skills:**
- Technical procedure documentation
- Troubleshooting guides
- Configuration documentation
- Clear, organized record-keeping

---

## Future Enhancements

**Potential improvements to explore:**
- Configure additional blocklists for enhanced filtering
- Set up DNS over HTTPS (DoH) for encrypted queries
- Implement conditional forwarding for local domains
- Create custom blocklists for specific categories
- Set up monitoring and alerting for service health
- Configure multiple upstream DNS providers for redundancy

---

## Real-World Applications

This lab simulates enterprise DNS scenarios including:

**Help Desk/Desktop Support:**
- Troubleshooting DNS resolution issues
- Understanding why users can't reach certain websites
- Analyzing network connectivity problems
- Supporting remote access and VPN users

**Network Administration:**
- Managing DNS infrastructure
- Monitoring network traffic patterns
- Implementing content filtering policies
- Maintaining service availability

**Security Operations:**
- Identifying malicious domain requests
- Blocking known malicious sites
- Analyzing DNS logs for anomalies
- Understanding DNS-based attacks

---

## Conclusion

This Pi-hole DNS server lab provided practical, hands-on experience with DNS fundamentals, Linux server administration, and network troubleshooting. The skills gained are directly applicable to help desk, desktop support, and network administration roles where DNS troubleshooting is a daily task.

**Key Takeaway:** Understanding how DNS works at a fundamental level—by actually running and monitoring a DNS server—provides invaluable insight that helps diagnose connectivity issues more effectively in production environments.

---
