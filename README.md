# task1
Network Reconnaissance and Service Exposure Report

Tool Used: Nmap 7.98
Scan Date: 13-Nov-2025
Scan Type: Local Network Port Scan (/24 subnet)

1. Objective

The purpose of this scan was to enumerate active hosts within the local network and identify exposed TCP services. The findings help assess potential attack surfaces and evaluate security risks related to open ports and services.

2. Scan Summary
Item	Result
Total IPs Scanned	256
Live Hosts Detected	3
Scan Duration	27.33 seconds
Scan Method	Default TCP SYN scan

4. Host Findings
Host 1
Details	Info
IP Address	192.xxx.xxx.xxx
Host Status	Up (0.0090s latency)
MAC Vendor	Intel Corporate

Open Ports:

Port	Service	Description
135/tcp	msrpc	Windows RPC service
139/tcp	netbios-ssn	NetBIOS session service
445/tcp	microsoft-ds	SMB file sharing
2701/tcp	sms-rcinfo	Microsoft SMS Remote Control Information

Risk Level:  High
SMB services (ports 139, 445) are frequently exploited by malware (e.g., WannaCry, EternalBlue).

Host 2
Details	Info
IP Address	192.xxx.xxx.xxx
Host Status	Up (0.0032s latency)
MAC Vendor	Unknown

Open Ports:

Port	Service	Description
53/tcp	domain	DNS service

Risk Level:  Medium
Likely a DNS resolver or router. Ensure DNS is not exposed externally.

Host 3
Details	Info
IP Address	192.xxx.xxx.xxx
Host Status	Up (0.0012s latency)

Open Ports:

Port	Service	Description
135/tcp	msrpc	Windows RPC
139/tcp	netbios-ssn	File sharing
445/tcp	microsoft-ds	SMB
6646/tcp	unknown	Unknown service (requires investigation)

Risk Level:  High
Unknown port 6646 may indicate custom software or a potential backdoor.

4. Risk Assessment
Risk	Explanation
SMB Ports Open	Highly targeted by ransomware, worms, and internal lateral movement attacks.
Unknown Service (6646)	Unknown and undocumented ports may represent vulnerable software or malware.
DNS Exposure	Misconfigured DNS servers may allow internal data leakage.

5. Recommended Actions
For All Hosts

Apply latest Windows security updates (especially SMB patches).

Disable SMBv1 if still enabled.

Restrict internal ports using host-based firewalls.

Run authenticated vulnerability scanning (e.g., Nessus, OpenVAS).

Host 2 (Port 53)

Confirm DNS access is only allowed internally.

Disable recursion if not required.

Monitor logs for DNS tunneling activity.

Host 3 (Port 6646)

Perform service identification:

6. Conclusion

The network hosts expose multiple Microsoft SMB services that may be vulnerable if not properly patched. One unknown service was discovered and should be analyzed further. Hardening measures are strongly recommended to reduce internal attack surface.
