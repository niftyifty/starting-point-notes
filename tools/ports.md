| Port | Service | ELI5 | Pentesting Tip |
|------|---------|------|----------------|
| 20 | FTP (Data) | Used for transferring files | Check for anonymous FTP access or misconfigurations. |
| 21 | FTP (Control) | Controls FTP sessions | Try brute-forcing or banner grabbing for software version. |
| 22 | SSH | Secure shell for remote access | Check for weak credentials, outdated versions, or misconfigs. |
| 23 | Telnet | Unencrypted remote access | Often forgotten; try default creds or sniffing credentials. |
| 25 | SMTP | Sends email | Check for open relay or info leak via VRFY/EXPN. |
| 53 | DNS | Resolves domain names | Can allow DNS zone transfers or be used for tunneling. |
| 67 | DHCP (Server) | Assigns IP addresses | Useful in MITM attacks if DHCP is open. |
| 68 | DHCP (Client) | Receives IP addresses | Not a scanning target, but important for network attacks. |
| 69 | TFTP | Trivial FTP, very simple file transfer | Unauthenticated file access is common. |
| 80 | HTTP | Web traffic | Look for default pages, outdated CMS, and test with Dirb/Gobuster. |
| 110 | POP3 | Receives email | Try sniffing or brute-forcing weak email creds. |
| 111 | RPCbind | Remote procedure call | Used in NFS exploits and Linux enumeration. |
| 123 | NTP | Time synchronization | Can be abused in DDoS reflection attacks. |
| 135 | MS RPC | Microsoft RPC service | Important in Windows enumeration and EternalBlue exploit. |
| 139 | NetBIOS | Windows file/printer sharing | Try enum4linux or check for open shares. |
| 143 | IMAP | Receives email (advanced) | Can expose mailboxes if weak credentials are used. |
| 161 | SNMP | Device management | Use `snmpwalk` to enumerate devices if community string is public. |
| 162 | SNMP Trap | SNMP alerts | Same risk as SNMP – info disclosure. |
| 389 | LDAP | Directory services | Used in AD – can be misconfigured for data leaks. |
| 443 | HTTPS | Encrypted web traffic | Look for SSL issues or web app vulnerabilities. |
| 445 | SMB | Windows sharing & AD | Target for EternalBlue, NTLM relaying, etc. |
| 465 | SMTPS | Encrypted email sending | Check certs and config for info leak. |
| 514 | Syslog | Logs from network devices | Can leak sensitive log info if misconfigured. |
| 587 | SMTP (Submission) | Email sending with authentication | Check for email spoofing or open relay. |
| 631 | IPP | Internet printing protocol | Can be an entry point if exposed. |
| 636 | LDAPS | Secure LDAP | Test for expired or weak SSL certs. |
| 993 | IMAPS | Encrypted IMAP | Brute-forcing might still work. |
| 995 | POP3S | Encrypted POP3 | Look for cert misconfigs. |
| 1433 | MSSQL | Microsoft SQL Server | Try `sqsh`, brute-force, or SQL injection. |
| 1521 | Oracle DB | Oracle database listener | Use `tnscmd` to interact with it. |
| 1723 | PPTP | VPN protocol | Outdated – vulnerable to MS-CHAPv2 cracking. |
| 3306 | MySQL | MySQL database | Try default creds or SQLi. |
| 3389 | RDP | Remote Desktop Protocol | Target for brute-force or CVEs. |
| 3690 | Subversion | Version control system | May expose source code. |
| 5432 | PostgreSQL | Postgres database | Try `psql`, default creds, or SQLi. |
| 5900 | VNC | Remote desktop sharing | Check for no password or weak password. |
| 6379 | Redis | In-memory database | Unauthenticated by default – huge risk. |
| 8080 | HTTP Alt | Alternative HTTP port | Often used by dev servers – check for tools like Jenkins. |
| 8443 | HTTPS Alt | Alternative HTTPS port | Web UIs may be exposed here. |
| 9001 | Tor ORPort | Tor node traffic | Usually just indicates Tor use. |


