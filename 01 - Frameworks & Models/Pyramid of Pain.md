Hash Values (Trivial)
As per Microsoft, the hash value is a numeric value of a fixed length that uniquely identifies data
- a hash value is the result of a hashing algorithm
- MD5 (Message Digest, defined by RFC 1321) - was designed by Ron Rivest in 1992 an dis a widely used cryptographic hash function with a 128-bit hash value
- MD5 hashes are NOT considered cryptographically secure, in 2011, the IETF published RFC 6151, "Updated Security Considerations for the MD5 Message-Digest and the HMAC-MD5 Algorithms." which mentioned a number of attacks against MD5 hashes, included the hash collision!
- SHA-1, secure hash algorithm 1, defined by RFC 3174, was invented by United States National Security Agency in 1995.
- when data is fed to SHA-1 hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number
- NIST deprecated the use of SHA-1 in 2011 and banned its used for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks
- Instead, NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3 families
- The SHA-2 (Secure Hash Algorithm 2) - SHA-2 Hashing Algorithm was designed by The National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1
- SHA-2 has many variants and arguable the most common is SHA-256 
- The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number

- a hash is not considered to be cryptographically secure if two files have the same hash value or digest
- security professionals usually use the hash values to gain insight into a specific malware sample, a malicious or a suspicious file, and as a way to uniquely identify and reference the malicious artifact
- various online tools can be used to do hash lookups like VirusTotal and Metadefender Cloud - OPSWAT


![[OPSWAT 1.png]]Below the hash in the screenshot above, you can see the filename. In this case, it is "m_croetian.wnry"


![[VirusTotal.png]]


- as an attacker, modifying a file by even a single bit is trivial, which would produce a different hash value
- with so many variation and instances of known malware or ransomware, threat hunting using file hashes as the IOC (Indicators of Compromise) can become difficult

![[echo Hash.png]]



IP Address
- an IP address is used to identify any device connected to a network
- tehse devies range from desktops, to servers and even CCTV cameras
- we rely on IP addresses to send and recieve the infromation over the network
- in the Pyramid of Pain, IP addresses are indicated with t eh color green
- from a defense standpoint, knowlege of the IP addresses an adversary uses can be valuable
- a common defense tactic is to block, drop,  or deny inbound requests from IP addresses on your paramerter or external firewall
- this tactic is often not bulletproof as its trivial for an experienced adversarty to recover simply by using a new public IP address
- one of the ways an adversary can make it challenging to successfyuly carry out IP blocking is by using Fast Flux
- according to Akamai, Fast Flux is a DNS technique used byh botnets to hide phishing, web proxying, malware delivery, adn malaware ocmunication actgivities behind compromised hosts acting as proxies
- the purpos of using hte Fast Flux network is to make the communication between malware and its command and control server (C&C) challengin to be discovered by security professionals
- the primary concept of a Fast Flux network is having multiple IP addressess associated with a domain name, which is constanlty changing
- Palo Alto created a great fictional scenario to explain Fast Flux "Fast Flux 101: Hwo Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and LAw Enforcement TAkedowns"
 ![[Malicious IP.png]]

Domain Names
- can be thought as simply mapping an IP address to a string of text
- a domain name can contain a domain and a top-level domain (e.g. evilcorp.com) or a sub-domain followed by a domain and top-level domain (e.g. tryhackme.evilcorp.com)
- can be a little more of a pain for the attacker to change as they would most likely need to purchase the domain, register it and modify DNS records
- unfortunately for defenders, many DNS providers have loose standards and provide APIs to make it even easier for the attacker to change the domain

![[domain set.png]]


![[adidas mal domain 1.png]]

Can you spot anything malicious in the above screenshot? Now, compare it tot he legiitamate website below:

![[adidas good domain.png]]
This is one of the examples of a Punycode attack used by the attackers to redirect users toa malicious domain that seems legitamate at first glance

- What is Punycode? as per Jamf, "Puny code is a way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding"

What you saw in the URL above is adidas.de which has the Punycode of http://xn--addas-o4a.de/

- Internet Explorer, Google Chrome, Microsoft Edge, and Apple Safari aere now pretty good at translating the obfuscated characters into the full Punycode domain name
- to detect malicious domains, proxy logs, or web server logs can be used

Attackers usually hide the malicious domains under URL shortner. A URL shortner isa  tool that creates a short and unique URL that will redirect to the specific webswite specified durign the intial step of setting up the URL shortner link. the attackersx normally use the following URL-shortnenig seeviecs to generate malicious links:
- bit.ly
- goo.gl
- ow.ly
- s.id
- smarturl.it
- tiny.pl
- tinyurl.com
- x.co
you can see the actual website the shortened link is redirefting you to appendiung "+" to it 
- type the shortned URL in teh address bar of the web browser and add the above characters to see the redirected URL


![[shortenedurl 1.png]]

Viewing Connections in Any.run
- Because Any.run is a sandboxing service that executes the sample, we can review any connections such as HTTP requests, DNS requests or process communicating with an IP address
-  to do so, we can look at the "networking" tab located just below the snapshot of the machine

