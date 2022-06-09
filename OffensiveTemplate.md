# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
_TODO: Fill out the information below._

Nmap scan results for each machine reveal the below services and OS details:

Command: $ nmap -sV 192.168.1.110

This scan identifies the services below as potential points of entry:
- Target 1
  - List of
  - Exposed Services

_TODO: Fill out the list below. Include severity, and CVE numbers, if possible._

The following vulnerabilities were identified on each target:
- Target 1
- Port 22/TCP Open SSH
- Port 80/TCP Open HTTP
- Port 111/TCP Open rcpbid
- Port 139/TCP Open netbios-ssn
- Port 445/TCP Open netbios-ssn
  - List of Critical Vulnerabilities


- Target 1
 - User Enumeration (WordPress site)
 - Found the occurrence of simplistic usernames and weak passwords (Hydra Command)
 - Brute forced ssh to gain access in to the system.
 - Secure files are not hidden away.
 - Misconfiguration of User Privileges/ Privilege Escalation


_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: _TODO: Insert `flag1.txt` hash value_
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
  - `flag2.txt`: _TODO: Insert `flag2.txt` hash value_
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
