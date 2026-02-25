https://cyberdefenders.org/blueteam-ctf-challenges/oski/

##### Difficult = Easy

##### Category: `Threat Intel`

##### Tactics: `Initial Access` `Execution` `Defense Evasion` `Credential Access` `Command and Control` `Exfiltration`

##### Tools: `VirusTotal` `ANY.RUN`

---

#### Q1. Determining the creation time of the malware can provide insights into its origin. What was the time of malware creation?
Using VirusTotal, we can see the creation time in the `Details` section.  
<img width="1476" height="877" alt="image" src="https://github.com/user-attachments/assets/f073a52b-34d7-4cc9-95b9-b5976006283e" />

#### Q2. Identifying the command and control (C2) server that the malware communicates with can help trace back to the attacker. Which C2 server does the malware in the PPT file communicate with?
<img width="1560" height="636" alt="image" src="https://github.com/user-attachments/assets/4c04a263-c275-415d-a74d-6deaff89c3c1" />

#### Q3. Identifying the initial actions of the malware post-infection can provide insights into its primary objectives. What is the first library that the malware requests post-infection?
<img width="1560" height="648" alt="image" src="https://github.com/user-attachments/assets/50be0c4d-1be9-49ca-91e4-bf8dd3f7a3b8" />

#### Q4. By examining the provided Any.run report, what RC4 key is used by the malware to decrypt its base64-encoded string?
Use Any.run
<img width="1881" height="846" alt="image" src="https://github.com/user-attachments/assets/1cc660ba-936b-4301-8139-526b67fa65b2" />
<img width="1862" height="796" alt="image" src="https://github.com/user-attachments/assets/60d98ece-d72f-47b5-80dc-04c064ffb0b8" />


