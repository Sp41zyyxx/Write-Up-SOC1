Uncover the secrets of the new emerging threat, the Boogeyman.

Artefacts

For the investigation proper, you will be provided with the following artefacts:

Copy of the phishing email (dump.eml)
Powershell Logs from Julianne's workstation (powershell.json)
Packet capture from the same (capture.pcapng)

TASK 2
The Boogeyman is here!
we know that the compromise started with a phishing email. Let's start with analysing the dump.eml file located in the artefacts directory.

Q1.What is the email address used to send the phishing email?
The sender’s email address is visible in the From header.

Q2.What is the email address of the victim?
The victim’s email address is visible in the email headers, specifically in the To: field.

Q3.What is the name of the third-party mail relay service used by the attacker based on the DKIM-Signature and List-Unsubscribe headers?
By inspecting the DKIM-Signature and List-Unsubscribe headers in the email, we can determine the third-party mail relay service used by the attacker.
Tip: You can use cat and grep to filter these headers.

Q4.What is the name of the file inside the encrypted attachment?
To identify the file name, the dump.eml file must be saved locally. The encrypted attachment reveals the file name once extracted.

Q5.What is the password of the encrypted attachment?
The password of the encrypted attachment is visible between the <strong> tags in the email body. The full body can be viewed using cat dump.eml.

Q6.Based on the result of the lnkparse tool, what is the encoded payload found in the Command Line Arguments field?
After extracting Invoice.zip, the encoded payload can be identified by analyzing the .lnk file with lnkparse, specifically in the Command Line Arguments field.


TASK 3

Q1.What are the domains used by the attacker for file hosting and C2? Provide the domains in alphabetical order. (e.g. a.domain.com,b.domain.com)
We searched for ScriptBlockText in powershell.json because it logs the full PowerShell commands executed, including URLs used for payload download and command-and-control communication. By extracting and parsing these URLs, we identified the attacker-controlled domains.

Q2.What is the name of the enumeration tool downloaded by the attacker?
By inspecting the ScriptBlockText PowerShell logs and filtering for GitHub URLs, we identified that the attacker downloaded a publicly available enumeration tool hosted on GitHub.

Q3.What is the file accessed by the attacker using the downloaded sq3.exe binary? Provide the full file path with escaped backslashes.
We analyzed PowerShell Script Block logs to identify attacker activity. To remove benign PowerShell internal noise (Set-StrictMode) and extract only meaningful commands, we used:
cat powershell.json | jq -r '.. | .ScriptBlockText? // empty' | grep -v "Set-StrictMode"
This provided a clean view of attacker‑executed PowerShell commands used for downloads, enumeration, and post‑exploitation activity.

Q4.What is the software that uses the file in Q3?
We can see it in the location of the Q3 file.

Q5.What is the name of the exfiltrated file?
We used grep "file" in powershell.json to find it.

Q6.What is the name of the exfiltrated file?
Search on internet

Q7.What is the encoding used during the exfiltration attempt of the sensitive file?
The encoding used during the exfiltration attempt can be identified by examining the same PowerShell command line used to access the file in Q3.

Q8.What is the tool used for exfiltration?
The tool used for exfiltration can be identified by examining the same PowerShell command line used to answer Q7.

TASK 4

Q1.What software is used by the attacker to host its presumed file/payload server?
The hosting software was identified by analyzing the HTTP headers in Wireshark. By inspecting the HTTP GET request for sq3.exe, the server banner revealed the software used to host the payload.

Q2.What HTTP method is used by the C2 for the output of the commands executed by the attacker?
The HTTP method used by the C2 was identified by analyzing the PowerShell command. The command output is sent back to the C2 server using an Invoke-WebRequest request with the -Method POST parameter.

Q3.What is the protocol used during the exfiltration activity?
Encoded data was observed being sent within repeated domain name queries as part of the exfiltration activity. TIP: No. 33244

Q4.What is the password of the exfiltrated file?
To identify the password, we analyzed the same packet capture used in Q1. We followed the relevant stream (stream 750), extracted the hexadecimal data, and decoded it using CyberChef, which revealed the password of the exfiltrated file.

Q5.What is the credit card number stored inside the exfiltrated file?
tshark -r capture.pcapng  -Y 'dns' -T fields -e dns.qry.name |grep ".bpakcaging.xyz" | cut -f1 -d '.'|grep -v -e "files" -e "cdn" | uniq | tr -d '\\n' > extracted.txt
use from Hex on cyberchef, save the result like protected_data.kdbx and use the password
