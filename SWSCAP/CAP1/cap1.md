### CAP1
# Penetration Test Report

## Introduction

The objective of this report is to document the findings of the penetration test conducted on the server deployed within the College Network. As a Penetration Tester, the task was to assess the security posture of the new server set up before its release on the internet. The assessment aimed to identify vulnerabilities, potential points of entry, and assess the server's resistance to unauthorized access. This report outlines the methods used, vulnerabilities identified, and recommendations for mitigation.

### Scope

The scope of this penetration test encompassed:

1. Identifying all potential entry points into the SWS10 server.
2. Assessing vulnerabilities present in the server software and configurations.

### Methodology

1. **Enumeration:** Checked all ports and services to see where potential access points to the server were.
2. **Vulnerability Assessment:** Utilized specialized tools to identify weaknesses or issues in the server's software and settings.
3. **Exploitation:** Attempted to exploit any identified weaknesses to gain unauthorized access to the server.
4. **Privilege Escalation:** Sought ways to gain additional control over the server once initial access was achieved.
5. **Reporting:** Documented all findings, including discovered problems and recommended solutions.

### Gathering Information

1. **Network Scanning:** Identified active hosts, open ports, and services running on those ports.
2. **Enumeration:** Gathered detailed information about the services and versions running on each open port.
3. **Using Framework:** Utilized the Metasploit framework to conduct auxiliary scans and further probe for potential vulnerabilities in the identified services.

### Exploiting Vulnerabilities

#### PORT 80 (Apache HTTP Server 2.8.8)
- Utilized Metasploit framework for automated exploitation and testing of vulnerabilities.
![alt text](image.png)
- Searched for php_cgi vulnerability, targeting weaknesses in how PHP CGI scripts are handled by the Apache httpd 2.8.8 server.
![alt text](image-1.png)
- Used "use" command to select specific exploits related to PHP CGI argument injection.


- Employed "Show options" command to display configurable parameters for selected exploit modules.
![alt text](image-2.png)

- Executed selected exploit module to take advantage of system weaknesses for unauthorized access.

- Elevated privileges using "/usr/bin/nmap --interactive" while operating in a shell with the user "www-data".

#### PORT 5432 (PostgreSQL 8.3.0 - 8.3.7)
- Leveraged Metasploit and searched for PostgreSQL vulnerabilities.

![alt text](image-3.png)
- Utilized auxiliary scanner module "auxiliary/scanner/postgres/postgres_login" to identify PostgreSQL servers and attempt authentication using default or weak credentials.

![alt text](image-4.png)
- Exploited vulnerabilities in PostgreSQL on Linux systems using "exploit/linux/postgres/postgres_payload".
![alt text](image-5.png)
![alt text](image-6.png)
#### PORT 5900 (VNC - Protocol 3.3)
- Utilized Metasploit framework and searched for the VNC 3.3 module.

- Used auxiliary scanner module "auxiliary/scanner/vnc/vnc_login" to identify VNC servers and attempted authentication using default or weak credentials.
![alt text](image-9.png)
- Exploited vulnerabilities to gain control over the server's desktop and acquire root password.
![alt text](image-7.png)
![alt text](image-8.png)
#### PORT 6667 (UnrealIRCD)
- Initiated Metasploit framework and searched for UnrealIRCd vulnerabilities.

![alt text](image-10.png)

- Exploited known backdoor vulnerability in UnrealIRCd versions prior to 3.2.8.1 using "exploit/unix/irc/unreal_ircd_3281_backdoor" module.


- Configured payload to "cmd/unix/bind_ruby" for interactive access to the compromised system's command-line interface.
![alt text](image-11.png)
![alt text](image-12.png)
#### PORT 8180 (Apache Tomcat/Coyote JSP Engine 1.1)
- Searched for Tomcat vulnerabilities to assess web server and Java-based applications security.

![alt text](image-13.png)
- Utilized "auxiliary/scanner/http/tomcat_mgr_login" module to attempt login to Tomcat Manager interface using a list of credentials.
![alt text](image-14.png)
- Stopped bruteforcing upon successful authentication.
![alt text](image-16.png)
![alt text](image-15.png)
### Exploited Actions

- Gained root access and attempted adding a folder named "dolkerwashere" on the root directory.
- Explored server's desktop via VNC and executed arbitrary commands.
- Obtained root password through exploitation.

## Recommendations

1. **PORT 80 (Apache HTTP Server 2.8.8):**
   - Update Apache to the latest version to fix any security issues.
   - Keep an eye out for updates from Apache and install them regularly.
   - Use firewalls to block unauthorized access to the server.

2. **PORT 5432 (PostgreSQL 8.3.0 - 8.3.7):**
   - Upgrade PostgreSQL to a newer version for better security.
   - Ensure PostgreSQL uses strong passwords and encryption.
   - Monitor access to the database.

3. **PORT 6667 (UnrealIRCd):**
   - Install updates from UnrealIRCd to keep it secure.
   - Employ firewalls to prevent attacks on the IRC server.
   - Enforce strong passwords for users.

4. **PORT 8180 (Apache Tomcat/Coyote JSP Engine 1.1):**
   - Update Tomcat to the latest version for enhanced security.
   - Configure Tomcat for secure logins and access control.
   - Regularly scan web applications for vulnerabilities.

5. **PORT 5900 (VNC - Protocol 3.3):**
   - Utilize strong passwords and encryption for VNC server security.
   - Ensure protection of VNC data during internet transmission.
   - Restrict access to trusted users only.

# Penetration Test Summary

The penetration test conducted on the College Network server unveiled critical vulnerabilities across various ports and services. Through meticulous methods including network scanning, enumeration, and the utilization of Metasploit framework, weaknesses in software versions and configuration settings were exposed.

Exploitation of these vulnerabilities enabled unauthorized access to key components such as Apache HTTP Server, PostgreSQL database, VNC, UnrealIRCd, and Apache Tomcat. Actions undertaken during exploitation included attempts to add folders to the root directory, accessing the server's desktop via VNC, executing arbitrary commands, and obtaining root passwords.

These findings underscore the significance of robust security measures and regular updates to mitigate potential cyber threats. Addressing the identified vulnerabilities and implementing recommendations are imperative steps to bolster the server's security posture and ensure a resilient defense against malicious actors.