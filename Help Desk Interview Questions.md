How do you list directories and delte them in cmd?
- dir - lists files and folders in currernt directory
- dir /ad lists only directories
- dir /s - lists directories and subdirectories recursively

Delete directories
- rmdir FolderName or rd FolderName - removes an empty directory
- rmdir /s FolderName - removes a directory and all its contents (prompts for confirmation)
- rmdir /s /q FolderName - same but quiet mode, No confirmation prompt

**In an interview, you'd want to mention:**

- Always verify what's in a directory before deleting (`dir FolderName`) — especially in a production environment
- `/s` is recursive and `/q` skips confirmation, so use with caution
- If a file inside is in use or locked, the delete will fail
- For PowerShell (which they may follow up with): `Get-ChildItem` to list and `Remove-Item -Recurse` to delete

What is DHCP?
- DHCP is Dynamic Host Configuration Protocl which automatically assigns IP addeesses and network ocnfigurartion to devices when they connect to a newtwork
-  without DHCP youd have to manually configure every single device
- DORA process
	- 1. Discover - Cliente broadcasts "Hey, I need an IP address"
	- 2. Offer - DHCP server responds "Heres one you can use
	- 3 Request - Client says Ill take that one
	- 4. Acknowledge - Server confirms its yours"

What does DCHO assign?
- Ip addrerss, subnet mask, defautl gateway, DNS server addresses, lease duration
- 
**Key terms to know:**

- **DHCP Lease** — the IP isn't permanent, it's "rented" for a set time and renewed periodically
- **DHCP Scope** — the range of IP addresses the server can hand out
- **DHCP Reservation** — ties a specific IP to a device's MAC address (useful for printers, servers, etc. that need a consistent IP without being fully static

What is Iconfig release and renew?
ipconfig /release -= tells your machien to give up its current ip addess. it droped the dhcp lease and youll ahve no IP

ipconfig /renew - tells yoru amchine to request a new IP from the DHCP serfver. Goes throguh the DORA prtocess agin to get a fresh lease

**When you'd use them at a help desk:**

- User can't access the network → try `ipconfig /release` then `ipconfig /renew` to get a fresh IP
- Network changes were made (new VLAN, new DHCP scope) and you need the client to pick up the new settings
- User has an IP conflict (two devices with the same IP)

**Common interview follow-up:** "What's the difference between `/renew` and `/flushdns`?"

- `/renew` fixes IP address issues
- `/flushdns` clears the local DNS cache, which fixes **name resolution** issues (e.g., user can ping an IP but not a website name)

A typical help desk troubleshooting flow would be:

`ipconfig /release` → `ipconfig /renew` → `ipconfig /flushdns` → test connectivity with `ping`

That sequence shows you have a methodical approach to network troubleshooting, which is exactly what they want to hear.

What would you look for when  moving a PC to a new location?
- learn if location is available and free
- check internet connection
- do a site survey
- pick a day and time and schedule

How do you use Active Directory?
- for password reset we go to server manager, open active directory, drop down in tools, search for domain controllers, go under users. right click on their name, click reset passwords, if account is unlocked hit properties and hit unlock profile unlock account

How do you map a network drive?
go into C explore, this pc, (my computer), right click and hit properties and map network drive

how do you connect a network printer and map it?
1. settings - devices -= rpinters & scanners
2. click add printer
3. selweecet the printer from the list -> add device or use add printer usinga (TCVP/IP address or hostname)
4. if it doesnt show up click the printer that i want isnt listedn and ehter the path manually

what is needed to configure a network printer?

