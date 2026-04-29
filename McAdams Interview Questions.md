**McAdams Company**

Help Desk Technician — Interview Prep

Study Guide — February 2026

# **TROUBLESHOOTING**

**Q:** **Walk me through your troubleshooting process.**

_"I follow a structured approach: first I identify the problem by gathering info from the user — when did it start, what changed, who's affected. Then I establish a theory starting with the simplest cause. I test that theory, and if it checks out, I plan and implement the fix. After that I verify everything is working and have the user confirm. Then I document it all in a ticket so the next tech can reference it."_

**Q:** **A computer won't turn on. What do you do?**

▸ Check power cable is securely connected

▸ Test the outlet with another device

▸ Check the power supply

▸ Remove battery and try again (if laptop)

▸ Check if the monitor is the issue vs the actual PC

▸ Try different charger

▸ Escalate if hardware failure is suspected

_"First I'd check the basics — is the power cable plugged in, does the outlet work? I'd test with another device. If it's a laptop, I'd try removing the battery and powering on with just the adapter. I'd also make sure it's not just the monitor that's off. If none of that works, it's likely a hardware issue and I'd escalate."_

**Q:** **A user can't connect to the internet. What do you check?**

▸ Check Wi-Fi connection status

▸ Run ipconfig to verify IP address

▸ Ping the default gateway

▸ Check modem and router

▸ Flush DNS cache (ipconfig /flushdns)

▸ Check for outages in the area

_"I'd start by checking if they're connected to Wi-Fi or if the cable is plugged in. Then I'd run ipconfig to check their IP — if they have a 169 address, they're not getting one from DHCP. I'd ping the default gateway to see if they can reach the router. If that works but they still can't browse, I'd flush the DNS cache and check for any outages."_

**Q:** **A user can't reach a website — DNS troubleshooting.**

▸ ping google.com — does it resolve?

▸ ping 8.8.8.8 — if yes, it's a DNS problem; if no, it's a network problem

▸ Resolve-DnsName site.com -Server 8.8.8.8 — compare company DNS vs Google DNS

▸ Clear-DnsClientCache — flush stale cache

▸ ipconfig /all — verify DNS server settings

  
  

**Q:** **Common causes of a slow computer.**

▸ Low RAM

▸ HDD/SSD at capacity

▸ Malware

▸ Too many programs/processes running (check Task Manager)

▸ Outdated OS

_"I'd check Task Manager first to see if anything is eating up CPU or memory. Then I'd check disk space, run a malware scan, and make sure the OS is up to date. If it's a hardware limitation like low RAM, I'd document it and recommend an upgrade."_

**Q:** **How would you remove malware from a computer?**

▸ Disconnect from the network immediately

▸ Run antivirus and EDR scans

▸ Remove infected files

▸ Update the system

▸ Reset passwords if needed

▸ Document and escalate

_"First thing — disconnect it from the network so it doesn't spread. Then I'd run antivirus and EDR scans to identify and remove the threat. I'd update the system, reset any potentially compromised passwords, and document everything. If it's beyond what I can handle, I'd escalate to the security team."_

# **NETWORKING & KEY CONCEPTS**

**Q:** **What is Active Directory?**

_"Active Directory is Microsoft's centralized directory service for managing a network. It handles authentication — verifying who you are when you log in — and authorization — controlling what you can access. Admins use it to manage users, computers, permissions, and push out security policies through Group Policy, all from one place."_

**Q:** **What's the difference between HTTP and HTTPS?**

▸ HTTP is the standard protocol for web traffic

▸ HTTPS is the secured version, encrypted through SSL/TLS

▸ HTTPS is now the standard for most websites

_"HTTP is the standard web protocol, but it sends data in plain text. HTTPS adds encryption through SSL or TLS, so the data is protected in transit. Pretty much every site uses HTTPS now because it keeps user data secure."_

**Q:** **Explain the difference between a router and a switch.**

▸ A switch connects devices within a local network (LAN) and uses MAC addresses

▸ A router connects different networks together and uses IP addresses

▸ A router directs traffic between your LAN and the internet

_"A switch connects devices on the same local network — it uses MAC addresses to forward traffic between them. A router connects different networks together, like your office network to the internet, and it routes traffic using IP addresses."_

**Q:** **Why is MFA important?**

_"Multi-factor authentication adds an extra layer of security beyond just a password. Even if someone's password gets compromised, they still can't get in without that second factor. It significantly reduces the risk of unauthorized access."_

# **TICKETING & DOCUMENTATION**

**Q:** **Have you used ticketing systems?**

_"I haven't used one in a professional role yet, but I've trained on ServiceNow through labs and practice environments. I'm comfortable with the workflow — creating tickets, documenting steps, updating status, and closing them out."_

**Q:** **How do you prioritize tickets?**

