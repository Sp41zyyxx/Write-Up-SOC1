https://cyberdefenders.org/blueteam-ctf-challenges/redishell-kinsing/

##### Difficult == `Medium`

##### Category: `Network Forensics`

##### Tactics: `Initial Access` `Execution` `Privilege Escalation` `Credential Access`

##### Tool: `Wireshark`

---
**Initial Access & Reconnaissance**

#### Q1. Security monitoring flagged suspicious HTTP traffic targeting the container subnet. Identifying the first system that received malicious requests is essential for establishing the initial point of compromise. What is the IP address of the first compromised system?
<img width="1918" height="753" alt="image" src="https://github.com/user-attachments/assets/db42a59c-f6c0-4320-a050-7950cefb9e26" />

#### Q2. Identifying attacker IP is critical for threat intelligence and blocking future connections. What is the attacker's command and control (C2) IP address?
We can find it in the Q1 IP source.

#### Q3. What web application and version was exploited for initial access?
<img width="1917" height="746" alt="image" src="https://github.com/user-attachments/assets/974dbc2f-2fec-43ad-8741-36146bc9b5a2" />

#### Q4. Before fully exploiting a vulnerability, attackers often perform a proof-of-concept test to confirm code execution capabilities. What file did the attacker initially read to test the vulnerability? (Provide full path)
<img width="1364" height="746" alt="image" src="https://github.com/user-attachments/assets/2403517f-edf9-40f1-a7bd-633f5ab8b300" />

#### Q5. Identifying this vulnerable endpoint helps understand the attack vector and informs remediation efforts. What is the URI path of the vulnerable endpoint exploited by the attacker?
<img width="920" height="117" alt="image" src="https://github.com/user-attachments/assets/1a07946e-5047-47fa-8412-15ef814203eb" />

**Execution**

#### Q6. After confirming code execution, the attacker established a reverse shell connection back to their C2 infrastructure. What port number did the attacker use for the initial reverse shell listener?
<img width="1227" height="661" alt="image" src="https://github.com/user-attachments/assets/a11f0435-cb24-463b-a535-06f84224d227" />

**Discovery**

#### Q7. Once inside the compromised container, the attacker uploaded a well-known enumeration script to identify privilege escalation vectors. What privilege escalation enumeration script did the attacker download after gaining shell access?
linpeas
