https://cyberdefenders.org/blueteam-ctf-challenges/honeybot/

##### Difficult = `Medium`

##### Category: `Network Forensics`

##### Tactics: `Initial Access` `Execution` `Privilege Escalation` `Defense Evasion` `Command and Control`

##### Tools: `Brim` `NetworkMiner` `Wireshark` `Libemu (sctest)` `scdbg` `IP LookUp`

---

#### Q1. What is the attacker's IP address? 
By analyzing the SOCKS protocol traffic in the PCAP, we identified the attacker's source IP address in the SOCKS connection request.

#### Q2. What is the target's IP address?
Same as Q1 
<img width="1917" height="847" alt="image" src="https://github.com/user-attachments/assets/752e3fa2-d4db-410f-8f04-48fd008a7686" />

#### Q3. Provide the country code for the attacker's IP address (a.k.a geo-location).
After identifying the attacker’s IP address, we performed a WHOIS and geolocation lookup using an online IP intelligence service.
The lookup results indicate that the IP address is registered in [COUNTRY NAME], with the country code [CC].
<img width="1271" height="847" alt="image" src="https://github.com/user-attachments/assets/9fdfe195-527e-4b90-a4ba-f88462b7798c" />

#### Q4. How many TCP sessions are present in the captured traffic?
To determine the number of TCP sessions in the captured traffic, we navigated to Statistics → Conversations in Wireshark and selected the TCP tab. The total number of entries shown corresponds to the number of TCP sessions present in the capture.
<img width="1918" height="1047" alt="image" src="https://github.com/user-attachments/assets/c8658380-c431-40f0-bd44-793b07ecbd59" />

#### Q5. How long did it take to perform the attack (in seconds)?
Since the time display format was set to “Seconds Since Beginning of Capture”, the timestamp of the last packet directly indicates the total duration of the attack. Therefore, the attack lasted [xx] seconds.

#### Q6. Provide the CVE number of the exploited vulnerability.
By navigating to Statistics → Endpoints, we identified TCP traffic on port 1957. After applying a filter for that specific port, we analyzed the related packets and observed traffic associated with Active Directory services. Further inspection of the exploit pattern allowed us to identify the vulnerability being targeted
`ip.addr==192.150.11.111 && tcp.port==1957`
<img width="1918" height="887" alt="image" src="https://github.com/user-attachments/assets/9d6754a6-c0a4-4309-ae68-f7463ad03604" />
<img width="1912" height="1008" alt="image" src="https://github.com/user-attachments/assets/7b72e704-0e63-4e60-8746-97ca054d32b0" />

#### Q7. Which protocol was used to carry over the exploit?
<img width="1918" height="883" alt="image" src="https://github.com/user-attachments/assets/15cf8c40-7f76-4b9b-a6e1-0a4522487b71" />

#### Q8. Which protocol did the attacker use to download additional malicious files to the target system?
#### Q9. What is the name of the downloaded malware?
#### Q10. The attacker's server was listening on a specific port. Provide the port number.

FILTER `tcp.stream eq 2` here we have answers for Q8, Q9 and Q10
<img width="1918" height="1006" alt="image" src="https://github.com/user-attachments/assets/248c0572-4e90-4e54-b36d-a5097f2bd9cd" />

#### Q11. When was the involved malware first submitted to VirusTotal for analysis? Format: YYYY-MM-DD
By applying the filter tcp.stream eq 2, we isolated the relevant TCP stream containing the malware payload.
We then exported the stream in raw format and calculated its hash (MD5/SHA256).
Using this hash, we searched for the sample on VirusTotal and identified the first submission date, which indicates when the malware was initially uploaded for analysis.

#### Q12.What is the key used to encode the shellcode?
0X99
#### Q13.What is the port number the shellcode binds to?
1957
#### Q14. The shellcode used a specific technique to determine its location in memory. What is the OS file being queried during this process?
kernel32.dll
