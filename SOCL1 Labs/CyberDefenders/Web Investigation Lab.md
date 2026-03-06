https://cyberdefenders.org/blueteam-ctf-challenges/web-investigation/

##### Difficult == `Medium`

##### Category: `Network Forensics`

##### Tactics: `Initial Access` `Persistence` `Command and Control`

##### Tools: `Wireshark` `Network Miner`

---

#### Q1. By knowing the attacker's IP, we can analyze all logs and actions related to that IP and determine the extent of the attack, the duration of the attack, and the techniques used. Can you provide the attacker's IP?
Using `http.request.method == "GET"` we can see sqli injections 
<img width="1918" height="337" alt="image" src="https://github.com/user-attachments/assets/d6267026-f568-406d-8f73-b637f3ce6676" />

#### Q2. If the geographical origin of an IP address is known to be from a region that has no business or expected traffic with our network, this can be an indicator of a targeted attack. Can you determine the origin city of the attacker?
Use `https://www.iplocation.net/ip-lookup`

#### Q3. Identifying the exploited script allows security teams to understand exactly which vulnerability was used in the attack. This knowledge is critical for finding the appropriate patch or workaround to close the security gap and prevent future exploitation. Can you provide the vulnerable PHP script name?
Same packets as Q1

#### Q4. Establishing the timeline of an attack, starting from the initial exploitation attempt, what is the complete request URI of the first SQLi attempt by the attacker?
<img width="1668" height="332" alt="image" src="https://github.com/user-attachments/assets/7be5e3ad-3c36-45d4-8011-729aad18ec87" />

#### Q5. Can you provide the complete request URI that was used to read the web server's available databases?
`ip.dst == 111.224.250.131 and http.response.code == 200` No. 1525

#### Q6. Assessing the impact of the breach and data access is crucial, including the potential harm to the organization's reputation. What's the table name containing the website users data?
<img width="1918" height="892" alt="image" src="https://github.com/user-attachments/assets/f8caf7e6-bf3b-4ab4-9303-ecd2ae64e994" />

#### Q7. The website directories hidden from the public could serve as an unauthorized access point or contain sensitive functionalities not intended for public access. Can you provide the name of the directory discovered by the attacker?
<img width="1918" height="425" alt="image" src="https://github.com/user-attachments/assets/318f53a1-858d-404c-a53e-ff34a48c8dbf" />

#### Q8. Knowing which credentials were used allows us to determine the extent of account compromise. What are the credentials used by the attacker for logging in?
<img width="1550" height="993" alt="image" src="https://github.com/user-attachments/assets/e4e2f719-9397-4fd8-83ba-d61afc450905" />

#### Q9. We need to determine if the attacker gained further access or control of our web server. What's the name of the malicious script uploaded by the attacker?

<img width="1536" height="973" alt="image" src="https://github.com/user-attachments/assets/6ce8ea9c-68e8-47ae-88fd-6171634676ec" />


