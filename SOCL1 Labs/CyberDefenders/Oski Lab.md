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

#### Q5. By examining the MITRE ATT&CK techniques displayed in the Any.run sandbox report, identify the main MITRE technique (not sub-techniques) the malware uses to steal the user’s password.
<img width="1872" height="824" alt="image" src="https://github.com/user-attachments/assets/4ab9bd03-0218-4be1-ac55-ca85876cdb83" />
<img width="1870" height="847" alt="image" src="https://github.com/user-attachments/assets/54443349-4c88-42a1-a955-7ca55f0817c1" />

#### Q6. By examining the child processes displayed in the Any.run sandbox report, which directory does the malware target for the deletion of all DLL files?
<img width="1020" height="930" alt="image" src="https://github.com/user-attachments/assets/767996ed-ac26-479d-8195-441f9fdbac2e" />

#### Q7. Understanding the malware's behavior post-data exfiltration can give insights into its evasion techniques. By analyzing the child processes, after successfully exfiltrating the user's data, how many seconds does it take for the malware to self-delete?
<img width="1015" height="896" alt="image" src="https://github.com/user-attachments/assets/6b7832b4-82ff-4ab8-b1be-5502b48b8635" />





