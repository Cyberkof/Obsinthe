Email Phishing

Email phishing is one of the main precursors of any cyber attack. Unsuspecting users get duped into opening and accessing malicious files and links sent to them by email, as they appear to be legitimate. As a result, adversaries infect their victims’ systems with malware, harvesting their credentials and personal data and performing other actions such as financial fraud or conducting ransomware attacks.

For more information and content on phishing, check out these rooms:

- [Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe)
- [Phishing Emails 2](https://tryhackme.com/room/phishingemails2rytmuv)
- [Phishing Emails 3](https://tryhackme.com/room/phishingemails3tryoe)
- [Phishing Emails 4](https://tryhackme.com/room/phishingemails4gkxh)
- [Phishing Emails 5](https://tryhackme.com/room/phishingemails5fgjlzxc)

[PhishTool](https://www.phishtool.com/) seeks to elevate the perception of phishing as a severe form of attack and provide a responsive means of email security. Through email analysis, security analysts can uncover email IOCs, prevent breaches and provide forensic reports that could be used in phishing containment and training engagements.

PhishTool has two accessible versions: **Community** and **Enterprise**. We shall mainly focus on the Community version and the core features in this task. Sign up for an account via this [link](https://app.phishtool.com/sign-up/community) to use the tool. **Note**: The tool may be geo-blocked in some locations, and therefore you can take appropriate action towards accessing it.

The core features include:

- **Perform email analysis:** PhishTool retrieves metadata from phishing emails and provides analysts with the relevant explanations and capabilities to follow the email’s actions, attachments, and URLs to triage the situation.
- **Heuristic intelligence:** OSINT is baked into the tool to provide analysts with the intelligence needed to stay ahead of persistent attacks and understand what TTPs were used to evade security controls and allow the adversary to social engineer a target.
- **Classification and reporting:** Phishing email classifications are conducted to allow analysts to take action quickly. Additionally, reports can be generated to provide a forensic record that can be shared.

Additional features are available on the Enterprise version:

- Manage user-reported phishing events.
- Report phishing email findings back to users and keep them engaged in the process.
- Email stack integration with Microsoft 365 and Google Workspace.

We are presented with an upload file screen from the Analysis tab on login. Here, we submit our email for analysis in the stated file formats. Other tabs include:

- **History:** Lists all submissions made with their resolutions.
- **In-tray:** An Enterprise feature used to receive and process phish reports posted by team members through integrating Google Workspace and Microsoft 365.

![PhishTool Dashboard](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/4c5d66d92d6aeb83d67961be5239842d.png)

### Analysis Tab

Once uploaded, we are presented with the details of our email for a more in-depth look. Here, we have the following tabs:

- **Headers:** Provides the routing information of the email, such as source and destination email addresses, Originating IP and DNS addresses and Timestamp.
- **Received Lines:** Details on the email traversal process across various SMTP servers for tracing purposes.
- **X-headers:** These are extension headers added by the recipient mailbox to provide additional information about the email.
- **Security:** Details on email security frameworks and policies such as Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM) and Domain-based Message Authentication, Reporting and Conformance (DMARC).
- **Attachments:** Lists any file attachments found in the email.
- **Message URLs:** Associated external URLs found in the email will be found here.

We can further perform lookups and flag indicators as malicious from these options. On the right-hand side of the screen, we are presented with the Plaintext and Source details of the email.

![Email analysis](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/03364f3a4fb2177cce13abc3b181bca9.gif)

Above the **Plaintext** section, we have a **Resolve** checkmark. Here, we get to perform the resolution of our analysis by classifying the email, setting up flagged artefacts and setting the classification codes. Once the email has been classified, the details will appear on the **Resolution** tab on the analysis of the email.

![Email investigation resolution](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/b13d63d0c2fe177085a1b487efb4065e.gif)

# Phishing email analysis — concise Obsidian-ready summary

Use this as a single-note wrap-up. Copy into Obsidian and tag it (e.g., `#phishing`, `#email-forensics`, `#tryhackme`).

---

## Purpose

Quick reference for analyzing `.eml` phishing samples (Thunderbird, CLI, PhishTool) and extracting the **Originating IP**, counting hops, and writing up results for TryHackMe-style tasks.

---

## Tools used

- Thunderbird (GUI) — open `.eml` and view raw headers
    
- Terminal (Ubuntu VM) — `grep`, `awk`, `sed`, `python3` for parsing headers
    
- PhishTool (Community) — optional OSINT + parsing (upload `.eml`)
    
- VirtualBox shared folder — move `.eml` to host if VM has no internet
    

---

## Key concepts / heuristics (memorize these)

- **Read `Received:` headers bottom → up.** The bottom-most `Received:` entry is the earliest hop (closest to sender).
    
- **Prefer `X-Originating-IP:`** if present — it explicitly names the sender IP.
    
- **Pick the first public IPv4** in the bottom-most `Received:` (ignore private/internal addresses).
    
- **Ignore RFC1918 private IPs** when identifying public origin:
    
    - `10.0.0.0/8`
        
    - `172.16.0.0` — `172.31.255.255`
        
    - `192.168.0.0/16`
        
- **Every `Received:` line = one hop.** Count them to find number of mail-server hops.
    
- `Authentication-Results` often repeats the SMTP sender IP used in SPF checks — use that to corroborate.
    

---

## Example header interpretation (how to read)

Given:

`Received: from sc500.whpservers.com (204.93.183.11)   by DM6NAM10FT030.mail.protection.outlook.com (10.13.152.224) ... Received: from DM6NAM10FT030.eop-nam10.prod.protection.outlook.com (2603:...) ... ...`

- Read from bottom up. The bottom `Received` shows `sc500.whpservers.com (204.93.183.11)` → **public IPv4** that submitted mail to Microsoft → use **204.93.183.11** as originating IP.
    
- The `10.13.152.224` is private/internal and not the public origin.
    

---

## Quick CLI commands (paste in VM terminal)

Show any `X-Originating-IP`:

`grep -i '^X-Originating-IP:' Email1.eml || true`

Show all `Received:` lines (with context):

`grep -n -i '^Received:' Email1.eml -A2`

List all IPv4s in file (unique):

`grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' Email1.eml | sort -u`

Get the last (bottom-most) IPv4 (public heuristic):

`grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' Email1.eml \   | grep -v -E '^(10\.|192\.168\.|172\.(1[6-9]|2[0-9]|3[0-1])\.)' \   | tail -n1`

Count `Received:` headers (hop count):

`grep -c -i '^Received:' Email1.eml`

Small Python helper (all IPs + last IP):

`python3 - <<'PY' import re with open('Email1.eml','r',errors='ignore') as f: s=f.read() ips=re.findall(r'([0-9]{1,3}(?:\.[0-9]{1,3}){3})', s) print("Unique IPs:", sorted(set(ips))) if ips: print("Last IP in file:", ips[-1]) PY`

Defang IPv4 / ip:port:

`# IPv4 echo "204.93.183.11" | sed 's/\./[.]/g' # IPv4:PORT echo "212.192.246.30:5555" | sed -e 's/\./[.]/g' -e 's/:/[:]/g'`

---

## How to use Thunderbird (GUI quick steps)

1. File → Open → Saved Message… → select `Email1.eml`.
    
2. View → Headers → All (shows full raw headers).
    
3. Scroll to `Received:` block. Read bottom → up.
    
4. Hover links (do not click) to reveal true URL destinations.
    
5. Check Attachments pane for filenames.
    
6. Use `Resolve` / tagging if using PhishTool (if uploaded).
    

---

## PhishTool in a VM (options if Firefox in VM is offline)

- Fix VM network (VirtualBox → Settings → Network → Adapter 1 → NAT and Cable connected). Restart NetworkManager inside VM.
    
- If VM remains offline: use **VirtualBox Shared Folder** to copy `Email1.eml` to host and upload to PhishTool from host browser.
    
- If PhishTool geo-blocked: use other tools — local parsing + VirusTotal for attachment hashes.
    

Shared folder quick flow:

- Host: create `~/thm-share`. VirtualBox Settings → Shared Folders → add `thm-share`, Auto-mount on.
    
- VM: `cp ~/Desktop/Emails/Email1.eml /media/sf_thm-share/` (path may vary). Upload from host.
    

---

## What to submit to TryHackMe (examples)

- **Originating IP (plain):**
    
    `204.93.183.11`
    
- **Defanged (report):**
    
    `204[.]93[.]183[.]11`
    
- **Hop count (if asked):**
    
    `4`
    
- **Short explanation to paste for grading:**
    
    > “I read the raw headers and counted the `Received:` chain (4 hops). I used the bottom-most `Received:` entry and ignored RFC1918 addresses; `Authentication-Results` shows `sender IP is 204.93.183.11`, so I used `204.93.183.11` as the originating IP.”
    

---

## Notes / gotchas

- Attackers can forge or remove headers; header analysis is best-effort.
    
- Presence of only IPv6 addresses: questions that expect IPv4 may require scanning for IPv4 in other Received headers or using `Authentication-Results`.
    
- Internal/private IPs in Received lines are normal (infrastructure hops); don’t treat them as public origin.
    
- `Authentication-Results` is useful for SPF/DKIM/DMARC status and often repeats the SMTP sender IP used for SPF checks.

`#email-analysis #phishing #headers #forensics #tryhackme #phishtool #thunderbird`


Cisco Talos Intelligence

IT and Cybersecurity companies collect massive amounts of information that could be used for threat analysis and intelligence. Being one of those companies, Cisco assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. The solution is accessible as [Talos Intelligence](https://talosintelligence.com/).

Cisco Talos encompasses six key teams:

- **Threat Intelligence & Interdiction:** Quick correlation and tracking of threats provide a means to turn simple IOCs into context-rich intel.
- **Detection Research:** Vulnerability and malware analysis is performed to create rules and content for threat detection.
- **Engineering & Development:** Provides the maintenance support for the inspection engines and keeps them up-to-date to identify and triage emerging threats.
- **Vulnerability Research & Discovery:** Working with service and software vendors to develop repeatable means of identifying and reporting security vulnerabilities.
- **Communities:** Maintains the image of the team and the open-source solutions.
- **Global Outreach:** Disseminates intelligence to customers and the security community through publications.

More information about Cisco Talos can be found on their [White Paper](https://www.talosintelligence.com/docs/Talos_WhitePaper.pdf)

## Talos Dashboard

Accessing the open-source solution, we are first presented with a reputation lookup dashboard with a world map. This map shows an overview of email traffic with indicators of whether the emails are legitimate, spam or malware across numerous countries. Clicking on any marker, we see more information associated with IP and hostname addresses, volume on the day and the type.

![Talos Dashboard](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/e8ad635a9e449c698e081895bbb13ab1.png)  

At the top, we have several tabs that provide different types of intelligence resources. The primary tabs that an analyst would interact with are:  

- **Vulnerability Information:** Disclosed and zero-day vulnerability reports marked with CVE numbers and CVSS scores. Details of the vulnerabilities reported are provided when you select a specific report, including the timeline taken to get the report published. Microsoft vulnerability advisories are also provided, with the applicable snort rules that can be used.

![Talos Vulnerability Information Navigation](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/c761ada971950f5c2b676263d6e328a8.gif)

- **Reputation Center:** Provides access to searchable threat data related to IPs and files using their SHA256 hashes. Analysts would rely on these options to conduct their investigations. Additional email and spam data can be found under the **Email & Spam Data tab**.

![Talos Reputation Center](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/e14c377b524b9eb51b0a8ed8f1ee8356.gif)

  

![Talos Reputation Center](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/844f12e63a5a255b85df2ad6d261facb.gif)

## Task

Use the information gathered from inspecting the **Email1.eml** file from Task 5 to answer the following questions using Cisco Talos Intelligence. Please note that the VM launched in Task 5 would not have access to the Internet.

**The TryHackMe lab was written using an older Cisco Talos dataset** — back when the IP **204.93.183.11** had its reverse DNS (PTR) set to **scnet.net**. Since then, the live Talos data has changed to show `whpservers.com`, but **the grading system is still expecting the historical value `scnet.net`**.

---

### 🧠 Wrap this up in your notes:

- IP **204.93.183.11** currently resolves to `sc500.whpservers.com` and the domain `whpservers.com` in Talos.
    
- **Historically**, it resolved to **scnet.net**, which is what TryHackMe’s question expects.
    
- This illustrates that:
    
    - DNS and PTR records can change over time.
        
    - Threat-intel sources (like Talos, VirusTotal, AbuseIPDB, etc.) may show different results depending on when data was indexed.
        
    - When following a lab or certification exercise, **always use the value the exercise expects**, even if live data has shifted.
        

---

`204.93.183.11 → historical domain: scnet.net  (expected TryHackMe answer) Current Talos domain: whpservers.com Lesson: DNS and reputation data evolve; lab answers rely on snapshots in time.`

Email investigation summary (plain text)

1. What I looked at
    

- I examined three suspicious email files saved on a virtual machine: **Email1.eml**, **Email2.eml**, and **Email3.eml**.
    

2. Big findings — quick list (the short version)
    

- **Email1** — The message came from an external server with **IP address:** `204.93.183.11` (I write it defanged as `204[.]93[.]183[.]11` so it’s not clickable). That IP has a hostname `sc500.whpservers.com` and is linked to the domain `whpservers.com`. Historically it was also associated with `scnet.net`. The company name (network owner) tied to that IP is **Complete Web Reviews**.
    
- **Email2** — The email was sent to **chris.lyons@supercarcenterdetroit.com**. The attached file was checked on VirusTotal (an online scanner) and it had an antivirus detection alias that starts with the letter **H** (I didn’t reveal the alias text here).
    
- **Email3** — I extracted the attachment and checked it on VirusTotal. The malware family identified is **Dridex**.
    

3. What those things mean (simple explanations)
    

- **IP address / hostname / domain:** This is like a return address for a computer on the internet. It helps us see where the email came from. I made the IP safe to paste by replacing dots (`.`) with `[.]`.
    
- **Network owner / customer name:** This is the organization that registered the IP block. For the main suspicious IP we saw, the owner is **Complete Web Reviews** (this is the registration/WHOIS owner, not necessarily the person who sent the email).
    
- **VirusTotal detection / malware family:** VirusTotal aggregates antivirus results. For Email3’s attachment, several engines identified it as **Dridex**, which is a known banking malware. For Email2 the attachment had a detection alias beginning with **H** in VirusTotal.
    
- **Historical vs current data:** Some online records change over time. The lab expected an older name (`scnet.net`), but the live lookup now shows `whpservers.com`. I recorded both so we have context.
    

4. What I actually did (short steps, in plain words)
    

- Opened each `.eml` file to read the raw message and headers (using an email program).
    
- From the headers I found and confirmed the originating IP for Email1. I ignored internal/private addresses and picked the public one.
    
- Saved attachments from the emails to a safe folder.
    
- Calculated the file hash (a digital fingerprint) and used that to search VirusTotal so I didn’t have to upload potentially malicious files.
    
- Read VirusTotal’s report to find what antivirus engines call the file (the detection alias) and the likely malware family.
    

5. Safety notes (what to tell others)
    

- Don’t open suspicious email attachments or click links.
    
- If you get an odd email from someone you trust, check with them another way (text / call) before opening attachments.
    
- Save suspicious emails as files and don’t forward the file itself without warning — give coworkers context.
    

6. Short, shareable report you can forward (copy/paste)
I analyzed three suspicious emails:

- Email1.eml
  - Originating IP: 204[.]93[.]183[.]11
  - Hostname/domain seen: sc500.whpservers.com / whpservers.com
  - Historical domain seen in lab: scnet.net
  - Network owner (WHOIS): Complete Web Reviews

- Email2.eml
  - Recipient: chris.lyons@supercarcenterdetroit.com
  - Attachment scanned on VirusTotal: detection alias begins with "H" (flagged by AV engines)

- Email3.eml
  - Extracted attachment scanned on VirusTotal: identified as malware family DRIDEX

Notes:
- I inspected email headers to find the source IP and saved attachments safely to compute file hashes.
- I used VirusTotal (by hash) to check the attachments so I didn’t have to upload suspicious files from the VM.
- Recommendation: Do not open these attachments or click links. Block or quarantine the files and report to your security team.

---

## Related Notes
- [[Phishing]]
- [[Phishing Analysis Tools]]
- [[Intro to Cyber Threat Intel]]
