# Wireshark-SOC-Labs-Network-Traffic-Analysis-Forensic-Investigations
This repository documents six Security Operations Center (SOC) investigation labs completed as part of the Networkwalks Cybersecurity Internship (Module: Wireshark SOC Labs, Week 1 Extras).

## Overview
This repository documents six hands-on Security Operations Center (SOC) investigation labs completed using Wireshark as part of my Networkwalks Cybersecurity Internship. 

The exercises focused on:
* **Investigating** network packet captures (PCAP) to identify operational security anomalies and unauthorized access attempts.
* **Capturing** live and pre-recorded network traffic across multiple OSI layers.
* **Reconstructing** application-layer conversations using TCP stream analysis.
* **Detecting** credential leaks, brute-force attacks, and unencrypted session traffic.
* **Analyzing** real-time media protocols and Session Initiation Protocol (SIP) signaling for VoIP security.

---

## Tools & Technologies Used
* **Wireshark** (Packet Analyzer & DPI)
* **Ubuntu Linux**
* **TCP/IP Protocol Suite**
* **HTTP / HTTPS**
* **FTP**
* **SIP & RTP**

---

## Lab Investigations

### Lab 3: Identify the Attacker's IP
* **Scenario:** An unauthorized host on the network initiated malicious scanning activity against internal subnets.
* **Objective:** Locate the specific IP address belonging to the attacker by analyzing baseline network traffic.
* **Investigation:** Filtered ARP requests and IP connection patterns across host interfaces to pinpoint the origin of suspicious traffic spikes.
* **Key Learning:** How to isolate attacker IP addresses using Wireshark filter syntax (`ip.src` / `ip.dst`) and examine basic packet header properties.

#### Evidence
<img width="1357" height="767" alt="Screenshot 2026-11-05 225222" src="https://github.com/user-attachments/assets/4a91e6fa-8b51-4285-a406-db62620461eb" />


---

### Lab 4: Follow TCP Stream (Part 1)
* **Scenario:** A suspicious TCP session was captured, containing plain-text payload transmissions between an internal client and a remote server.
* **Objective:** Reconstruct the complete client-server conversation using Wireshark's stream follow capabilities.
* **Investigation:** Applied TCP display filters (`tcp.stream eq 0`), followed the entire TCP conversation stream, and parsed ascii text data exchanged during the session.
* **Key Learning:** TCP stream reconstruction allows analysts to read full session contents without manually piecing together individual packet segments.

#### Evidence
<img width="1357" height="767" alt="Screenshot 2026-11-05 225528" src="https://github.com/user-attachments/assets/19281710-035d-4505-9677-3279953adf7e" />



---

### Lab 5: Follow TCP Stream (Part 2)
* **Scenario:** A multi-turn TCP session was established involving larger data transfers and potential protocol negotiation.
* **Objective:** Analyze secondary TCP streams to evaluate data exchange flags, sequence numbers, and payload data.
* **Investigation:** Inspected `[SYN]`, `[SYN-ACK]`, and `[ACK]` three-way handshake sequences, followed secondary streams (`tcp.stream eq 4`), and identified transacted data lengths.
* **Key Learning:** Deep packet inspection of TCP handshake states helps identify session hijacking, unexpected payload delivery, or broken session logic.

#### Evidence
<img width="1359" height="766" alt="Screenshot 2026-11-05 230047" src="https://github.com/user-attachments/assets/530a5035-069a-4d42-b63c-0048800cdb27" />



---

### Lab 6: HTTP Plain Text Credentials
* **Scenario:** An old staff portal still runs on plain HTTP. An unauthorized entity captured traffic to extract cleartext sign-in credentials.
* **Objective:** Identify the HTTP request method, web page path, and the cleartext credentials submitted via the web form.
* **Investigation:** Filtered for `http.request.method == "POST"`, located the `/login` path request, and expanded the `HTML Form URL Encoded` packet structure to expose cleartext parameters (`username=Farhan.k&password=Mango2025`).
* **Key Learning:** Plaintext HTTP web forms transmit sensitive authentication data unencrypted, leaving credentials exposed to basic packet sniffing.

#### Evidence
<img width="1356" height="767" alt="Screenshot 2026-11-05 230442" src="https://github.com/user-attachments/assets/dfa67ddc-ea81-4013-8510-64e7f89591b4" />


---

### Lab 7: FTP Brute Force Catch
* **Scenario:** The owner of an FTP server reported multiple failed login attempts occurring in rapid succession within a short time window.
* **Objective:** Identify the targeted FTP server IP, verify the protocol involved, count total failed login attempts, and confirm if access was obtained.
* **Investigation:** Evaluated `Statistics > Protocol Hierarchy` to confirm high FTP traffic volume (31.7% of total capture), identified target IP `192.168.10.20`, and filtered for server response codes (`ftp.response.code == 530`) to document 8 failed login attempts.
* **Key Learning:** Brute-force attacks targeting unencrypted protocols like FTP create distinct high-frequency footprint patterns in Wireshark packet captures.

#### Evidence
<img width="1359" height="767" alt="Screenshot 2026-11-05 231034" src="https://github.com/user-attachments/assets/53148bb2-e372-42d5-a0b2-60c42e174ebb" />


---

### Lab 8: VoIP Call Replay
* **Scenario:** A corporate phone call was executed over an unencrypted VoIP deployment. Traffic was captured to review signaling parameters and reconstruct spoken voice content.
* **Objective:** Distinguish between signaling and media protocols, extract caller extensions, identify the display name, identify the audio codec, and replay the call.
* **Investigation:** Identified SIP (`INVITE`) as the call setup protocol and RTP as the voice media carrier. Inspected SIP `From:` headers to identify extension `101` ("Ali Raza"), parsed RTP packet headers to confirm the `G.711 PCMU` codec, and utilized `Telephony > VoIP Calls` to decode and replay the call.
* **Key Learning:** VoIP traffic lacking encryption exposes call metadata (extension, caller name) via SIP headers and voice payloads via RTP streams.

#### Evidence
<img width="1359" height="767" alt="Screenshot 2026-11-05 231540" src="https://github.com/user-attachments/assets/034ed7aa-a452-4dee-a28d-f521b947edd9" />


---

## Skills Developed
* Network Traffic Analysis & Deep Packet Inspection (DPI)
* TCP Stream Reconstruction & Conversation Tracking
* IP Address & Port Scanning Investigation
* HTTP Security & Cleartext Authentication Exposure Analysis
* Brute-Force Attack Detection & Response Code Filtering
* SIP/RTP Analysis & VoIP Security Fundamentals
* Wireshark Display Filtering & Statistics Analysis

---

## Conclusion
Completing these six SOC labs provided practical, hands-on experience in analyzing real-world network packet captures, identifying security threats, and dissecting protocol vulnerabilities. This project represents continuous hands-on development in Security Operations Center methodologies and forensic packet analysis.

* **Programme:** Networkwalks Cybersecurity Internship
* **Module:** Wireshark SOC Labs
* **Track:** Week 1 Extras
* **Platform:** Networkwalks SOC Practice Labs
* **Primary Tools:** Wireshark
* **Author:** Rushna Imran
* **Linkedin:**  [RushnaIMRAN](https://www.linkedin.com/in/rushna-imran-3338303b6/)

---
*Disclaimer: All investigations were performed in authorized training lab environments.*
