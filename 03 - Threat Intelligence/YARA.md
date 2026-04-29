Introduction  

This room will expect you to understand basic Linux familiarity, such as installing software and commands for general navigation of the system. Moreso, this room isn't designed to test your knowledge or for point-scoring. It is here to encourage you to follow along and experiment with what you have learned here.  

  

As always, I hope you take a few things away from this room, namely, the wonder that Yara (_Yet Another Ridiculous Acronym_) is and its importance in infosec today. Yara was developed by Victor M. Alvarez ([@plusvic](https://twitter.com/plusvic)) and [@VirusTotal](https://twitter.com/virustotal). Check the GitHub repo [here](https://github.com/virustotal/yara).

All about Yara 

_"The pattern matching swiss knife for malware researchers (and everyone else)" ([Virustotal., 2020](https://virustotal.github.io/yara/))_

With such a fitting quote, Yara can identify information based on both binary and textual patterns, such as hexadecimal and strings contained within a file.

  

Rules are used to label these patterns. For example, Yara rules are frequently written to determine if a file is malicious or not, based upon the features - or patterns - it presents. Strings are a fundamental component of programming languages. Applications use strings to store data such as text.

  

For example, the code snippet below prints "Hello World" in Python. The text "Hello World" would be stored as a string.

```python
print("Hello World!")
```

  

We could write a Yara rule to search for "hello world" in every program on our operating system if we would like. 

  

Why does Malware use Strings?

Malware, just like our "Hello World" application, uses strings to store textual data. Here are a few examples of the data that various malware types store within strings:

  

|            |                                                                                                                 |                                                        |
| ---------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| **Type**   | **Data**                                                                                                        | **Description**                                        |
| Ransomware | [12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw](https://www.blockchain.com/btc/address/12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw) | Bitcoin Wallet for ransom payments                     |
| Botnet     | 12.34.56.7                                                                                                      | The IP address of the Command and Control (C&C) server |

Caveat: Malware Analysis  

Explaining the functionality of malware is vastly out of scope for this room due to the sheer size of the topic. I have covered strings in much more detail in "Task 12 - Strings" of my [MAL: Introductory room](https://tryhackme.com/room/malmalintroductory). In fact, I am creating a whole Learning Path for it. If you'd like to get a taster whilst learning the fundamentals, I'd recommend my room.

Deploy

In-Browser (No  VPN required)  

Deploy your own instance by pressing the green "Start Machine" button and scroll up to the top of the room and await the timer. The machine will start in a split-screen view. In case the VM is not visible, use the blue "Show Split View" button at the top-right of the page.

![The view of the deployed instance attached to this task.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/7c222bb437b106d862d93ce76117c9e8.png)  

Using SSH (TryHackMe VPN required).

You must be connected to the TryHackMe VPN if you wish to connect your deployed Instance from your own device.  If you are unfamiliar with this process, please visit the [TryHackMe OpenVPN](https://tryhackme.com/room/openvpn) room to get started. If you have any issues, please [read our support articles](https://help.tryhackme.com/).

IP Address: **MACHINE_IP**

Username: **cmnatic**

Password: **yararules!**

SSH Port: **22**

Your First Yara Rule

The proprietary language that Yara uses for rules is fairly trivial to pick up, but hard to master. This is because your rule is only as effective as your understanding of the patterns you want to search for.  
  
Using a Yara rule is simple. Every `yara` command requires two arguments to be valid, these are:  
**1)** The rule file we create  
**2)** Name of file, directory, or process ID to use the rule for.  
  
Every rule must have a name and condition. For example, if we wanted to use "myrule.yar" on directory "some directory", we would use the following command:  
`yara myrule.yar somedirectory`  
  
Note that **.yar** is the standard file extension for all Yara rules. We'll make one of the most basic rules you can make below.  
1. Make a file named "**somefile**" via `touch somefile`  
2. Create a new file and name it "**myfirstrule.yar**" like below:

Creating a file named somefile

```shell-session
cmnatic@thm:~$ touch somefile
```

Creating a file named myfirstrule.yar

```shell-session
cmnatic@thm touch myfirstrule.yar
```

3. Open the "myfirstrule.yar" using a text editor such as `nano` and input the snippet below and save the file:

```yaml
rule examplerule {
        condition: true
}
```

  

Inputting our first snippet into "myfirstrule.yar" using nano

```shell-session
cmnatic@thm nano myfirstrule.yar   GNU nano 4.8 myfirstrule.yar
rule examplerule {
        condition: true
}
```

The **name** of the rule in this snippet is `examplerule`, where we have one condition - in this case, the **condition** is `condition`.

As previously discussed, every rule requires both a name and a condition to be valid. This rule has satisfied those two requirements.

Simply, the rule we have made checks to see if the file/directory/PID that we specify exists via `condition: true`. If the file does exist, we are given the output of `examplerule`

Let's give this a try on the file **"somefile"** that we made in step one:  
`yara myfirstrule.yar somefile`  
  
If "somefile" exists, Yara will say `examplerule` because the pattern has been met - as we can see below:

  

Verifying our the examplerule is correct

```shell-session
cmnatic@thm:~$ yara myfirstrule.yar somefile 
examplerule somefile
```

If the file does not exist, Yara will output an error such as that below:  
  

Yara complaining that the file does not exist

```shell-session
cmnatic@thm:~$ yara myfirstrule.yar sometextfile
error scanning sometextfile: could not open file
```

Congrats! You've made your first rule.

Yara Conditions Continued...

Checking whether or not a file exists isn't all that helpful. After all, we can figure that out for ourselves...Using much better tools for the job.  
  
Yara has a few conditions, which I encourage you to read [here](https://yara.readthedocs.io/en/stable/writingrules.html) at your own leisure. However, I'll detail a few below and explain their purpose.  

|   |
|---|
|**Keyword  <br>**|
|Desc|
|Meta|
|Strings|
|Conditions|
|Weight|

  

Meta

This section of a Yara rule is reserved for descriptive information by the author of the rule. For example, you can use `desc`, short for description, to summarise what your rule checks for. Anything within this section does not influence the rule itself. Similar to commenting code, it is useful to summarise your rule.

  
Strings

Remember our discussion about strings in Task 2? Well, here we go. You can use strings to search for specific text or hexadecimal in files or programs. For example, say we wanted to search a directory for all files containing "Hello World!", we would create a rule such as below:

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
}
```

We define the keyword `Strings` where the string that we want to search, i.e., "Hello World!" is stored within the variable `$hello_world`  
  
Of course, we need a condition here to make the rule valid. In this example, to make this string the condition, we need to use the variable's name. In this case, `$hello_world`:

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
		$hello_world
}
```

Essentially, if any file has the string "Hello World!" then the rule will match. However, this is literally saying that it will only match if "Hello World!" is found and will not match if "_hello world_" or "_HELLO WORLD_."

  
To solve this, the condition `any of them` allows multiple strings to be searched for, like below:  

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
		$hello_world_lowercase = "hello world"
		$hello_world_uppercase = "HELLO WORLD"

	condition:
		any of them
}
```

Now, any file with the strings of:

1. Hello World!

2. hello world

3. HELLO WORLD

  

Will now trigger the rule.

Conditions

We have already used the `true` and `any of them` condition. Much like regular programming, you can use operators such as:

- **<=** (less than or equal to)
- **>=** (more than or equal to)
- **!=** (not equal to)

For example, the rule below would do the following:

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
        #hello_world <= 10
}
```

  
The rule will now:

1. Look for the "Hello World!" string  
2. Only say the rule matches if there are less than or equal to ten occurrences of the "Hello World!" string  
  

Combining keywords

Moreover, you can use keywords such as:

- and
- not
- or

To combine multiple conditions. Say if you wanted to check if a file has a string and is of a certain size (in this example, the sample file we are checking is **less than** <10 kb and has "Hello World!" you can use a rule like below:  
  

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!" 
        
        condition:
	        $hello_world and filesize < 10KB 
}
```

  
The rule will now:

1. Look for the "Hello World!" string  
2. Only say the rule matches if there are less than or equal to ten occurrences of the "Hello World!" string  
  

Combining keywords

Moreover, you can use keywords such as:

- and
- not
- or

To combine multiple conditions. Say if you wanted to check if a file has a string and is of a certain size (in this example, the sample file we are checking is **less than** <10 kb and has "Hello World!" you can use a rule like below:  
  

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!" 
        
        condition:
	        $hello_world and filesize < 10KB 
}
```

Yara Modules

Integrating With Other Libraries  

Frameworks such as the [Cuckoo Sandbox](https://github.com/cuckoosandbox/cuckoo) or [Python's PE Module](https://pypi.org/project/pefile/) allow you to improve the technicality of your Yara rules ten-fold.  

  

  

Cuckoo

Cuckoo Sandbox is an automated malware analysis environment. This module allows you to generate Yara rules based upon the behaviours discovered from Cuckoo Sandbox. As this environment executes malware, you can create rules on specific behaviours such as runtime strings and the like.

  

  

Python PE

Python's PE module allows you to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) structure.

  
Explaining this structure is out of scope as it is covered in my [malware introductory room](https://tryhackme.com/room/malmalintroductory). However, this structure is the standard formatting of all executables and DLL files on windows. Including the programming libraries that are used. 

  
Examining a PE file's contents is an essential technique in malware analysis; this is because behaviours such as cryptography or worming can be largely identified without reverse engineering or execution of the sample.

﻿﻿﻿Yara Tools

Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements. 

LOKI (What, not who, is Loki?)

LOKI is a free open-source IOC (_Indicator of Compromise_) scanner created/written by Florian Roth.

Based on the GitHub page, detection is based on 4 methods:

1. File Name IOC Check
2. Yara Rule Check **(we are here)**
3. Hash Check
4. C2 Back Connect Check

There are additional checks that LOKI can be used for. For a full rundown, please reference the [GitHub readme](https://github.com/Neo23x0/Loki/blob/master/README.md).

LOKI can be used on both Windows and Linux systems and can be downloaded [here](https://github.com/Neo23x0/Loki/releases).

﻿﻿﻿Yara Tools

Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements. 

LOKI (What, not who, is Loki?)

LOKI is a free open-source IOC (_Indicator of Compromise_) scanner created/written by Florian Roth.

Based on the GitHub page, detection is based on 4 methods:

1. File Name IOC Check
2. Yara Rule Check **(we are here)**
3. Hash Check
4. C2 Back Connect Check

There are additional checks that LOKI can be used for. For a full rundown, please reference the [GitHub readme](https://github.com/Neo23x0/Loki/blob/master/README.md).

LOKI can be used on both Windows and Linux systems and can be downloaded [here](https://github.com/Neo23x0/Loki/releases).

Displaying Thor Lite's help menu

```shell-session
cmnatic@thm:~$ ./thor-lite-linux-64 -h
Thor Lite
APT Scanner
Version 10.7.3 (2022-07-27 07:33:47)
cc) Nextron Systems GmbH
Lite Version

> Scan Options
  -t, --template string      Process default scan parameters from this YAML file
  -p, --path strings         Scan a specific file path. Define multiple paths by specifying this option multiple times. Append ':NOWALK' to the path for non-recursive scanning (default: only the system drive) (default [])
      --allhds               (Windows Only) Scan all local hard drives (default: only the system drive)
      --max_file_size uint   Max. file size to check (larger files are ignored). Increasing this limit will also increase memory usage of THOR. (default 30MB)

> Scan Modes
      --quick     Activate a number of flags to speed up the scan at cost of some detection.
                  This is equivalent to: --noeventlog --nofirewall --noprofiles --nowebdirscan --nologscan --noevtx --nohotfixes --nomft --lookback 3 --lookback-modules filescan
```

  

FENRIR (naming convention still mythical themed)

This is the 3rd [tool](https://github.com/Neo23x0/Fenrir) created by Neo23x0 (Florian Roth). You guessed it; the previous 2 are named above. The updated version was created to address the issue from its predecessors, where requirements must be met for them to function. Fenrir is a bash script; it will run on any system capable of running bash (nowadays even Windows).

Running Fenrir

```shell-session
cmnatic@thm-yara:~/tools$ ./fenrir.sh
##############################################################
    ____             _
   / __/__ ___  ____(_)___
  / _// -_) _ \/ __/ / __/
 /_/  \__/_//_/_/ /_/_/
 v0.9.0-log4shell

 Simple Bash IOC Checker
 Florian Roth, Dec 2021
##############################################################
```

  

YAYA (_Yet Another Yara Automaton_)

YAYA was created by the [EFF](https://www.eff.org/deeplinks/2020/09/introducing-yaya-new-threat-hunting-tool-eff-threat-lab) (_Electronic Frontier Foundation_) and released in September 2020. Based on their website, "_YAYA is a new open-source tool to help researchers manage multiple YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules and then lets researchers add their own rules, disable specific rulesets, and run scans of files._"

Note: Currently, YAYA will only run on Linux systems.

Running YAYA

```shell-session
cmnatic@thm-yara:~/tools$ yaya
YAYA - Yet Another Yara Automaton
Usage:
yaya [-h]  
    -h print this help screen
Commands:
   update - update rulesets
   edit - ban or remove rulesets
   add - add a custom ruleset, located at 
   scan - perform a yara scan on the directory at 
```

  Using LOKI

As a security analyst, you may need to research various threat intelligence reports, blog postings, etc. and gather information on the latest tactics and techniques used in the wild, past or present. Typically in these readings, IOCs (hashes, IP addresses, domain names, etc.) will be shared so rules can be created to detect these threats in your environment, along with Yara rules. On the flip side, you might find yourself in a situation where you've encountered something unknown, that your security stack of tools can't/didn't detect. Using tools such as Loki, you will need to add your own rules based on your threat intelligence gathers or findings from an incident response engagement (forensics). 

  

As mentioned before, Loki already has a set of Yara rules that we can benefit from and start scanning for evil on the endpoint straightaway.  

  

Loki is located in the `tools`.

  

Listing the tools directory

```shell-session
cmnatic@thm-yara:~/tools$ ls
Loki  yarGen
```

Navigate to the `Loki` directory. Run `python loki.py -h` to see what options are available. 

  

If you are running Loki on your own system, the first command you should run is `--update`. This will add the `signature-base` directory, which Loki uses to scan for known evil. This command was already executed within the attached VM. 

  

Listing Loki signature-base directory

```shell-session
cmnatic@thm-yara:~/tools/Loki/signature-base$ ls
iocs  misc  yara
```

Navigate to the `yara` directory. Feel free to inspect the different Yara files used by Loki to get an idea of what these rules will hunt for.

  

To run Loki, you can use the following command (**note that I am calling Loki from within the file 1 directory**)

  

Instructing Loki to scan the suspicious file

```shell-session
cmnatic@thm-yara:~/suspicious-files/file1$ python ../../tools/Loki/loki.py -p .
```

**Scenario**: You are the security analyst for a mid-size law firm. A co-worker discovered suspicious files on a web server within your organization. These files were discovered while performing updates to the corporate website. The files have been copied to your machine for analysis. The files are located in the `suspicious-files` directory. Use Loki to answer the questions below.

![[Pasted image 20251030155340.png]]
File 2

![[Pasted image 20251030163347.png]]
![[Pasted image 20251030163724.png]]![[Pasted image 20251030163935.png]]

Creating Yara rules with yarGen

From the previous section, we realized that we have a file that Loki didn't flag on. At this point, we are unable to run Loki on other web servers because if **file 2** exists in any of the webs servers, it will go undetected.

We need to create a Yara rule to detect this specific web shell in our environment. Typically this is what is done in the case of an incident, which is an event that affects/impacts the organization in a negative fashion.

We can manually open the file and attempt to sift through lines upon lines of code to find possible strings that can be used in our newly created Yara rule.

Let's check how many lines this particular file has. You can run the following: `strings <file name> | wc -l`.

Using wc to count the amount of lines in the file

```shell-session
cmnatic@thm-yara:~/suspicious-files/file2$ strings 1ndex.php | wc -l
3580
```

If you try to go through each string, line by line manually, you should quickly realize that this can be a daunting task.


What is yarGen? yarGen is a generator for YARA rules.

From the README - "_T__he main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use_."

Navigate to the `yarGen` directory, which is within `tools`. If you are running yarGen on your own system, you need to update it first by running the following command: `python3 yarGen.py --update`. Please note that you cannot update on the VM attached to this room as the VM doesn't have Internet connectivity.

This will update the good-opcodes and good-strings DB's from the online repository. This update will take a few minutes. 

 Once it has been updated successfully, you'll see the following message at the end of the output.
Updating yarGen

```shell-session
cmnatic@thm-yara:~/tools/yarGen$ python3 yarGen.py --update
------------------------------------------------------------------------
                   _____
    __ _____ _____/ ___/__ ___
   / // / _ `/ __/ (_ / -_) _ \
   \_, /\_,_/_/  \___/\__/_//_/
  /___/  Yara Rule Generator
         Florian Roth, July 2020, Version 0.23.3

  Note: Rules have to be post-processed
  See this post for details: https://medium.com/@cyb3rops/121d29322282
------------------------------------------------------------------------
Downloading good-opcodes-part1.db from https://www.bsk-consulting.de/yargen/good-opcodes-part1.db ...
```

  

To use yarGen to generate a Yara rule for file 2, you can run the following command:

`python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar` 

A brief explanation of the parameters above:

- `-m` is the path to the files you want to generate rules for
- `--excludegood` force to exclude all goodware strings (_these are strings found in legitimate software and can increase false positives_)
- `-o` location & name you want to output the Yara rule

If all is well, you should see the following output.

Using yarGen to generate a rule for file2

```shell-session

           [=] Generated 1 SIMPLE rules.
           [=] All rules written to /home/cmnatic/suspicious-files/file2.yar
           [+] yarGen run finished
```

  

Generally, you would examine the Yara rule and remove any strings that you feel might generate false positives. For this exercise, we will leave the generated Yara rule as is and test to see if Yara will flag file 2 or no. 

**Note**: Another tool created to assist with this is called [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/) (you guessed it - created by Florian Roth). We will not examine that tool in this room, but you should read up on it, especially if you decide to start creating your own Yara rules. 

**Further Reading on creating Yara rules and using yarGen**:

- [https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/](https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/)
- [https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/](https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/)
- [https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/](https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/)
- ![[Pasted image 20251030211210.png]]

![[Pasted image 20251030211245.png]]

![[Pasted image 20251030211325.png]]

![[Pasted image 20251030212611.png]]

# 1 — Move to the suspicious files and look around

- **Goal:** get to the folder that contains the suspicious sample(s).
    
- **Command**
    
    `cd ~/suspicious-files/file2 pwd ls -la`
    
- **Explain:** “`cd` moves us to the folder. `pwd` prints the current folder path so we’re sure where we are. `ls -la` lists all files so we can see the suspicious file (e.g., `1ndex.php`).”
    

# 2 — Safely read the top of the file (don’t execute it)

- **Goal:** find the comment/header that likely contains the web-shell name & version.
    
- **Command**
    
    `sed -n '1,40p' 1ndex.php`
    
- **Explain:** “This prints the first 40 lines of the file. We do this to read human comments or banners (the webshell name/version) without running the file.”
    

# 3 — Extract all readable strings from the file (optional background)

- **Goal:** see how many readable text snippets exist inside the file (shows complexity/size).
    
- **Command**
    
    `strings 1ndex.php | wc -l`
    
- **Explain:** “`strings` finds printable text inside the file; `wc -l` counts how many strings. Example: `3580` means lots of readable fragments — useful to know how noisy the file is.”
    

# 4 — Generate a YARA rule from the sample (yarGen)

- **Goal:** create a YARA detection rule based on the sample’s unique strings.
    
- **Command** (run from the yarGen folder for reliability)
    
    `cd ~/tools/yarGen python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar`
    
- **Explain:**
    
    - `-m <path>` tells yarGen which folder to analyze (our sample folder).
        
    - `--excludegood` removes common “good” strings to reduce false alerts.
        
    - `-o <file>` writes the resulting YARA rule to the specified file.
        
    - Outcome: a `.yar` file that contains string signatures and a condition that can identify the sample.
        

# 5 — Test the generated YARA rule against the sample (basic)

- **Goal:** confirm the rule matches the sample file.
    
- **Command**
    
    `cd ~/suspicious-files yara file2.yar file2/1ndex.php`
    
- **Explain:** “`yara` applies the rule (`file2.yar`) to the sample. If the rule matches, it prints the rule name and the filename — that means detection works.”
    

# 6 — Show exactly which string variable matched (so you can report the 4-char name)

- **Goal:** see which string inside the YARA rule matched the file (YARA prints the variable that matched).
    
- **Command**
    
    `yara -s file2.yar file2/1ndex.php`
    
- **Explain:** “`-s` makes YARA print _which_ string(s) matched. The output shows offset, the YARA variable (e.g. `$s20` or `$x1`), and the snippet. The variable (like `$s20`) is the 4-character answer TryHackMe expects.”
    

# 7 — Inspect the YARA rule to read its `strings:` block

- **Goal:** review the strings that were placed into the rule (so you can count them and review for false positives).
    
- **Commands**
    
    `# Show the whole rule header (first 120 lines) sed -n '1,120p' /home/cmnatic/suspicious-files/file2.yar  # Print only the strings: block (clean view) awk '/strings:/{p=1; next} /condition:/{p=0} p' /home/cmnatic/suspicious-files/file2.yar | nl -ba  # Count how many $... string definitions are in the .yar file (total) grep -E '^\s*\$' /home/cmnatic/suspicious-files/file2.yar | wc -l`
    
- **Explain:**
    
    - `awk` extracts only the `strings:` area so you can read the `$var = "..."` lines.
        
    - `nl -ba` numbers those lines to make reviewing easier.
        
    - `grep ... | wc -l` counts lines starting with `$` — the number of YARA strings generated.
        

# 8 — (Important) Count strings _only for the rule that matched_

- **Goal:** if the YARA file contains multiple rules, count strings only for the rule that fired.
    
- **Commands (concise learner version)**
    
    1. Get the rule name that matched:
        
        `RULE=$(yara file2.yar file2/1ndex.php | awk 'NR==1{print $1}') echo $RULE`
        
    2. Count `$` strings inside that rule:
        
        `awk -v r="$RULE" '   /^rule[[:space:]]+/ { cur=$2; sub(/\{.*/,"",cur); in_strings=0 }   /^strings:/ && cur==r { in_strings=1; next }   /^condition:/ && cur==r { in_strings=0 }   in_strings && cur==r && /^\s*\$/ { c++ }   END { print c } ' /home/cmnatic/suspicious-files/file2.yar`
        
- **Explain:** “First we capture the exact rule name that matched; then we run a short `awk` script to count only the `$...` lines inside that matching rule. The printed number is the answer TryHackMe expects.”
    

# 9 — Copy your YARA rule into Loki’s signature folder (so Loki can use it)

- **Goal:** add your custom rule to Loki’s signatures so Loki will detect the sample during its scan.
    
- **Commands** (from `~/tools/Loki`)
    
    `# find the folder Loki reads (example returned ./test/yara) find . -type d -iname "yara" -print -quit  # copy the rule into the discovered folder (example: ./test/yara) cp /home/cmnatic/suspicious-files/file2.yar ./test/yara/  # also copy to the standard signature folder (most Loki installs) cp /home/cmnatic/suspicious-files/file2.yar ./signature-base/yara/ 2>/dev/null || true  # verify the file is present ls -la ./test/yara | grep file2.yar ls -la ./signature-base/yara | grep file2.yar`
    
- **Explain:** “We copy the new rule into the folder Loki loads its YARA rules from. `find` helps us discover the correct path. `ls` confirms the copy.”
    

# 10 — Install YARA Python bindings if Loki errors with `No module named 'yara'`

- **Goal:** provide Loki with the Python YARA bindings so it can load `.yar` rules via Python.
    
- **Commands**
    
    `sudo apt update sudo apt install -y python3-pip libyara-dev pip3 install yara-python # verify python3 -c "import yara; print('YARA module installed')"`
    
- **Explain:** “Loki uses Python to call YARA. If the Python module isn’t present, Loki can’t load YARA rules — we install the system library and the Python package.”
    

# 11 — Re-run Loki to scan the sample (and confirm the rule fires)

- **Goal:** make Loki scan the folder and demonstrate that it flags the file using your rule.
    
- **Command**
    
    `cd ~/tools/Loki python3 loki.py -p /home/cmnatic/suspicious-files/file2 2>&1 | tee ~/loki_test_file2.txt tail -n 80 ~/loki_test_file2.txt`
    
- **Explain:** “`loki.py -p <path>` scans the path for indicators. We capture output into a file and view the tail so we can see alerts. If Loki loads your rule, it will show a YARA rule match and the matched string variable or snippet.”
    

# 12 — Helpful quick checks & troubleshooting lines (meaningful and short)

- **Check file exists where you think it is**
    
    `ls -la /home/cmnatic/suspicious-files/file2`
    
    _Explain:_ verify sample present.
    
- **Show where yara file2.yar is**
    
    `find ~ -type f -name "file2.yar" 2>/dev/null`
    
    _Explain:_ find the generated rule if you misplaced it.
    
- **Print which YARA variables matched (just the variable names)**
    
    `yara -s file2.yar file2/1ndex.php | grep '0x' | awk -F: '{print $2}'`
    
    _Explain:_ extracts only the `$variable` names (the 4-character answers TryHackMe asks for).
    

---

## Short example flow — what to show on a single slide (copy/paste)

1. `cd ~/suspicious-files/file2` — go to sample
    
2. `sed -n '1,40p' 1ndex.php` — read header (get `b374k` and `3.2.3`)
    
3. `strings 1ndex.php | wc -l` — raw readable strings count (`3580`)
    
4. `python3 ~/tools/yarGen/yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar` — generate rule
    
5. `yara -s file2.yar file2/1ndex.php` — see matched variable (e.g. `$s20`)
    
6. `grep -E '^\s*\$' ~/suspicious-files/file2.yar | wc -l` — count strings in the rule (submit the integer)
    
7. `cp ~/suspicious-files/file2.yar ~/tools/Loki/signature-base/yara/` — copy rule into Loki signatures
    
8. `python3 loki.py -p /home/cmnatic/suspicious-files/file2` — run Loki to confirm detection
    

(Each slide note: what to expect, what the output means — e.g., “`yara` prints rule name and file when matched.”)

---

## How to explain this to a non-technical audience (single sentence each)

- **`sed -n '1,40p' file`** → “We preview the top of the file to read its label, like checking the cover of a book.”
    
- **`strings | wc -l`** → “We count how many readable fragments are inside — shows how noisy/complex the file is.”
    
- **`yarGen`** → “A helper tool that suggests fingerprints (signatures) from this file.”
    
- **`yara`** → “YARA applies signatures to files and tells us when something matches — like scanning for telltale fingerprints.”
    
- **`cp ... to Loki`** → “Add our fingerprint to the central detector so the automated scanner (Loki) will recognize it.”
    
- **`python3 loki.py -p ...`** → “Run the automated scanner to see if it flags the file using our new fingerprint.”


**Valhalla**

**Valhalla** is an online Yara feed created and hosted by [Nextron-Systems](https://www.nextron-systems.com/valhalla/) (erm, Florian Roth). By now, you should be aware of the ridiculous amount of time and energy Florian has dedicated to creating these tools for the community. Maybe we should have just called this the Florian Roth room. (lol)

Per the website, "_Valhalla boosts your detection capabilities with the power of thousands of hand-crafted high-quality YARA rules._"

![A picture displaying the search menu for the Valhalla tool.](https://assets.tryhackme.com/additional/yara/yara13.png)  

From the image above, we should denote that we can conduct searches based on a keyword, tag, ATT&CK technique, sha256, or rule name. 

**Note**: For more information on ATT&CK, please visit the [MITRE](https://tryhackme.com/room/mitre) room. 

Taking a look at the data provided to us, let's examine the rule in the screenshot below:

![A picture displaying the results of a rule, depicting the rule name, description and the date it was submitted to Valhalla](https://assets.tryhackme.com/additional/yara/yara14.png)  

We are provided with the name of the rule, a brief description, a reference link for more information about the rule, along with the rule date. 

Feel free to look at some rules to become familiar with the usefulness of Valhalla. The best way to learn the product is by just jumping right in. 

Picking up from our scenario, at this point, you know that the 2 files are related. Even though Loki classified the files are suspicious, you know in your gut that they are malicious. Hence the reason you created a Yara rule using yarGen to detect it on other web servers. But let's further pretend that you are not code-savvy (FYI - not all security professionals know how to code/script or read it). You need to conduct further research regarding these files to receive approval to eradicate these files from the network. 

Time to use Valhalla for some threat intelligence gathering...

![[Pasted image 20251030214942.png]]

![[Pasted image 20251030220906.png]]


![[Pasted image 20251030220830.png]]

![[Pasted image 20251030222916.png
![[Pasted image 20251030225300.png]]

In this room, we explored Yara, how to use Yara, and manually created basic Yara rules. We also explored various open-source tools to hit the ground running that utilizes Yara rules to detect evil on endpoints.

By going through the room scenario, you should understand the need (_as a blue teamer_) to know how to create Yara rules effectively if we rely on such tools. Commercial products, even though not perfect, will have a much richer Yara ruleset than an open-source product. Both commercial and open-source will allow you to add Yara rules to expand its capabilities further to detect threats. 

If it is not clear, the reason why **file 2** was not detected is that the Yara rule was not in the Yara file used by Loki to detect the hack tool (web shell) even though its the hack tool has been around for years and has even been attributed to at least 1 nation-state. The Yara rule is present in the commercial variant of Loki, which is Thor. 

There is more that can be done with Yara and Yara rules. We encourage you to explore this tool further at your own leisure.

# 🧠 TryHackMe YARA & Loki Investigation Notes

## 🧩 Objective

Analyze two suspicious PHP files using **Loki** and **YARA** to identify:

- Whether files are malicious or benign
    
- Which **YARA rules** triggered detections
    
- What strings, hashes, and patterns were matched
    
- How to cross-reference findings with **Valhalla** or **VirusTotal**
    

---

## ⚙️ Tools Used

- **Loki** – Open-source IOC scanner built by Florian Roth
    
- **YARA** – Rule-based pattern matcher for malware signatures
    
- **yarGen** – Auto-generates YARA rules from samples
    
- **Valhalla** – Public YARA rule & threat intelligence database
    
- **VirusTotal** – Online multi-AV hash scanner
    

---

## 🧭 Workflow Summary

### 🔹 1. Locate and inspect suspicious files

`cd ~/suspicious-files/file1 sed -n '1,40p' ind3x.php     # Shows file header, name & version cd ~/suspicious-files/file2 sed -n '1,40p' 1ndex.php`

**Finding:**

- File 1 → contains `b374k shell 3.2.3` → known PHP webshell
    
- File 2 → contains `Zepto v1.1.2` JavaScript library reference
    

---

### 🔹 2. Run Loki to scan for YARA matches

`python3 ~/tools/Loki/loki.py -p ~/suspicious-files/file1 python3 ~/tools/Loki/loki.py -p ~/suspicious-files/file2`

**Loki output shows:**

- File 1 → **Matched rule:** `webshell_b374k_rule1`
    
- File 2 → **Matched rule:** `_home_cmnatic_suspicious_files_file2_1ndex`
    
- “REASON 1” and “MATCHES” lines identify which YARA rule triggered.
    

---

### 🔹 3. Examine YARA match details

`yara -s file2.yar file2/1ndex.php`

Shows variable that matched (e.g. `$x1`, `$s20`, etc.) and the code snippet that triggered.

---

### 🔹 4. Count YARA rule strings

`grep -E '^\s*\$' file2.yar | wc -l`

Each `$` = a string condition in the rule.  
Used to answer “How many strings were generated?”

---

### 🔹 5. Calculate SHA-256 hashes

`sha256sum ~/suspicious-files/file1/ind3x.php sha256sum ~/suspicious-files/file2/1ndex.php`

**Results**

- File 1 → `5479f8cd1375364770df36e5a18262480a8f9d311e8eedb2c2390ecb233852ad`
    
- File 2 → `53fe44b4753874f079a936325d1fdc9b1691956a29c3aaf8643cbdb49f5984bf`
    

---

### 🔹 6. Cross-reference hashes online

- **Valhalla** ([https://valhalla.nextron-systems.com](https://valhalla.nextron-systems.com?utm_source=chatgpt.com))
    
    - Paste the SHA-256 hash in **Hash Lookup**
        
    - Requires a free account
        
    - If no result → file not in public DB (normal)
        
- **VirusTotal**
    
    - Paste same hash
        
    - Checks if any AV vendors already flagged it
        

**Outcome:**  
File 1 → recognized (linked to b374k webshell).  
File 2 → no public hash entry (unique sample).

---

### 🔹 7. Explore local YARA signatures

`cd ~/tools/Loki/signature-base/yara grep -R -n -i "b374k\|zepto\|webshell" . 2>/dev/null`

**Finding:**

- `webshell_b374k_rule1` located in Loki’s webshell signatures
    
- Confirms detection source for file 1
    

---

## 🧠 Key Takeaways

### 🧾 Concept Learning

- **YARA Rules** detect malware using text/string patterns.
    
- **Loki** maps these rules to file scans, producing “REASON 1” detections.
    
- **yarGen** can auto-generate new YARA rules from unknown samples.
    
- **Valhalla** & **VirusTotal** are intel databases for validating hashes.
    
- Each YARA rule includes:
    
    - `meta:` → info (author, description)
        
    - `strings:` → list of detectable patterns (`$s1`, `$x2`, etc.)
        
    - `condition:` → logic combining strings to trigger detection.
        

---

### 🕵️‍♂️ Analytical Results

|File|Finding|Rule Match|SHA-256|Verdict|
|---|---|---|---|---|
|`file1/ind3x.php`|b374k webshell (PHP backdoor)|`webshell_b374k_rule1`|5479f8cd1375...852ad|**Malicious**|
|`file2/1ndex.php`|Zepto JS variant / obfuscated webshell|`_home_cmnatic_suspicious_files_file2_1ndex`|53fe44b4753...5984bf|**Suspicious / Malicious**|

---

### 💡 Practical Skills Learned

- Reading **Loki output** and identifying rule matches
    
- Using **grep/sed/less** to inspect PHP headers
    
- Counting **YARA strings** to answer analysis questions
    
- Extracting **matched variables** with `yara -s`
    
- Generating **SHA256** hashes and validating via threat-intel sites
    
- Navigating **Loki’s signature-base** to find rule definitions
    
- Understanding the workflow from **local detection → global verification**
    

---

### 🗣️ How to Explain to Others

> “In this lab, I learned how analysts detect and classify malicious files using YARA rules and Loki.  
> Loki scans files against a database of known signatures, and each hit corresponds to a specific rule — similar to how antivirus engines work.  
> By checking the file headers, matched strings, and hashes, we can identify what malware family or webshell the file belongs to.  
> Finally, we validate those findings through public databases like Valhalla or VirusTotal to confirm whether it’s a known threat or a new variant.”
---

## Related Notes
- [[Pyramid of Pain]]
- [[Threat Intelligence Tools]]
- [[Malware Classification]]
- [[Summit]]
- [[Intro to Cyber Threat Intel]]