_"I prioritize based on impact and urgency. If something is affecting multiple users or a critical system is down, that's top priority. Single user issues that block their work come next, and things like software requests or general questions I handle as I can. I also pay attention to context — if someone's on a tight project deadline, that factors in. And even if I can't get to a ticket right away, I make sure to communicate with the user so they know I'm on it."_

**Q:** **What do you document in a ticket?**

_"Every ticket gets the key details — who reported it, a clear description of the issue, when it started, what steps I took to troubleshoot, and the final resolution. I keep it clear enough that if another tech picks it up, they can understand exactly what happened without starting over."_

**Q:** **Why would you escalate to Tier 2?**

▸ Issue is outside my scope or expertise

▸ Requires admin privileges I don't have

▸ Hardware needs to be replaced

▸ Issue has been resolved but keeps recurring

_"I'd escalate if the issue is outside my scope, requires admin access I don't have, involves hardware replacement, or if it's a recurring problem that keeps coming back after I fix it. I'd always make sure the ticket is fully documented before handing it off."_

**Q:** **How do you ensure full resolution?**

_"I confirm with the user that everything is working — have them test it themselves. I check that my fix didn't break anything else. I ask if they need anything else from me. Then I document the findings and the fix in the ticket."_

# **SECURITY**

**Q:** **How would you protect sensitive information?**

_"I follow the principle of least privilege — users only get access to what they need. I verify identity before resetting passwords or sharing account info. I never send credentials over email or unsecured channels. And I stay aware of social engineering tactics — if something feels off about a request, I verify through a separate channel."_

**Q:** **A user's computer may have been exposed to phishing. What do you do?**

▸ Advise them not to click any links or open attachments

▸ Report it to the security team immediately

▸ Block the sender

▸ Scan the system

_"I'd tell them not to click anything else and report it to the security team right away. I'd block the sender, scan the system for any threats, and document everything. If they already clicked a link, I'd treat it as a potential compromise and escalate."_

**Q:** **What is the process after a device is lost or stolen?**

_"First I'd report it to my supervisor and follow the incident response policy. Then I'd disable the account associated with that device to prevent unauthorized access. If we have remote wipe, I'd initiate that. I'd reset any passwords tied to that device, check for suspicious activity, and document everything."_

# **SOFT SKILLS & CUSTOMER SERVICE**

**Q:** **Tell me about a time you gave excellent customer service.**

_"At my_ _last job__, we use__d_ _a POS system called Toast. A vendor came in who had never used a tablet-based system before and was really struggling. I walked them through the entire process step by step — entering the tip amount, signing up for rewards, and how to text themselves a receipt. I stayed patient and made sure they were comfortable before moving on. They left confident using the system on their own."_

**Q:** **How do you stay patient with repetitive issues?**

_"I treat every ticket like it's the first time I'm seeing it, because for that user, it is their first time dealing with it. Each person deserves the same level of attention and urgency. I also document each instance thoroughly, because if the same issue keeps popping up, that data helps identify a root cause so we can fix it permanently."_

**Q:** **An angry user can't access their network or files and they're on a deadline.**

▸ Listen calmly and let them be heard

▸ Open a ticket, get user details and full description

▸ Check Active Directory — permissions and security groups

▸ Check network — cable, Wi-Fi, can they reach internet?

▸ Determine scope — just them or others affected?

▸ Resolve or escalate quickly given the time pressure

▸ Document time spent and resolution

_"First I'd listen and let them know I understand the urgency. Then I'd jump right in — open a ticket, check their permissions in Active Directory, make sure they're in the right security groups. I'd check their network connection and whether it's just them or a wider issue. If I can fix it, I fix it fast. If not, I escalate immediately and let them know what's happening every step of the way."_

  

# **QUICK REFERENCE — COMMANDS & TOOLS**

## **Windows Commands**

▸ ipconfig — View IP configuration

▸ ipconfig /flushdns — Clear DNS cache

▸ ipconfig /all — Full network details including DNS servers

▸ ipconfig | findstr "IPv4" — Show only IP addresses

▸ ping [address] — Test connectivity

▸ nslookup [domain] — Query DNS

## **PowerShell Commands**

▸ Resolve-DnsName [domain] — PowerShell version of nslookup

▸ Resolve-DnsName site.com -Server 8.8.8.8 — Test against specific DNS

▸ Get-DnsClientCache — View cached DNS records

▸ Clear-DnsClientCache — Flush DNS cache

## **Key Concepts to Remember**

▸ Principle of Least Privilege — Only give access that's needed

▸ MFA — Multi-factor authentication, extra security layer

▸ GPO — Group Policy Objects, push settings to domain machines

▸ OU — Organizational Units, folders in AD for organizing objects

▸ DC — Domain Controller, server running Active Directory

▸ DHCP — Auto-assigns IP addresses

▸ DNS — Translates domain names to IP addresses

▸ 169.x.x.x address — Means DHCP isn't assigning an IP