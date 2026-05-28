# Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]
```
**A.Capturing Traffic in Wireshark**

+ Open Wireshark and start capturing on the active interface (Wi- Fi/Ethernet).

<img width="1920" height="1200" alt="Screenshot (79)" src="https://github.com/user-attachments/assets/14868f0e-1a6a-4971-adb6-99fc748246e6" />


* Perform activities like opening a website or sending an email through a client (e.g., Gmail via browser or Thunderbird).
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/1262e3f4-c363-44dd-aed7-df3cbcbc3f8a" />


**B. Analyzing Web Browser Artifacts**


* Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate browser traffic.

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/e7940a14-6354-4d97-979d-114b6e4f8f98" />


* Inspect HTTP GET/POST requests: 
  - Look for URLs, hostnames, user agents, and cookies in the HTTP headers.
  - Follow TCP Stream to reconstruct page request flow: Right-click a packet → Follow → TCP Stream.
  - Filter: dns o Reveal domains the browser tried to resolve.

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c10cd71c-9bd7-4433-b89e-23eadf74f27e" />

**C. Email Header Analysis**

* Apply relevant filters: 
  - For POP3: tcp.port == 110 o For SMTP: tcp.port == 25 or 587 o For IMAP: tcp.port == 143 or 993
 
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d935d11b-4655-4320-b3b9-3a2e6bb83835" />

* Locate email data: 
  - Look for SMTP packets to see sender/receiver email addresses.
  - Use "Follow TCP Stream" to view the full email headers and body if unencrypted.
 
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/30cba6c7-aa46-4c23-843c-e6de5ee902d2" />

* Extract Email Header Fields:
  - Analyze From, To, Subject, Date, Message-ID, and relay servers used in sending the email.


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/33493c33-7c18-4f75-9384-78f7b1decae3" />



## OUTPUT:
Captured Web Activity and Email Header Information

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c10cd71c-9bd7-4433-b89e-23eadf74f27e" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/33493c33-7c18-4f75-9384-78f7b1decae3" />



## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

