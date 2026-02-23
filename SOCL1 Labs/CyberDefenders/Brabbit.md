https://cyberdefenders.org/blueteam-ctf-challenges/brabbit/ 
##### DIFFICULT = `MEDIUM`
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

To identify the username contained within the dropped file, we analyzed public threat intelligence related to the ransomware. We reviewed the technical analysis published by Kaspersky on https://securelist.com/bad-rabbit-ransomware/82851/

From the report and supporting images, we observed that the malware contained hardcoded credentials inside the dropped file, including a specific username. The only person's username identified in the analysis is:

<img width="1858" height="727" alt="image" src="https://github.com/user-attachments/assets/36851455-5e14-4892-a6ac-f12a5dfa3e14" />

#### Q5. After execution, the ransomware communicated with a C2 server. Recognizing its communication techniques can assist in mitigation. What MITRE ATT&CK sub-technique describes the ransomware’s use of web protocols for sending and receiving data?

We analyzed the sample on [Hybrid Analysis](https://hybrid-analysis.com/sample/630325cac09ac3fab908f903e3b00d0dadd5fdaa0875ed8496fcbb97a558d0da) and reviewed the MITRE ATT&CK sub-techniques section. Searching for “Web Protocols” shows the technique used by the ransomware for C2 communication.

<img width="1875" height="836" alt="image" src="https://github.com/user-attachments/assets/70963375-6f94-432c-990c-bce4ada685fd" />

#### Q6. Persistence mechanisms are a hallmark of sophisticated ransomware. Identifying how persistence was achieved can aid in recovery and prevention of reinfection. What is the MITRE ATT&CK Sub-Technique ID associated with the ransomware’s persistence technique?

We analyzed the sample on Hybrid Analysis and reviewed the MITRE ATT&CK section. By searching for “persistence”, we found the technique describing the initial or recurring execution of malicious code, which indicates how the ransomware maintains persistence.

<img width="1667" height="772" alt="image" src="https://github.com/user-attachments/assets/b0e13cd2-38e0-4679-9a63-c26a609a4820" />

#### Q7. As part of its infection chain, the ransomware created specific tasks to ensure its continued operation. Recognizing these tasks is crucial for system restoration. What are the names of the tasks created by the ransomware during execution?

We analyzed the execution timeline in ANY.RUN and reviewed the commands executed by the malware. By inspecting the schtasks activity, we identified the scheduled tasks created by the ransomware to maintain execution and persistence.

The tasks created during execution are:

`schtasks /Create /RU SYSTEM /SC ONSTART /TN (*USER*) /TR "C:\WINDOWS\system32\cmd.exe /C Start \"\" \"C:\Windows\dispci.exe\" -id 970686855 && exit"`

`/c schtasks /Create /SC once /TN (*USER*) /RU SYSTEM /TR "C:\WINDOWS\system32\shutdown.exe /r /t 0 /f" /ST 08:58:00`

<img width="1860" height="801" alt="image" src="https://github.com/user-attachments/assets/fd6ea944-e3bc-4cf4-85bd-97b43d138d3b" />

#### Q8. he malicious binary dispci.exe displayed a suspicious message upon execution, urging users to disable their defenses. This tactic aimed to evade detection and enable the ransomware's full execution. What suspicious message was displayed in the Console upon executing this binary?

We analyzed the binary execution using [ANY.RUN](https://app.any.run/tasks/c7f11627-5d84-42d4-a18f-991f0c4e3215). By reviewing the process execution and console output, we observed the message displayed in the CMD window urging users to disable their defenses.

<img width="1830" height="816" alt="image" src="https://github.com/user-attachments/assets/58980287-b73b-49a0-a4f6-aea1fa04a7ed" />

#### Q9. To modify the Master Boot Record (MBR) and encrypt the victim’s hard drive, the ransomware utilized a specific driver. Recognizing this driver is essential for understanding the encryption mechanism. What is the name of the driver used to encrypt the hard drive and modify the MBR?

Read https://securelist.com/bad-rabbit-ransomware/82851/

<img width="1867" height="836" alt="image" src="https://github.com/user-attachments/assets/e23e20ec-b5c7-4adf-8fb5-c9655e2ce4b6" />

#### Q10. Attribution is key to understanding the threat landscape. The ransomware was tied to a known attack group through its tactics, techniques, and procedures (TTPs). What is the name of the threat actor responsible for this ransomware campaign?

https://malpedia.caad.fkie.fraunhofer.de/details/win.eternal_petya

#### Q11. The ransomware rendered the system unbootable by corrupting critical system components. Identifying the technique used provides insight into its destructive capabilities. What is the MITRE ATT&CK ID for the technique used to corrupt the system firmware and prevent booting?

https://mitre.ptsecurity.com/en-US/T1495

