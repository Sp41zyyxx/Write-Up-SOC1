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
use `grep -n "DhMybcleyUJ8bZbaqtAkL3FTz6SQ840xELBsFWt9yekNCVYQ1WgRtjL1bTF3" XWorm.decompiled.cs` 







