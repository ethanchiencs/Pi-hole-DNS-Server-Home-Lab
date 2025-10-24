# Pi-hole-DNS-Server-Home-Lab
Project Date: October 2025  
Platform: Ubuntu Server 24.04 LTS on Hyper-V  
Purpose: Learn DNS fundamentals, network-wide ad blocking, and Linux server administration  
Project Overview:    
Deployed Pi-hole DNS server in a virtual machine environment to gain hands-on experience with DNS configuration, network traffic monitoring, and ad blocking at the network level. This project provided practical experience with DNS troubleshooting, Linux server management, and understanding how DNS queries work in real-world networks.

Technologies Used:    
Operating System: Ubuntu Server 24.04 LTS  
Virtualization: Hyper-V on Windows 11  
DNS Server: Pi-hole 5.x  
Web Server: Lighttpd (included with Pi-hole)  
Networking: Virtual network with DHCP  
 
Through this project, I gained hands-on experience with:  
<b>1. DNS Fundamentals</b>  
- DNS query resolution process  
- Upstream DNS server configuration  
- DNS forwarding and caching  
- DNS troubleshooting techniques  

<b>2. Linux Server Administration</b>  
Ubuntu Server installation and configuration  
Command-line navigation and system management  
Service management (systemctl)  
Basic networking configuration  

<b>3. Network Security</b>  
Network-wide ad blocking  
DNS filtering and blocklists  
Query logging and analysis  
Understanding DNS-based security  

<b>4. Troubleshooting Skills</b>  
DNS resolution testing (nslookup, dig)  
Service status checking  
Log file analysis  
Network connectivity diagnostics  

<b>Installation Steps</b>  
1. Environment Setup  
Created Ubuntu Server VM in Hyper-V:  
2GB RAM  
20GB virtual hard disk  
Connected to virtual network switch  
Generation 2 VM with Secure Boot disabled  

2. Ubuntu Server Installation  
Installed Ubuntu Server 24.04 LTS with:  
<img width="1027" height="871" alt="Screenshot (30)" src="https://github.com/user-attachments/assets/1526f2b6-fed8-4854-a911-19932321163a" />

Minimal installation (no GUI)  
Default disk partitioning  
SSH server  
Created administrative user account   
<img width="1027" height="869" alt="Screenshot (32)" src="https://github.com/user-attachments/assets/0e6d27fd-821a-4b72-beaf-9b62716b3078" />
<img width="1029" height="875" alt="Screenshot (33)" src="https://github.com/user-attachments/assets/961de508-d040-4365-826b-590624e97ba8" />

3. System Preparation  
Updated system packages:  
bash  
sudo apt update  
sudo apt upgrade -y  
<img width="1029" height="875" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/32f20cf2-2068-4c3d-ad12-b686b2121c02" />


4. Pi-hole Installation  
Installed Pi-hole using official installation script:  
bash
curl -sSL https://install.pi-hole.net | bash
<img width="1035" height="877" alt="Screenshot (35)" src="https://github.com/user-attachments/assets/78e13a75-adca-48ce-af99-e840eb51f6d8" />

