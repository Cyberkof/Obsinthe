


**If they ask "What are your salary expectations?"**

_"I'm flexible and really more focused on finding the right fit and opportunity to grow. I'd love to hear what the budgeted range is for this role."_


**If they push you for a number:**

_"Based on my experience and certifications, I'd be looking in the $48K to $55K range, but I'm open to discussing the full compensation package."_

Tell me about yourself:

_"I'm someone who's been hands-on with technology for over 20 years — from building and configuring my own systems, to photography production work, to now diving deep into cybersecurity and IT infrastructure. I completed a cybersecurity bootcamp, earned my CompTIA Security+, and I'm currently studying for CCNA.

_What I've been doing recently is building out a full home lab where I run three Domain Controllers on Windows Server 2022 with Active Directory, practice Group Policy, PowerShell automation, and user management. I also built a SOC environment with Splunk, Wazuh, and pfSense where I'm doing log analysis and incident detection. I'm also using Cyber-Atlanta's ticketing system lab to practice real help desk workflows._

_What excites me about this role at McAdams is the chance to work in a technical environment supporting your engineering teams which is something much needed. Im glad McAdams is Raleigh/North Carolina based so I can relate. I grew up in Apex and went to Panther Creek. I know your staff relies on tools like Civil 3D and AutoCAD to do their work, and I want to be the person who keeps them running smoothly. I'm a fast learner, I'm hungry, and I'm ready to prove myself."_

Troubleshoooting Process

- Identify the problem (ask questions, reproduce it)
- Establish a theory (what could cause this)
- Test the theory
- Establish a plan of action
- Implement the fix
- Verify it works
- Document everything

**2. ACTIVE DIRECTORY**

- What is AD? (Centralized directory service that manages users, computers, and resources on a network)
- Password resets — where do you do it? (Active Directory Users and Computers or ADUC, or PowerShell)
- Account lockouts — how do you check? (Check lockout status in ADUC, look at properties, unlock the account)
- What's an OU? (Organizational Unit — container to organize users/computers and apply GPOs)
- What's a GPO? (Group Policy Object — pushes settings and restrictions to users and computers)
- What's the difference between a security group and a distribution group? (Security controls access to resources, distribution is for email lists)

**3. NETWORKING BASICS**

- What's DHCP? (Automatically assigns IP addresses to devices)
- What's DNS? (Translates domain names to IP addresses — like a phone book for the internet)
- What's a subnet? (Divides a network into smaller sections)
- What's the difference between a switch and a router? (Switch connects devices on same network, router connects different networks)
- What's a VLAN? (Logically separates network traffic without separate physical hardware)
- Basic ports to know: 80 (HTTP), 443 (HTTPS), 3389 (RDP), 53 (DNS), 25 (SMTP)

**4. WINDOWS TROUBLESHOOTING**

- Computer is slow — what do you check? (Task Manager for CPU/RAM/disk usage, startup programs, check for updates, disk space, malware scan)
- Blue screen of death — what do you do? (Note the error code, check Event Viewer, update drivers, check RAM)
- Application won't open — steps? (Restart the app, restart the PC, check Task Manager for hung process, repair/reinstall the app, check Event Viewer)
- What's Event Viewer? (Windows tool that logs system events, errors, and warnings — this is your best friend for troubleshooting)
- What's Safe Mode? (Boots Windows with minimal drivers to isolate problems)

**5. MICROSOFT 365**

- User can't get email — what do you check? (Outlook profile, internet connection, credentials, license assigned in admin portal, mailbox status)
- OneDrive not syncing — steps? (Check sync status icon, restart OneDrive, check storage, re-sign in)
- How do you reset a password in M365? (Admin center → Users → Active Users → Reset password)

**6. TICKETING / PROCESS**

- What's a ticketing system? (Tracks and manages IT support requests)
- How do you prioritize tickets? (Severity and impact — a whole office down beats one person's printer not working)
- What do you do if you can't solve an issue? (Document what you tried, escalate to Tier 2 with detailed notes)

**7. HARDWARE**

- Laptop won't turn on — steps? (Check power adapter, try hard reset by holding power button 15 seconds, remove battery if possible, try different outlet)
- Monitor no display — what do you check? (Cable connections, try different cable, different port, connect to different monitor, check if laptop is detecting external display)
- Printer not printing — steps? (Check connection, print queue for stuck jobs, restart print spooler service, reinstall driver)

**8. SECURITY BASICS**

- What's MFA? (Multi-factor authentication — requires two or more forms of verification)
- What's phishing? (Social engineering attack using fake emails to steal credentials or deliver malware)
- User clicked a suspicious link — what do you do? (Disconnect from network, reset their password, scan for malware, report to security team, document the incident)
- What's the principle of least privilege? (Users only get the minimum access they need to do their job)

**9. AUTOCAD/AEC SPECIFIC (McAdams bonus points)**

- AutoCAD crashing — what do you check? (GPU drivers, hardware acceleration settings, run RECOVER on the file, check available RAM/disk space)
- License not working — steps? (Check Autodesk subscription status, restart FlexNet Licensing Service, clear license cache, reinstall Autodesk Licensing Service)
- File recovery — know that .bak and .sv$ are AutoCAD backup/autosave files

**The magic phrase for anything you don't know:**

_"I haven't encountered that specific issue before, but my approach would be to research it in the vendor's knowledge base, check for known issues, and if needed escalate it while documenting everything I've tried so far."_


ipconfig
ipconfig /flushdns

ping

tracert

nslookup
Resolve-DNSname
netstat -an
pathping

sfc /scannow
chkdsk
DISM /Online /Cleanup-Image /RestoreHealth

shut down

Get-Service 
Get-Process


- "What does a typical day look like for the help desk team here?"
- "What ticketing system do you use to track support requests?"
- "How many people would I be supporting across the offices?"
- "What's the most common issue your engineers run into that I'd be handling?"

**About the tools and environment (shows you did your research):**

- "I know your teams use Civil 3D and ArcGIS Pro — are there other AEC-specific applications I'd be supporting?"
- "How is the IT team structured? Would I be working alongside other technicians or is this a solo role for the Charlotte office?"
- "Are you using on-prem Active Directory, Azure AD, or a hybrid setup?"

**About growth (shows you're not just punching a clock):**

- "What does growth look like for someone in this role? Is there a path to move into systems administration or other areas of IT here?"
- "Are there opportunities for training or certifications that McAdams supports?"

**About culture and team (shows you care about fit):**

- "What do you enjoy most about working at McAdams?"
- "How does the IT team collaborate with the engineering and design teams?"

**Practical / next steps:**

- "What does the onboarding process look like for this role?"
- "What's the timeline for the next steps in the hiring process?"