# SOC Malware Detection Lab using Splunk

## Objective

The objective of this project is to design and implement a controlled SOC home lab to simulate a malware infection on a Windows endpoint and analyze the resulting security events using Splunk SIEM. The project focuses on endpoint visibility, log collection, and detection of suspicious activities within an isolated internal network, reflecting real-world SOC monitoring and investigation workflows.

### Skills Learned

- Network segmentation using internal networks to safely simulate attacks.
- Malware payload generation and delivery simulation for security testing purposes.
- Performing network reconnaissance and service enumeration using Nmap.
- Monitoring Windows endpoint activity through security and system logs.
- Collecting and analyzing logs using Splunk SIEM.
- Correlating endpoint events to identify suspicious and malicious behavior.
- Understanding the malware lifecycle from initial access to execution.
- Investigating security incidents using event timelines and log correlation.
- Applying SOC and Blue Team methodologies for detection and analysis.

### Tools Used

- Splunk SIEM – Log ingestion, correlation, searching, and security event analysis.
- Kali Linux – Attacker machine used for reconnaissance and malware delivery simulation.
- Windows 10 – Target endpoint for malware execution and security event generation.
- Nmap – Network scanning and service enumeration.
- msfvenom – Malware payload generation for simulation purposes.
- Python HTTP Server – Hosting and delivering the simulated malicious payload.
- VirtualBox / VMware – Virtualization platform for building an isolated lab environment.
- Windows Event Viewer – Reviewing and validating endpoint security logs.

## Steps

Both the attacker (Kali Linux) and the victim (Windows) machines are configured on the same isolated internal network with assigned IP addresses. This setup ensures a controlled lab environment and allows direct communication between the machines while remaining fully isolated from the host system and external networks.

<img width="498" height="320" alt="Screenshot 2025-12-24 195353" src="https://github.com/user-attachments/assets/efa8ddfe-3948-49e9-8074-5827611c6ad7" />
<img width="422" height="336" alt="Screenshot 2025-12-24 195521" src="https://github.com/user-attachments/assets/561aa06e-1591-40e6-983b-65e83447b083" />



A successful ICMP ping test from the Windows machine to the Kali Linux attacker confirms proper network connectivity and communication within the internal lab environment.

<img width="491" height="305" alt="Screenshot 2025-12-24 195736" src="https://github.com/user-attachments/assets/63cec45a-7289-40b1-bb91-42604ed4d156" />


An Nmap scan was performed against the Windows target to enumerate open ports and running services. The results indicate that port 3389 (RDP) is open, revealing a potential attack surface that will be assessed in later stages of the project.

<img width="405" height="337" alt="Screenshot 2025-12-24 201251" src="https://github.com/user-attachments/assets/0ab9b60f-5298-4ab0-8181-4655445aa85c" />


A malicious payload was generated using msfvenom to simulate a real-world malware delivery scenario. This payload will later be used to observe endpoint behavior and security event generation.

<img width="407" height="317" alt="Screenshot 2025-12-24 202414" src="https://github.com/user-attachments/assets/0d88839f-4584-4871-9fbf-17cb0b65b76e" />



A Metasploit multi/handler listener was configured to simulate a command-and-control connection following malware execution. This step establishes a controlled session used solely to generate endpoint activity and security events for monitoring and detection within the SOC lab environment.

<img width="407" height="306" alt="Screenshot 2025-12-24 203317" src="https://github.com/user-attachments/assets/7b673a0c-518c-4691-ae60-f4ffb66db6c3" />


A lightweight HTTP server was started on the attacker machine to host the malicious payload and simulate malware delivery within the internal lab environment.

<img width="402" height="307" alt="Screenshot 2025-12-25 010432" src="https://github.com/user-attachments/assets/e81f679e-9806-4eea-9790-e8ee60cc51a5" />


Windows Task Manager was used to verify that the downloaded malicious file (mal.pdf.exe) was successfully executed on the system. The presence of the malware process confirms execution on the Windows endpoint and marks the beginning of observable activity for subsequent monitoring and analysis.

<img width="386" height="115" alt="Screenshot 2025-12-24 211540" src="https://github.com/user-attachments/assets/ee171f9e-f5f6-491d-85d7-f892989e756a" />


A search was performed in Splunk using the malicious file name to identify all related security events. The resulting logs provide insight into the malware execution on the Windows endpoint and allow correlation between file activity and associated system behavior.

<img width="491" height="358" alt="Screenshot 2025-12-25 021450" src="https://github.com/user-attachments/assets/d1a0284d-27d5-48de-a7ad-cafcaa9e60ee" />

Following the confirmation of malware execution on the Windows endpoint, Splunk was used to search for events associated with the attacker machine’s IP address. The resulting logs highlight network activity related to the compromise and help correlate endpoint execution with external communication observed during the incident.

<img width="493" height="353" alt="Screenshot 2025-12-25 022904" src="https://github.com/user-attachments/assets/a06bf70d-fffa-49a9-bca1-912e8d457c19" />


A detailed review of a specific security event was performed in Splunk to examine its associated metadata. Key fields such as the process ID and process GUID were identified at this stage, providing critical context and serving as pivot points for deeper investigation in subsequent searches.

<img width="481" height="362" alt="Screenshot 2025-12-25 021639" src="https://github.com/user-attachments/assets/2209c4b5-f61d-4505-8f5e-ace9fbd3df61" />


The process GUID associated with the malicious execution was extracted and used as a pivot for deeper investigation in Splunk. By correlating events and enriching the search with key fields, a clearer execution chain was reconstructed to understand how the attacker-initiated process was launched and operated on the system.

<img width="490" height="261" alt="Screenshot 2025-12-25 022749" src="https://github.com/user-attachments/assets/781f081c-df68-4550-97b9-513ca4f81b68" />



