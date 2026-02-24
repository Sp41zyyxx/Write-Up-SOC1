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
Using Event Viewer, we reviewed the PowerShell logs and analyzed the HostApplication field. from this field, we were able to identify the legitimate process into which the attacker injected the C2 payload to escalate privileges.
<img width="1918" height="812" alt="image" src="https://github.com/user-attachments/assets/81247935-762e-444a-a735-81128e365baa" />

#### Q6. Following privilege escalation, the attacker attempted to download a file. Can you identify the URL of this file downloaded?
By filtering for `http.request.method == "GET"` and sorting packets by time, we identified the URL in the first HTTP GET request following the privilege escalation.
<img width="1918" height="822" alt="image" src="https://github.com/user-attachments/assets/582cba37-1f6e-495a-96eb-dca11fa8ba65" />

#### Q7. Understanding which group Security Identifier (SID) the malicious script checks to verify the current user's privileges can provide insights into the attacker's intentions. Can you provide the specific Group SID that is being checked?
After identifying the downloaded file in the previous step, we inspected the same packet in Wireshark. By selecting the packet and navigating to:
`Right Click` → `Follow` → `HTTP Stream`
we reviewed the full HTTP response content. Within the downloaded script, we identified the specific Group SID being checked to verify the current user's privileges.
<img width="1918" height="860" alt="image" src="https://github.com/user-attachments/assets/a902f7a8-093b-4435-8194-fdd59dfdb0d8" />

#### Q8. Windows Defender plays a critical role in defending against cyber threats. If an attacker disables it, the system becomes more vulnerable to further attacks. What are the registry keys used by the attacker to disable Windows Defender functionalities? Provide them in the same order found.
Using the same HTTP stream analyzed in Q6 and Q7, we reviewed the downloaded PowerShell script content.
Within the script, we identified the registry modification section where the variable:
`$defenderRegistryPath = "HKLM:\SOFTWARE\Microsoft\Windows Defender"`
is defined.
From this section, we extracted the registry keys modified by the attacker to disable Windows Defender functionalities, listed in the same order as they appear in the script.
<img width="1918" height="767" alt="image" src="https://github.com/user-attachments/assets/96dc523a-c324-467b-8bb3-9c53ffc45dfb" />








