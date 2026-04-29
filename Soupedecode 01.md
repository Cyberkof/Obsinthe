
A full list of our TryHackMe walkthroughs and cheatsheets is [here](https://happycamper84.medium.com/thm-walkthrough-list-ad-stuff-95280f400bec).

**Background**

After a rather annoying experience taking [TryHackMe’s PT1 exam](https://happycamper84.medium.com/tryhackme-junior-penetration-tester-pt1-ad-exam-review-b9b5fa225f44), luckily for free, I wanted to do a room that has nothing to do with webapps. This room was perfect for it and included a few new tricks I will add to my AD cheatsheet such as enumerating domain accounts while only having access as the Guest user with no password.

The room also included old classics like Kerberoasting, poking around share drives looking for interesting info, password spraying, hash spraying, and PTH via smbclient, wmiexec, smbexec, evil-winrm, xfreerdp, etc. It’s always good to get reps in with those tools.

On an admin note, you may notice the IP used changing throughout the commands used in this walkthrough. This is due to restarting the target VM on TryHackMe. I didn’t use any reverse shells in this room, all IPs shown are the target VM.


---

## Related Notes
- [[Hacking With Powershell]]
- [[Linux Shells]]
