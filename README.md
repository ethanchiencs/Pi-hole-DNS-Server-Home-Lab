# Pi-hole-DNS-Server-Home-Lab
Project Date: November 2025  
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


Learning Objectives
Through this project, I gained hands-on experience with:

DNS Fundamentals

DNS query resolution process
Upstream DNS server configuration
DNS forwarding and caching
DNS troubleshooting techniques


Linux Server Administration

Ubuntu Server installation and configuration
Command-line navigation and system management
Service management (systemctl)
Basic networking configuration


Network Security

Network-wide ad blocking
DNS filtering and blocklists
Query logging and analysis
Understanding DNS-based security


Troubleshooting Skills

DNS resolution testing (nslookup, dig)
Service status checking
Log file analysis
Network connectivity diagnostics

Installation Steps
1. Environment Setup
Created Ubuntu Server VM in Hyper-V:

2GB RAM
20GB virtual hard disk
Connected to virtual network switch
Generation 2 VM with Secure Boot disabled

2. Ubuntu Server Installation
Installed Ubuntu Server 24.04 LTS with:

Minimal installation (no GUI)
Default disk partitioning
SSH server (optional)
Created administrative user account
