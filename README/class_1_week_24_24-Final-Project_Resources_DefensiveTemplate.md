# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

  ![ ](/Images/NetworkTopology.png)


The following machines were identified on the network:
- Name of VM 1
  - **Operating System**: Linux 2.6.32
  - **Purpose**: Attacking machine
  - **IP Address**: 192.168.1.90
- Name of VM 2
  - **Operating System**:Linux 3.2-4.9
  - **Purpose**: Target machine
  - **IP Address**: 192.168.1.110


### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110)

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Error Alert

![ ](/Images/ScreenShot2021-03-24at10.42.45AM.png)

Alert 1 is implemented as follows:
  - **Metric**: Http.response.status.code
  - **Threshold**: Above 400 for the last 5 minutes
  - **Vulnerability Mitigated**: Brute force attacks, (CVE-2015-5600)
  - **Reliability**: high reliability.

#### CPU Usage Alert

![ ](/Images/ScreenShot2021-03-24at10.42.08AM.png)

Alert 2 is implemented as follows:
  - **Metric**: system.process.cpu.total.pct 
  - **Threshold**:  Above 0.5 for the last 5 minutes
  - **Vulnerability Mitigated**: DOS attack (CVE-2018-1303)
  - **Reliability**: low reliability.

#### HTTP Request Size Monitor

![ ](/Images/ScreenShot2021-03-24at10.43.17AM.png)

Alert 3 is implemented as follows:
  - **Metric**: http.request.bytes 
  - **Threshold**:Above 3500 over the last 1 minute
  - **Vulnerability Mitigated**: Directory browsing vulnerability (CWE-548)
  - **Reliability**: medium reliability.


### Suggestions for Going Further

- Vulnerability 1 : Brute Force Attacks
  - **Patch**: Setup password policy for users which will require them to use uppercase, lowercase, combination of alphabets and special characters ( @,$,*) and also requiring them to change password every other month, also implementing a blocklist 
  - **Why It Works**: This will make it difficult for attackers to brute force and gain access using wordlists and hydra
- Vulnerability 2 : DOS Attack
  - **Patch**: Setup a load balancer
  - **Why It Works**: This will distribute request or network load efficiently across the servers preventing redundancy
- Vulnerability 3 : Directory browsing vulnerability
  - **Patch**: Disable directory listing on webserver and create a honeyfile with a name that will attract an attacker
  - **Why It Works**: The honeyfile will serve as a bait file when an attacker tries accessing will alert administrator on a possible intrusion
