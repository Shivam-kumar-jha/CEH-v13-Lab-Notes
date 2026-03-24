CEH v13 — Personal Lab Notes & Command Reference

Documented by Shivam Kumar | BTech CSE (3rd Year) | C|CT Certified | C|EH In Progress
CGPA 9.25 | GD Goenka University | LinkedIn | Email


⚠️ Disclaimer
All techniques documented here were performed in EC-Council's official iLabs controlled environment as part of the CEH v13 curriculum. This repository is for educational and revision purposes only. No exam answers or proprietary EC-Council content is reproduced. Never use these techniques on systems you don't own or have explicit written permission to test.

About This Repository
This is my personal lab documentation for the Certified Ethical Hacker (C|EH) v13 course by EC-Council. Rather than just watching lectures, I document every lab with:

The concept behind each technique (the why)
The exact commands I ran (the what)
The real output from my lab sessions (the proof)
Defensive takeaways for blue team context


If you're studying for CEH or just getting into penetration testing — feel free to use these as a reference. Star ⭐ the repo if it helps.


 Module Index
#ModuleTopics CoveredStatus03Scanning NetworksHost Discovery, Port Scanning, OS Fingerprinting, IDS Evasion, Metasploit, ShellGPT✅ Complete04EnumerationNetBIOS, SNMP, LDAP, NFS, DNS, SMTP, Global Network Inventory✅ Complete05Vulnerability AnalysisComing soon🔄 In Progress06System HackingComing soon⏳ Planned

Module 03 — Scanning Networks
Core idea: Scanning is active reconnaissance — you're sending crafted packets to map the attack surface.
Labs Covered
LabToolTechniqueHost DiscoveryNmapARP, ICMP, UDP, TCP ping scansPort & Service DiscoveryNmap / ZenmapSYN, Xmas, Maimon, ACK, UDP scansOS DiscoveryNmap NSESMB fingerprinting, TTL analysisIDS/Firewall EvasionNmapFragmentation, decoys, MTU, source portNetwork ScanningMetasploitportscan modules, SMB versionAI-Assisted ScanningShellGPTNatural language → automated pipelines
Key Commands
bash# Host Discovery
nmap -sn -PR 10.10.1.22          # ARP ping (most reliable on LAN)
nmap -sn -PE 10.10.1.10-23       # ICMP ECHO sweep across subnet

# Port Scanning
nmap -sS -v 10.10.1.22           # SYN/Stealth scan (root required)
nmap -sT -v 10.10.1.22           # Full TCP connect scan
nmap -sU -v 10.10.1.22           # UDP scan
nmap -sX -v 10.10.1.22           # Xmas scan

# Service & OS Detection
nmap -sV 10.10.1.22              # Service version detection
nmap -O 10.10.1.22               # OS fingerprinting
nmap -A 10.10.1.22               # Aggressive: OS + version + scripts + traceroute

# IDS/Firewall Evasion
nmap -f 10.10.1.11               # Packet fragmentation
nmap -g 80 10.10.1.11            # Source port manipulation
nmap --mtu 8 10.10.1.11          # Custom MTU
nmap -D RND:10 10.10.1.11        # IP address decoys

 Module 04 — Enumeration
Core idea: Enumeration goes beyond scanning — you're actively extracting usernames, shares, and service details from open ports.

Scanning tells you what's OPEN. Enumeration tells you what's EXPLOITABLE.

Labs Covered
LabProtocolPortToolNetBIOS EnumerationNetBIOS137–139nbtstat, net useSNMP EnumerationSNMP/UDP161snmpwalkLDAP EnumerationLDAP/TCP389AD ExplorerNFS EnumerationNFS/TCP2049RPCScan, SuperEnumDNS EnumerationDNS/UDP53dig, nslookupSMTP EnumerationSMTP/TCP25Nmap NSEFull Host AuditSMB/WMI—Global Network Inventory
Key Commands
bash# SNMP
snmpwalk -v1 -c public 10.10.1.22       # Walk full MIB tree (SNMPv1)
snmpwalk -v2c -c public 10.10.1.22      # SNMPv2c walk

# NFS
nmap -p 2049 10.10.1.19                 # Check if NFS port is open
python3 rpc-scan.py 10.10.1.19 --rpc    # List RPC services + NFS exports

# DNS
dig ns www.certifiedhacker.com                           # Get name servers
dig @ns1.bluehost.com www.certifiedhacker.com axfr       # Zone transfer attempt

# SMTP
nmap -p 25 --script=smtp-enum-users 10.10.1.19    # Extract valid usernames
nmap -p 25 --script=smtp-open-relay 10.10.1.19    # Test for open relay
nmap -p 25 --script=smtp-commands 10.10.1.19      # List supported SMTP commands

 Defensive Takeaways (Blue Team)
FindingFixNetBIOS exposed on networkDisable NetBIOS over TCP/IP if not neededDefault SNMP community strings (public)Change defaults; upgrade to SNMPv3Anonymous LDAP queries allowedRequire authentication for all LDAP bindsNFS exports misconfiguredUse root_squash; restrict by IPDNS zone transfer openRestrict AXFR to trusted secondary NS IPs onlySMTP VRFY/EXPN enabledDisable in mail server configOpen SMTP relayEnforce SPF, DKIM, DMARC

 Tools Used
Nmap · Metasploit Framework · snmpwalk · AD Explorer (Sysinternals) · RPCScan · SuperEnum · dig · nslookup · ShellGPT · Parrot Security OS · Wireshark

 Certifications

 C|CT — Certified Cybersecurity Technician (EC-Council) — Completed
 C|EH — Certified Ethical Hacker v13 (EC-Council) — In Progress
 C|SA — Certified SOC Analyst — Planned (Feb 2026)
 E|CIH — Certified Incident Handler — Planned (Apr 2026)


 Connect
If you're studying for CEH, working in cybersecurity, or hiring for internships/roles — I'd love to connect.

 LinkedIn: linkedin.com/in/shivamkrj
 Email: becomeshivamjha@gmail.com
 Open to: Cybersecurity internships (Summer 2025) & full-time roles (May 2027)


More modules coming as I progress through the course. Watch/Star ⭐ to get notified.
