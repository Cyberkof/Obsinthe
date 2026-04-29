Troubleshooting Issues
- Using Task Manager to identify processes consuming high CPU, memory, or disk
- Running sfc /scannow to repair corrupted system files
- Using DISM (Deployment Image Servicing and Management) to repair the Windows image when sfc can't fix it
- Event Viewer - checking logs to diagnose errors, crashes, and application failures
- Safe Mode - booting into it to troubleshoot driver issues or malware
- Device Manager - identifying driver problems (yellow triangle icons), updating or rolling back drivers
- Disk Cleanup and clearing temp files to free up space
- Troubleshooting BSOD by noting the stop code and researching it
- MSconfig and Startup tab in task manager to disable problematic startup programs
- network troubleshooting with ipconfig, ping, tracert, nslookup

Managing Updates
- Using Windows Update (Settings > Update & Security) to check for and install updates
- Understanding update types:  feature updates (major, twice a year), quality updates (monthly patches), and security updates
- Knowing how to pause updates or schedule restarts so you're not disrupting users mid-workday
- In enterprise, updates are typically managed through WSUS (Windows Server Update Services) or SCCM/Intune so IT controls what gets pushed and when
- Troubleshooting failed updates using Windows Update Troubleshooter or clearing the SoftwareDistrubution folder 

Configuring Security Settings
- Windows Defender/Microsoft Defender - managing real-time protection, running scans, checking threat history
- Windows Firewall - enabling/disabling, creating inbound/outbound rules
- BitLocker - full disk encryption, knowing how to enable it and recover with a recovery key
- UAC (User Account Control) - understanding permission levels and prompts
- Configuring password policies and account lockout policies through Local Security Policy or Group Policy
- Enabling Secure Boot and TPM in BIOS/UEFI

Windows Server Knowledge
- Active Directory (AD) - creating user accounts, resetting passwords, managing OUs and security groups
- Group Policy (GPOs) - pushing settings like password requirements, mapped drives, desktop restrictions across the domain
- DNS and DHCP server roles - understanding how devices get IP addresses and resolve names on the network
- File shares and NTFS permissions - setting up shared folders with proper access controls
- Remote Desktop Services - enabling and managing remote access
- Understanding domain vs workgroup environments


Ground to Cover

DISM (Deployment Image Servicing and Management)

DISM is a command lien tool that repairs the Windows system image- think of it as a deeper fix than sfc /scannow. When sfc can't repair corrupted files because the source image itself is damaged, DISM fixes that source image so sfc can then do its job

How to use it:
1. Open command prompt as Admin
2. Run DISM /Online /Cleanup-Image /CheckHealth - quick check for corruption
3. Run DISM /Online /Cleanup-Image /ScanHealth - deeper scan
4. Run DISM /Online /Cleanup-Image /RestoreHealth - actually repairs the image by downloading the clean files from Windows Update

Typical workflow: run DISM first, then run sfc /scannow aft er


WSUS (Windows Server Update Services)
- a free Microsoft server role that lets ITS admins centrally amngae and approve Windows updates before they get pushed to workstations
- instead of every computer pulling updates diresct ly from Microsoft, they pull from the WSUS seerver
- This gives IT control over which updates get deployed and when, so a bad update doesnt break 500 machines at once

SCCM (System Center Configuration Manager) / INtune

These are more advanced tools from Microsoft

SCCM (now called Microsoft Endpoint Configuration Manager or MECM)
- an on-prem tool for managing large fleets of devices
- deplyoing software, pushing updates, imaging machines, ruinning copmpliance reports
- heavy duty enterprise

Intune 
- Microsoft's cloud-based device manmagament solution (part of Microsoft Entra/Azure)
- does s imilairt things to SCCM but from the cloud
- makes it ideal fro managing remote workers and BYOD devices

In moderne environments, many ocmpanies use both together
- SCCM for on-prem devices and intuen fro renmote/cloud-0managed devices
- called co-managment


Windows Update Troubleshooter
- a built-in automated tool that diagnoses and fixes common Windows Update problems like stuck downloads, failed installationsl, or corruptd update components
- found in Settings > System > Troubleshoot > Other Troubleshooters > Windows Update
- resets update components and clears caches automatically

SoftwareDistribution Folder
- Located at C:\Windows\SoftwareDistribution
- this is where Windows temporarily stores downloaded update fails before installing them
- when updates get stuck or corrupted, manually clearing this folder forces Windows to re-download fresh copies
How to clear it:
1. Open Command Prompt as Admin
2. net stop wuauserv - stops the Windows update service
3. net stop bits - stops the Background Intelligent Transfer Service
4. Delete the contents inside C:\Windows\SoftwareDistribution\Download
5. net start wuauserv - restart Windows Update
6. 6. net start bits - restart BITS
7. Check for updates again


BitLocker
- Microsoft's built-in full disk encryption tool
- encrypts the entire drive so if someone steals the laptop or pulls the hard drive out they cant read the data without the encryption key

