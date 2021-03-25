# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
Nmap scan results for each machine reveal the below services and OS details:

$ nmap 192.168.1.0/24
![ ](/Images/ScreenShot2021-03-19at10.30.43PM.png)

![ ](/Images/ScreenShot2021-03-19at10.31.23PM.png)

This scan identifies the services below as potential points of entry:
- Target 1
  - Port 22/SSH
  - Port 80/HTTP
  - Port 111/rpcbind
  - Port 139/netbios-ssn
  - Port 445/microsoft-ds


The following vulnerabilities were identified on each target:
- Target 1
  - Brute force vulnerability 
  - Weak password requirements (CWE-521)
  - port 22 open allowing for ssh remote login (CVE-2015-5600)
  - Directory crawling
  - CVE-2009-2335 (wordpress user ID vulnerability aloowing us to determine the users)

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: b9bbcb33e11b80be759c4e844862482d
    - **Exploit Used**
      ![ ](/Images/ScreenShot2021-03-19at11.07.26PM.png)

      ![ ](/Images/ScreenShot2021-03-19at11.10.02PM.png)

      ![ ](/Images/ScreenShot2021-03-19at11.59.16PM.png)

      ![ ](/Images/ScreenShot2021-03-20at12.13.23AM.png)

      ![ ](/Images/ScreenShot2021-03-24at12.57.46PM.png)
      
      - We enumerated the wordpress site with a wpscan to determine the users (command is in screenshot)
      - After finding the users we bruteforced using hydra and a wordlist file to determine the user password
      - Since port 22 is open we were able to get remote through ssh with the username and password 
      - flag 1 was found in service.html file which was located in /var/www/html directory (commands used are in screenshots)

  - `flag2.txt`: fc3fd58dcdad9ab23faca6e9a36e581c
    - **Exploit Used**

    ![ ](/Images/ScreenShot2021-03-20at12.18.21AM.png)

    ![ ](/Images/ScreenShot2021-03-20at12.18.49AM.png)

    ![ ](/Images/ScreenShot2021-03-20at12.19.45AM.png)

      - While we had ssh into the target with Michael's credentials
      - We used the find command to locate flag 2  
      