HTTP Requests: 
- this tab shows the recorded HTTP requests since the detonation of the sample
- this can be useful to see what resources are being retrieved froma  webserver, such as a dropper or a callback

![[http requests.png]]

Connections
- this tab shows any communications made since the detonation of the sample
- this can be useful to see if a process communicates with another host
- for exfample this could be C2 traffic, upploading/downloading files over FTP, etc

![[connections.png]]

DNS Requests:
- this tab shows the DNS requets made since the detonation of the sample
- malware often makes DNS requests to check for internet connectivity (i.e. if it can't reach the internet/call home, then its probably being sandboxed or is useless)

![[dnsrequests.png]]

Host Artifacts
- on this level, the attacker will feel a little more annoyed and frustated if you can detect the attack
- - the attacker would need to circle back at this detectioin level and change his attack t oolse and methodologies
- this is very time-consuming for the attacker, and probably, he will need to spend more resources on his adversary tools
- host artifacts are the t races or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything exclusive to the current threat

Suspicious process execution from Word:

![[suspicious process execution.png]]

Suspicious events followed by openign a malicious application:

![[suspicous events.png]]

The files modified/dropped by the malicious actor:

![[modified malicious actor.png]]

Network Artifacts
- network artifacts also belong to the yelow zone in the Pyramid of Pain
- this means if you can detect and respond to the threat, the attacker would need mroe tiem to go back and change his tactics or modify the tools, which gives you mor time to respond and detect the upcoming threats or remediate the existing ones
- can ber a user-agent string, C2 information, or URI patterns followed by the HTTP POST requests
- an attacker might use a User-Agent string that hasn't been observed in your environment before or seems out of the ordinary
- User-Agent is defined by RFC2616 as the request-header field that contains the information about the user agent originating the request
- netwsork artifacts can be detected in Wiresharks PCAPs (file that contains the packet data of a network) by using a network protocol analyzer such as TShark or exploring IDS (Intrusion Detection System) loggin from a source such as Snort

HTTP POST rquests containing suspicious strings:
![[Suspicious host requests.png]]

Let's use TShark to filter out the User-Agent strings by using the following command: `tshark --Y http.request -T fields -e http.host -e http.user_agent -r analysis_file.pcap`

![[tsharkfilter.png]]
These are the most common User-Agent strings found for the [Emotet Downloader Trojan](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/emotet-downloader-trojan-returns-in-force/)

- If you can detect the custom User-Agent strings that the attacker is using, you might be able to block them, creating more obstacles and making their attempt to compromise the network more annoying.

Tools
- At this stage, we have levelled﻿ up our detection capabilities against the artifacts. The attacker would most likely give up trying to break into your network or go back and try to create a new tool that serves the same purpose. It will be a game over for the attackers as they would need to invest some money into building a new tool (if they are capable of doing so), find the tool that has the same potential, or even gets some training to learn how to be proficient in a certain tool.
- attackerts would use the utilities to create malicious macro documents (maldocs) for spearphishing attempts, a backdoor taht can be used to establish C2 (Command and Control Infrastructure), any custome .EXE, and .DLL files, payloads, or password crackers

A trojan dropped the supsicious "Stealer.exe" in the Temp folder:

![[Trojan stealer exe.png]]

The execution of the suspicious binary:

![[suspicious binary.png]]

Antivirus signatures, detection rules, adn YARA rules can be great weapons for you to use against atttackers at this stage

- MalwareBazaar and Malshare are good resources to provide you wit haccess tot he samples, malicious feeds, and YARA results - these all can be very helpful when it comes to threatg hunting and incident response
- For detection rules, SOC Prime Threat Detection MArketplace is a great platform, where security professionals share their detection rules for different kinds of thretas including the latest CVE's that are bineg exploited itn the wild by adversaries
- Fuzzy hashing is also a strong weapon against the attacker's tools
- fuzzy ahshing helps you to perfom similarity analysis - match two files with minor differences basd on the fuzzy hash values
- one of the examples of fuzzy hashing is the useage of SSDeep; on the SSDeep official websitel, you can also find the complete explanation for fuzzy hashing
- ![[ssdeep.png]]

TTPS
- the final stage of the Pyramid of Pain
- TTPS stands for Tactics, Techniques & Procedures
- includes the whole MITRE ATT&CK Matrix, which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration
- - if you can detect and respond to the TTPs quickly, you leave th eadversaries almost no chance to fight back
- for example if you could detect a Pass-the-Hash attack usign Windows Event Log Monitoring and remediate it, you would be able to fidn the compromised host very quickly and stop the lateral movement inside your network. At this point, the attacker would have two options:
		1. Go back, do more resarch and training, reconfigure their custom tools
		2. Give up and find another target

---

## Related Notes
- [[Cyber Kill Chain]]
- [[Unified Kill Chain]]
- [[Diamond Model]]
- [[MITRE]]
- [[Intro to Cyber Threat Intel]]
- [[Summit]]
- [[YARA]]
- [[Hashing Basics]]