How it works:
- Uses TPM(Trusted Platform Module) to store the encryption key securely
- When the machine boots normally, TPM releases the key automatically and you don't notice anything
- If someone tampers with the hardware or moves the drive to another machine, TPM won't release the key and they'll need the recovery key - a 48 digit number generated then BitLocker was enabled

How to enable it:
- Go to Control Panel > BitLocker Drive Encryption > Turn on BitLocker
- Or right-click a drive in File Explorer > Turn on BitLocker
- You'll be prompted to save the recovery key (to a file, USB, Microsoft account, or print it)
In enterprise, recovery keys are stored in Active Directory so help desk can look them up when a user gets locked out. This is very common help desk task- user calls saying their laptop is asking for a BitLocker recovery key, you look it up in AD and give it to them

BitLocker requires Windows Pro, Enterprise, or Education - its not available on Windows Home


UAC (User Account Control)
- a security feature that prevents unauthorized changes to the system
- its the prompt that pops up asking "Do you want to allow this app to make changes to your device?" with a Yes/No option

Why it matters:
- even if your logged in as an admin, UAC makes you explicitly confirm before elevated actions happen
- this prevents malware from silently making system changes
- standard users get a prompt asking for admin credentials instead of just Yes/No

How to configure it:
- Search "UAC" in the Start menu > "Change User Account Control settings"
- Slider rangers from Always Notify (most secure) to Never Notify (least secure, not recommended)
- default setting is the second level from the top

In enterprise, UAC behavior is typically controlled through Group Policy so users cant lower it themselves


Secure Boot and TPM in BIOS/UEFI 
- BIOS (Basic Input/Output System)/UEFI (Unified Extensible Firmware Interface) is the firmware that runs before your operating system loads
- UEFI is the modern replacement for the older BIOS, with a graphical interface and more features
- Secure Boort is a UEFI feature that only allows trusted, digitally signed software to run during the boot process
- this prevents rootkits and bootkits (malware that loads before the OS) from executing 
- if something unauthorized tries to load during boot, Secure Boot blocks it
- TPM (Trusted Platform Module) is a security chip on the motherboard (or firmware-based in newer systems) that has many features
	- stores encryption keys securely (used by BitLocker)
	- verifies system integrity during boot
	- Supports features like Windows Hello and credential storage
	- TPM 2.0 is require for Windows 11

To access these settings, you restart the computer and press the BIOS key during boot (usually F2, F10, F12, Del or Esc depending on manufacturer). Then look under the Security tab for Secure Boot and TPM settings.

File Shares and NTFS Permissions
- Files shares are folders on a sever or computer that are made accessible to other users over the network
- In a business environment you'd have shared drives like \\server\Marketing or \\server\Engineering where teams store their files

There are two layers of permissions:

share permissions - control who can access the folder over the network. These are simpler: 
- read, change, or full control

NTFS permission - control access at the file system level. These are more granular:
- Full Control - do everything including change permissions
- Modify - read, write, edit, delete
- Read & Execute - open and run files
- Read - view only
- Write - create new files and folders

The important rule: when both share and NTFS permission apply, the most restrictive permission wins.  So if share gives Full Control but NTFS gives Read, the user only gets Read access.

In enterprise, permissions are usually assigned to Active Directro7y security groups rather than individual users. So you'd create a group called "Marketing-Team," put the right users in it, and assign t hat group permissions on the Marketing shared folder. When someone joins or leaves the team, you just add or remove them from the group. 

**Scenario 1: "A user is locked out by BitLocker — what do you do?"**

"First, I'd verify the user's identity to make sure I'm not giving a recovery key to the wrong person. Then I'd look up their BitLocker recovery key in Active Directory — in AD Users and Computers, you can find the recovery key stored under the computer object's properties. I'd read them the 48-digit recovery key so they can enter it and get back into their machine. Once they're back in, I'd want to understand why it triggered in the first place. Common causes include a BIOS/UEFI update, a hardware change like swapping RAM, or a TPM issue. If it keeps happening repeatedly, that could indicate a hardware problem with the TPM chip and the machine might need to be looked at further. I'd document the incident in our ticketing system."

---

**Scenario 2: "A user can't access a shared drive — how do you troubleshoot?"**

"I'd start with the basics and work my way up:

First, I'd check network connectivity — can they access other network resources? Can they ping the file server? If not, it's a network issue and I'd troubleshoot that first with ipconfig, checking their IP address, making sure they're on the right network.

If the network is fine, I'd try accessing the share myself using the UNC path like `\\servername\sharename` to see if the share itself is up and working.

If the share works for me but not for them, it's likely a permissions issue. I'd check Active Directory to see what security groups the user is in and compare that to the NTFS and share permissions on the folder. Maybe they were recently moved to a new department and weren't added to the right security group yet.

I'd also check if their account is locked out or if their password expired, since that can sometimes cause access failures to network resources.

If they were recently added to a group, I'd have them log off and log back on because group membership changes don't take effect until the next login — the user gets a new Kerberos token at login that includes their updated group memberships.

Once resolved, I'd document the issue, the cause, and the fix in the ticket."