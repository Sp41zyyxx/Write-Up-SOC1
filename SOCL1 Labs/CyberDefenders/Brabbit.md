https://cyberdefenders.org/blueteam-ctf-challenges/brabbit/ 
##### DIFFICULT = MEDIUM
##### Category: `Threat Intel`

##### Tactics:`Execution` `Persistence` `Privilege Escalation` `Command and Control` `Impact`

##### Tools: `malpedia` `VirusTotal` `ANY.RUN` `Email Header Analyzer` `MalwareURL`

---
#### Q1. The phishing email used to deliver the malicious attachment showed several indicators of a potential social engineering attempt. Recognizing these indicators can help identify similar threats in the future. What is the suspicious email address that sent the attachment?

To identify the sender of the phishing email, we analyzed the .eml file using an online email analysis tool. The file was uploaded to https://eml-analyzer.herokuapp.com/#/ which allowed us to inspect the email headers and metadata.

By reviewing the header information, we identified indicators of a social engineering attempt, including a suspicious sender address. The malicious attachment was sent from:

<img width="1716" height="835" alt="image" src="https://github.com/user-attachments/assets/44b2cc98-68fa-496c-909c-0443b10f0f80" />

#### Q2. The ransomware was identified as part of a known malware family. Determining its family name can provide critical insights into its behavior and remediation strategies. What is the family name of the ransomware identified during the investigation?

To identify the ransomware family, we analyzed the .eml file using the same email analysis tool ( https://eml-analyzer.herokuapp.com/#/ ). At the bottom of the analysis results, we obtained the SHA256 hash of the malicious attachment.

<img width="1717" height="766" alt="image" src="https://github.com/user-attachments/assets/27c3ff22-f2dc-490a-8044-9ac9151a51f5" />

Using this hash, we performed a lookup on VirusTotal, which provides detailed information about detected malware. From the analysis results and Family Labels, we were able to identify the ransomware family as:

<img width="1917" height="685" alt="image" src="https://github.com/user-attachments/assets/49aee6c9-1b30-489a-86d2-8b0719bcd52d" />

#### Q3. Upon execution, the ransomware dropped a file onto the compromised system to initiate its payload. Identifying this file is essential for understanding its infection process. What is the name of the first file dropped by the ransomware?

To identify the first file dropped by the ransomware, we analyzed its behavior using a sandbox execution environment. By reviewing the execution results on [Threat.rip](https://www.threat.rip/file/630325cac09ac3fab908f903e3b00d0dadd5fdaa0875ed8496fcbb97a558d0da/video), we observed the ransomware’s activity after running the malicious attachment.

From the sandbox execution video, we can see the initial payload execution process, where the ransomware drops its first file on the compromised system:
<img width="1918" height="812" alt="image" src="https://github.com/user-attachments/assets/d654e2ca-7a4a-4744-90be-33bd009ff0ed" />

#### Q4. Inside the dropped file, the malware contained hardcoded artifacts, including usernames and passwords that could provide clues about its origins or configuration. What is the only person's username found within the dropped file?





