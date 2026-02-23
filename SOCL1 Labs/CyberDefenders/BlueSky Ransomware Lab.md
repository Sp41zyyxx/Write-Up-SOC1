https://cyberdefenders.org/blueteam-ctf-challenges/bluesky-ransomware/

##### DIFFICULT = `MEDIUM`

##### Category: `Network Forensics`

##### Tactics: `Execution` `Persistence` `Privilege Escalation` `Defense Evasion` `Credential Access` `Discovery` `Command and Control` `Impact`

##### Tools: `Wireshark` `Network Miner` `Windows Event Viewer` `Event Log Explorer` `VirusTotal` `CyberChef`

---

#### Q1. Knowing the source IP of the attack allows security teams to respond to potential threats quickly. Can you identify the source IP responsible for potential port scanning activity?
In this case, I used the `icmp.type == 3` command to grep for 'ICMP Destination Unreachable'. Thanks to that, I can see the IP addresses that are performing port scans.

<img width="1882" height="80" alt="image" src="https://github.com/user-attachments/assets/71012d35-9ed1-4d70-b7f4-b6d1a84a7478" />

#### Q2. During the investigation, it's essential to determine the account targeted by the attacker. Can you identify the targeted account username?
Using NetworkMiner, we can view the credentials, username and password used for exfiltration.
<img width="1918" height="222" alt="image" src="https://github.com/user-attachments/assets/64995e10-6198-4733-9ddd-168979731d16" />

#### Q3. We need to determine if the attacker succeeded in gaining access. Can you provide the correct password discovered by the attacker?
We can see the password using the same method as in Q2.
<img width="1918" height="222" alt="image" src="https://github.com/user-attachments/assets/c24867f4-f8ef-4d3d-8f1a-bb767244ebb1" />

#### Q4. Attackers often change some settings to facilitate lateral movement within a network. What setting did the attacker enable to control the target host further and execute further commands?
Using NetworkMiner, we checked the Parameters tab and analyzed the SQL queries. In SQL query 21, the attacker enabled xp_cmdshell, allowing remote command execution and further control of the target host.
<img width="1918" height="220" alt="image" src="https://github.com/user-attachments/assets/6c2e88a2-ddc7-4e21-ab31-89686c9ca5ce" />

#### Q5. Process injection is often used by attackers to escalate privileges within a system. What process did the attacker inject the C2 into to gain administrative privileges?





