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

#### Q9. Can you determine the URL of the second file downloaded by the attacker?
I used the same method as in Q6 and identified the second .exe file
<img width="1327" height="877" alt="image" src="https://github.com/user-attachments/assets/046e1ce3-23f5-4de1-93c5-9990b35b14be" />

#### Q10. Identifying malicious tasks and understanding how they were used for persistence helps in fortifying defenses against future attacks. What's the full name of the task created by the attacker to maintain persistence?
To identify the persistence mechanism, we analyzed the /checking.ps1 PowerShell script. Within this script, the `function CleanerEtc` contains commands related to scheduled task creation. By reviewing this function, we were able to identify the full name of the malicious task created by the attacker to maintain persistence.
<img width="1272" height="147" alt="image" src="https://github.com/user-attachments/assets/f6435c25-4e84-40da-872a-7019b2dbf41e" />

#### Q11. Based on your analysis of the second malicious file, What is the MITRE ID of the main tactic the second file tries to accomplish?
During the analysis, we observed that the malware modifies the registry path HKLM:\SOFTWARE\Microsoft\Windows Defender, indicating an attempt to disable Windows Defender protections. This behavior aligns with the MITRE ATT&CK tactic Defense Evasion (TA****), as the objective is to bypass security mechanisms and avoid detection.

#### Q12. What's the invoked PowerShell script used by the attacker for dumping credentials?
By applying the filter `http.request.method == "GET"` in Wireshark, we were able to enumerate all files retrieved via HTTP requests. One of the downloaded files contained the term `DUMP` in its name, suggesting credential harvesting activity. Further analysis confirmed that this PowerShell script was responsible for credential dumping.
<img width="1895" height="837" alt="image" src="https://github.com/user-attachments/assets/9d908c3a-a61a-4e00-852a-0046478abb1d" />

#### Q13. Understanding which credentials have been compromised is essential for assessing the extent of the data breach. What's the name of the saved text file containing the dumped credentials?
By analyzing /ichigo-lite.ps1, we identified the text file where the dumped credentials are saved.
<img width="1603" height="841" alt="image" src="https://github.com/user-attachments/assets/8ad07c26-f618-4094-b620-0fadf99f50fb" />

#### Q14. Knowing the hosts targeted during the attacker's reconnaissance phase, the security team can prioritize their remediation efforts on these specific hosts. What's the name of the text file containing the discovered hosts?
By applying the filter http.request.method == "GET" in Wireshark, we identified the downloaded files. The only file with a .txt extension corresponds to the text file containing the discovered hosts.
<img width="1915" height="250" alt="image" src="https://github.com/user-attachments/assets/9ec57593-1c5a-4324-af47-0bef8e0bfafb" />

#### Q15. After hash dumping, the attacker attempted to deploy ransomware on the compromised host, spreading it to the rest of the network through previous lateral movement activities using SMB. You’re provided with the ransomware sample for further analysis. By performing behavioral analysis, what’s the name of the ransom note file?
After generating the MD5 hash of javaw.exe, we searched it on VirusTotal. The behavioral analysis revealed the name of the ransom note file dropped by the ransomware.
<img width="1853" height="775" alt="image" src="https://github.com/user-attachments/assets/8b660412-750c-4997-97ad-be84e44bad16" />

#### Q16. In some cases, decryption tools are available for specific ransomware families. Identifying the family name can lead to a potential decryption solution. What's the name of this ransomware family?
<img width="1662" height="712" alt="image" src="https://github.com/user-attachments/assets/bb902ba2-a9c4-4742-9874-df602941398d" />

