https://cyberdefenders.org/blueteam-ctf-challenges/xworm/

##### Difficult == `Medium`

##### Category: `Malware Analysis`

##### Tactics: `Execution` `Persistence` `Privilege Escalation` `Defense Evasion` `Credential Access` `Discovery` `Collection`

##### Tools: `Detect It Easy` `CFF Explorer` `PEStudio` `dnSpy` `ProcMon` `RegShot` `Python3`

--- 

#### Q1. What is the compile timestamp (UTC) of the sample?
First, we need the SHA-256 hash of the malware. To obtain this, we use the command `sha256sum XWorm.Malware` at the malware's location. We will then use VirusTotal to analyse the result. 
<img width="1262" height="867" alt="image" src="https://github.com/user-attachments/assets/31aeb104-84c8-492f-a65e-dffbef2f1f5a" />

#### Q2. Which legitimate company does the malware impersonate in an attempt to appear trustworthy?
In the details section, we can see the 'File version information'.
<img width="1442" height="912" alt="image" src="https://github.com/user-attachments/assets/d017e0e9-9527-4930-bac5-956a92e60721" />

#### Q3. How many anti-analysis checks does the malware perform to detect/evade sandboxes and debugging environments?
Use `strings XWorm.malware | grep -i debug`

<img width="681" height="138" alt="image" src="https://github.com/user-attachments/assets/9b055b24-d002-4861-8118-db49e8b16888" />

#### Q4. What is the name of the scheduled task created by the malware to achieve execution with elevated privileges?
#### Q5. What is the filename of the malware binary that is dropped in the AppData directory?
Using https://app.any.run/tasks/77c9f72f-0af9-4390-9b6f-13a6eb5d07e0 we can see `Q4` and `Q5`:
<img width="763" height="751" alt="image" src="https://github.com/user-attachments/assets/00ffc4a4-e04e-4a85-90c1-9173ec4ebb1a" />

#### Q6. Which cryptographic algorithm does the malware use to encrypt or obfuscate its configuration data?
We can see it at this page https://www.joesandbox.com/analysis/1796812/0/pdf 
<img width="1918" height="858" alt="image" src="https://github.com/user-attachments/assets/5c18c71b-920e-4c35-af39-79f90a8dc729" />

#### Q7. To derive the parameters for its encryption algorithm (such as the key and initialization vector), the malware uses a hardcoded string as input. What is the value of this hardcoded string?
The malware derives its AES encryption key by computing the MD5 hash of a hardcoded string.
In the function f5Mo9y1FK1yJy4poW9CE, the string is retrieved from a static variable and passed to MD5CryptoServiceProvider.ComputeHash().
By locating the declaration of this variable in the decompiled source code using grep, we identified the literal value assigned to it.
This hardcoded value is used as the base material for key derivation.
use `grep -n "DhMybcleyUJ8bZbaqtAkL3FTz6SQ840xELBsFWt9yekNCVYQ1WgRtjL1bTF3" XWorm.decompiled.cs` for get `XWorm.decompiled.cs` i use: `ilspycmd XWorm.malware -o output_folder`

#### Q8.What are the Command and Control (C2) IP addresses obtained after the malware decrypts them?
#### Q9.What port number does the malware use for communication with its Command and Control (C2) server?
#### Q10.The malware spreads by copying itself to every connected removable device. What is the name of the new copy created on each infected device?

Using `https://www.joesandbox.com/analysis/1796812/0/pdf` on page 3 we can see Q8, Q9 and Q10
<img width="1907" height="855" alt="image" src="https://github.com/user-attachments/assets/2f79856e-f1a7-459f-988c-a372405428e3" />

#### Q11. To ensure its execution, the malware creates specific types of files. What is the file extension of these created files?
Using `https://app.any.run/tasks/d55e2294-5377-4a45-b393-f5a8b20f7d44` we can see the activities.
<img width="1918" height="860" alt="image" src="https://github.com/user-attachments/assets/02c9d2de-6bca-4a9a-9a68-4945a0a180c9" />

#### Q12. What is the name of the DLL the malware uses to detect if it is running in a sandbox environment?
Using `https://www.joesandbox.com/analysis/1796812/0/pdf` on page 3 we can see `Evasion Techniques`
<img width="1918" height="802" alt="image" src="https://github.com/user-attachments/assets/23f705c6-2498-4186-946e-962a69e64016" />

#### Q13. What is the name of the registry key manipulated by the malware to control the visibility of hidden items in Windows Explorer?
We have to use `cat XWorm.decompiled.cs | grep "Hidden"`
<img width="1918" height="500" alt="image" src="https://github.com/user-attachments/assets/d1c7ed30-45ee-4ad7-9d54-f64a40ad2598" />

#### Q14. Which API does the malware use to mark its process as critical in order to prevent termination or interference?
We have to use `cat XWorm.decompiled.cs | grep -i "critical"`
<img width="923" height="40" alt="image" src="https://github.com/user-attachments/assets/92133af5-5d43-412b-b311-e30210c66ec7" />

#### Q15. Which API does the malware use to insert keyboard hooks into running processes in order to monitor or capture user input?
Using `cat XWorm.decompiled.cs | grep -i "hook"` we gonna get the answer.
<img width="1101" height="72" alt="image" src="https://github.com/user-attachments/assets/01c6bddc-78b7-4598-a8d3-06a27e940b5b" />

#### Q16. Given the malware’s ability to insert keyboard hooks into running processes, what is its primary functionality or objective?
<img width="1918" height="642" alt="image" src="https://github.com/user-attachments/assets/b9778a1d-4049-4d38-b326-15a3ac23e392" />