How do you set up a brand new printer?
1. physical setup
- unbox it
- install toner/ink cartidges and paper
- plug in the power cable  nad turn it on
- connect it to he network with an ethernet cable to a switch/weall jack ( or configure wifi through the printersddisplay menu
1. itll grab a DHCP addres automatically on boot
2. print a config/netwrok page fro mthe printer menu to see what IP it got
3. go to your DHCP server and create a reservation fro that pritner's MAC address
4. or log into the printers web interface and set a static IP

An unkown virus bereaks out.  There is talk athat data files are being deleted by the thousands from computers and servers. What do you do and what do you do i n what order>?

1. Escalate conversations
2. Inform everyone
3. Disconnect all network switches
4. Shut down equipment
5. Isolate a computer to send a sample file
6. Apply update and patch (each computer individually)
7. Document and save resolution

How do you triage an incident?

Framework = Identify -> Assess -> Prioritize Respond -> Document

1. Identify whats happening, gather initial information from the alert, ticket, or user report. See what system is affected, or what are the sytsems, and when did it start
2. Assess the severetiy based on impact and urgency, how many users are affected, is it impacting business-critical systems, is there a secyurity threat inviolved
	1.  Most organizations yuse a priortiy scalel ike P1 through P4
	2. P1 similar to a fully system ouage or active secrutiy breach affecting the whole compalny'
	3. p4 might be a single user with a minor issue
3. Priotrize it agints it other open incidents. A P1 gets immediate attention and escalation, while lower priortiy items get queed accordingly
4. Resooind appropriately, resolve if within my scope or escalate tot he right team if its beyond my level
	1. communication is key


The power goes out. What do you do and in what order. What do you not do and why?
1. Shut down equipment
2. Contact the power company
3. Escalate teh conversation
4. Tell everyone to unplug equipment
5. Create a monitoring group
6. Bring all equipment when service is restored
7. Document incident and resolution

What are osme common solutiosn fora  user that cant log in?
- check for caps lock
- expired password
- suspended account
- reset passowrd

A Delete File needs to be restored. What do you do?
- check the recybe bin
- volume shadow copy restore
- standard restore

A users computer is slow what do you do?
- use the task amnager to check CPU usage
- remove temporary files from the windows folder
- check to sere if he hard drive is full
- check eth computer for virtuses or malware

the internet connection has been reported slow what do you do?
- determine hwo many people are affected
- check ip addrerssing and DNS

What are common fixes for printer problems?
- check to ensure the printer is powered on
- check for paper jame or ink outage
- add or replace teh printer driver

A user cannont access shared drive what do you do?
- remote into computer
- ping the server to check connection issues and remap the drive if necessary
- see if the server is down
- escalate to server team if out of your reach

there is suspecteed malware for a user what do you do?
- immediately remove the machine from the network
- determine the actual virus or malware
- next step may require on-site tech
- remove hard drive, air-gap computer by sandboxing
- scan hardrive for malware

Wireless keyboard or mouse not workikng what could you do to fix?
- replace batteries
- cross connection
- amke sure bluetwooth is working properly

What is the blue screen of death and how would you triage it?
- a system crash
- ask them what they were doing when it happened
- check to see ifts recurrign or one time thing
- note the stop code if they saw one on screen
- possible hardware failure
- a driver failure
- may require only a system reboot
- may need to disconnect unneccessary hardware
- may need to deploy a tech to repair or replace
- the dump files are stroed on C:\Windows\Minidump for mini dumps, or C:\Windows\Memory.dmp for full memory dumps

**How to analyze them:**

**WinDbg (Windows Debugger)** — this is the main tool:

1. Download it from Microsoft (part of the Windows SDK or standalone from the Microsoft Store)
2. Open WinDbg
3. Go to **File > Open Dump File** and navigate to the .dmp file in C:\Windows\Minidump
4. Once it loads, type `!analyze -v` in the command line — this is the magic command
5. It'll give you a detailed breakdown including the **stop code**, the **driver or module that caused the crash**, and a **stack trace**

**What to look for in the output:**

- **MODULE_NAME** — this tells you what driver or program caused the crash. If it says something like `nvlddmkm.sys` that's an Nvidia driver. `ntfs.sys` could be a disk issue.
- **BUGCHECK_STR** — the type of crash
- **DEFAULT_BUCKET_ID** — general category of the problem

**Common fixes based on what you find:**

- Bad driver → update or roll back that driver
- Memory related stop codes → run `mdsched.exe` (Windows Memory Diagnostic) to test the RAM
- Disk related → run `chkdsk /f /r`
- Overheating → check thermals and fans


**Layer 1 — Physical**

- Power cable unplugged or damaged
- Bad outlet or power strip
- PSU (power supply) dead
- Loose internal connections (RAM, GPU, CMOS battery)
- Bad power button
- Overheating — fans clogged or dead
- Damaged motherboard
- For laptops — dead battery, bad charging port
- Troubleshooting: check cables, swap power cord, reseat components, listen for fans, check link lights

**Layer 2 — Data Link**

- NIC failure (won't connect to network after booting)
- Bad display cable connection (HDMI, DisplayPort, VGA)
- Monitor not detecting signal
- Troubleshooting: swap cables, try different monitor, check NIC link lights

**Layer 3 — Network**

- Not really applicable to "won't start" but if the machine boots and can't get an IP address via DHCP that could look like "it's not working"
- Troubleshooting: `ipconfig /release` then `ipconfig /renew`

**Layer 4 — Transport**

- Ports blocked preventing network services from loading after boot
- Firewall misconfiguration making it seem like nothing works

**Layer 5 — Session**

- Can't authenticate to domain — user sees black screen after login
- Profile fails to load
- Troubleshooting: try logging in with a local account, check domain connectivity

**Layer 6 — Presentation**

- Display driver crash causing black screen or garbled graphics
- Resolution set to something the monitor can't display
- Troubleshooting: boot into Safe Mode (loads basic display driver), roll back driver

**Layer 7 — Application**

- Corrupted OS — boot loop, BSOD, stuck on Windows logo
- Bad Windows update
- Malware preventing startup
- Too many startup programs making it seem frozen
- Troubleshooting: Safe Mode, Startup Repair, `sfc /scannow`, `DISM`, check Event Viewer, reimage if necessary

What are common softare problems?
- vendor bug
- windows update issue
- corrupt software 