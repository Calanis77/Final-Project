# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Name of VM 1 -Kali
  - **Operating System**: Debian Kali
  - **Purpose**: Penetration Tester
  - **IP Address**: 192.168.1.90
- Name of VM 2 -ELK
  - **Operating System**:Ubuntu
  - **Purpose**:The ELK (Elasticsearch and Kibana) Stack
  - **IP Address**:192.168.1.100
- Name of VM 3 -Target 1
  - **Operating System**:Debian GNU/Linux 8
  - **Purpose**:WordPress Host
  - **IP Address**:192.168.1.110
- Name of VM 4 -Capstone
  - **Operating System**:Ubuntu
  - **Purpose**:Vulnerable Web Server
  - **IP Address**:192.168.1.105
  ![image](https://user-images.githubusercontent.com/94859787/173470168-4c509318-a29a-4c96-aca4-e719dddcdf33.png)  
  
### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Name of Alert 1


Alert 1 is implemented as follows: Excessive HTTP Errors
  - **Metric**:WHEN count() GROUPED OVER top 5 'http.response.status_code'
  - **Threshold**:IS ABOVE 400
  - **Vulnerability Mitigated**:Enumeration/ Brute Force
  - **Reliability**:This alert is highly reliable. Measuring the error code that are 400 and above filter out the normal activity or successful responses. 400 and plus codes are client and server errors which are ones of more concern. Especially, when the error codes happen at a high rate.
<img width="1108" alt="Screen Shot 2022-06-08 at 8 26 14 PM" src="https://user-images.githubusercontent.com/94859787/173470284-0ce9980c-a29b-4a39-974a-0fc3e356ea64.png">
#### Name of Alert 2
Alert 2 is implemented as follows:HTTP Request Size Monitor
  - **Metric**:WHEN sum() of http.request.byte OVER all documents
  - **Threshold**:IS ABOVE 3500
  - **Vulnerability Mitigated**:Code injection in HTTP requests (XSS and CRLF) or DDOS
  - **Reliability**:This alert could create false positives, which set the alert at medium reliability. There is a possiblity for a large number of non-malicious HTTP requests or legitimate HTTP traffic.
<img width="1121" alt="Screen Shot 2022-06-08 at 8 25 54 PM" src="https://user-images.githubusercontent.com/94859787/173470326-efd0e21a-9fd2-4d17-902b-3e686af889fc.png">
#### Name of Alert 3

Alert 3 is implemented as follows:CPU Usage Monitor
  - **Metric**:WHEN max() OF system.process.cpu.total.pct OVER all documents
  - **Threshold**:IS ABOVE 0.5
  - **Vulnerability Mitigated**:Malicious software, programs (malware or viruses) running taking up resources.
  - **Reliability**:This alert is highly reliable. Even if there isn't malicious programs running, this alert can still help determine where the CPU can improve usage.
<img width="1140" alt="Screen Shot 2022-06-08 at 8 26 59 PM" src="https://user-images.githubusercontent.com/94859787/173470367-b46116d7-2098-4f91-8230-ecb0f85d1149.png">

### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
