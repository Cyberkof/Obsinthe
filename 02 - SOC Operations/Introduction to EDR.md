
## Task 1 : Introduction

Endpoint Detection and Response (EDR) is one of the most critical security solutions in modern cybersecurity. Unlike traditional antivirus software, which primarily focuses on signature-based detection, EDR goes a step further by continuously monitoring endpoint activity, detecting suspicious behavior, and providing response capabilities to contain threats in real time.

For a SOC (Security Operations Center) analyst, understanding how EDR functions is essential, since it has become a standard defense mechanism across organizations. In this task, we explore the fundamental differences between EDR and traditional antivirus, the types of telemetry data collected from endpoints, and the architecture that enables its detection and response capabilities.

### Learning Objectives :

By the end of this section, you will be able to:

- Understand the basics of EDR and how it works.
- Differentiate between EDR and traditional antivirus solutions.
- Examine the core architecture of an EDR solution.
- Identify the types of telemetry data collected from endpoints.
- Understand the detection and response capabilities EDR provides.
- Investigate a realistic EDR alert.

### Prerequisites :

Before diving into this section, it is recommended to have:

- A basic understanding of endpoints (Windows, Linux, Mac) and common attack techniques.
- Awareness of the SOC team’s role in detecting and responding to security incidents.

Once you’re ready, let’s move forward!

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*pxEcNZgu9wZpbeXeP3Nveg.png)

## Task 2 : What is an EDR?

### Question 1 : Which feature of EDR provides a complete context for all the detections?

The feature of EDR that provides a **complete context for detections is _Visibility_.**

Why? Because EDR doesn’t just show you an alert , it records **everything happening on the endpoint** (process activity, file changes, registry modifications, user actions, and more). This data is then presented in structured views like **process trees** and timelines.

So instead of a single alert saying _“malicious file detected,”_ you get the **full chain of events,** which process spawned it, what changes it made, and how it connects to other activities. This context is what allows SOC analysts to understand the bigger picture and make accurate decisions.

> **Answer : Visibility  
> because it shows the full context of endpoint activity through process trees and telemetry.**

### Question 2 : Which process spawned sc.exe?

In an EDR process tree, every child process is linked back to its parent. By following the chain, analysts can trace where a suspicious process originated.

From the screenshot, we see that `sc.exe` (Service Control utility) was **not launched directly** , it was spawned by `cmd.exe`. This detail is important because attackers often use **command-line utilities** like `cmd.exe` to run administrative tools (`sc.exe`, `net.exe`, `powershell.exe`) for malicious purposes such as **creating new services** or **establishing persistence**.

Being able to see this parent-child relationship is what gives EDR its power: instead of just flagging `sc.exe`, it provides the **context** of how and why it was executed.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*cDfiSt-TTS0KcZmQdi9ekA.png)

Click on the above image to expand

> **Answer : cmd.exe**  
> `sc.exe` was spawned by **cmd.exe**.

### Task 2 complete ✅

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*G6ZlUroeqMJjdD7Tr1fU3Q.png)

## Task 3 : Beyond the Antivirus

### Question 1 : In the given analogy, what presents an AV?

In the given analogy, the **Antivirus (AV)** is compared to the **immigration check at an airport.**

Just like immigration officers check the passports of travelers against a database of known criminals, an antivirus checks files and processes against its **signature database.** If it finds a match, it blocks the threat.

But the limitation is the same:

- If the person (file/process) has no criminal record (no known malicious signature), immigration (AV) lets them pass.
- Similarly, AV misses advanced or unknown threats that don’t match its signature database.

This is why EDR , represented as **security officers inside the airport monitoring behavior via CCTV and sensors** , is needed as an additional layer.

> **Answer : Immigration Check**  
> In the analogy, an **Antivirus (AV) is represented by the immigration check at an airport.**

### Question 2 : Which legitimate process was hijacked by the attacker in the scenario?

In the attack scenario, the attacker used a phishing email with a malicious Word macro that eventually executed obfuscated PowerShell commands. These commands downloaded a second-stage payload.

Instead of running openly (where security tools might catch it), the payload was **injected into a legitimate Windows process —** `**svchost.exe**`**.**

This is a classic **process injection technique**. Attackers often hijack trusted system processes like `svchost.exe` to:

- Blend in with normal system activity,
- Evade signature-based antivirus detection, and
- Maintain persistence while avoiding suspicion.

From the comparison table:

- The **AV** missed this stage because it does not monitor memory injections.
- The **EDR** detected the **process injection into** `**svchost.exe**` and flagged it as suspicious.

> **Answer : svchost.exe**  
> The legitimate process hijacked by the attacker was `**svchost.exe**`

### Question 3 : Which security solution might mark this activity as clean?

In the scenario, the attacker went through several stages , from phishing and malicious macros to obfuscated PowerShell and finally process injection into `svchost.exe`.

Now, let’s compare how **Antivirus (AV)** and **EDR** react at the end of the attack chain:

- **Antivirus (AV):**  
    Since AV mainly relies on known signatures and does not monitor deep behaviors (like obfuscated scripts, process injection, or unusual outbound connections), it might miss all these advanced steps. As a result, it could mark the system as **clean**, even though the attacker has already gained access.
- **EDR:**  
    On the other hand, EDR continuously monitors endpoint behaviors, detects the unusual process relationships, flags the injection into `svchost.exe`, and alerts analysts with the full attack chain.

This highlights the big difference: **AV is good at catching “known” threats, but EDR is designed to detect “unknown” and advanced attacks.**

> **Answer : Antivirus  
> **The **Antivirus (AV)** might mark this activity as clean.

### Task 3 is now Done ✅

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*gHLeQcuaAnlqM4M3YjdTOg.png)

## Task 4 : How an EDR works?

### Question 1: Which component of the EDR is responsible for collecting telemetry from the endpoints?

The “magic” behind EDR lies in its **two core components: Agents and Console.**

1. **Agents (Sensors)**

- Small programs deployed on each endpoint (laptops, desktops, servers).
- These agents act as the _eyes and ears_ of the EDR — continuously monitoring activities like file changes, process executions, registry modifications, and network connections.
- They perform basic detections locally and send detailed telemetry to the central console in real time.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/0*SU7-YXVPL3envcWR.png)

**2. EDR Console**

- The central hub where all the data from agents is collected.
- Uses **correlation logic, machine learning, and threat intelligence feeds** to detect suspicious behavior.
- Displays detections in a dashboard with severities (Critical, High, Medium, Low), helping SOC analysts prioritize investigations.
- From the console, analysts can not only investigate but also **respond with a click**: isolate an endpoint, kill a malicious process, or quarantine files.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/0*nroh06huCB_hjhRc.png)

_CrowdStrike Falcon EDR Console with detections, severity levels, and dashboards_

**3. What Happens After Detection?**

- SOC analysts review alerts → decide if they’re false positives or true positives.
- For true positives, analysts can act instantly from the console.
- Example: If a process injection is detected, the analyst can isolate the host or terminate the malicious process in real time.

**4. EDR with Other Tools**

- EDR is powerful on its own but becomes even stronger when integrated into the organization’s broader **security ecosystem** (Firewalls, DLP, IAM, Email Security, etc.).
- All tools usually feed data into a **SIEM**, giving analysts one central place to investigate.

> **Answer : Agent  
> **_An EDR provides visibility and response capabilities through endpoint agents (sensors) that monitor activity and send data to a centralized EDR console, where advanced analysis and response actions happen._

### Question 2 : An EDR agent is also known as a?

An **EDR agent** is a lightweight program installed on endpoints (like laptops, desktops, and servers) to continuously monitor activity. Since its role is to **observe and report everything happening on the endpoint**, it is also commonly referred to as a **sensor**.

## Get Sunny Singh Verma [ SuNnY ]’s stories in your inbox

Join Medium for free to get updates from this writer.

Subscribe

Just like sensors in real life detect motion, temperature, or pressure, an EDR sensor detects processes, file changes, registry modifications, and network activity — then sends this telemetry to the central EDR console for analysis.

> **Answer : Sensor**

### Task 4 done ✅

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*n7AUQIARujIYXQXWjcQ2BA.png)

## Task 5: EDR Telemetry

### Question 1 : Which telemetry data helps in detecting C2 communications?

EDR collects a wide range of **telemetry data** from endpoints, such as process executions, file changes, registry modifications, and command-line activity.

When it comes to detecting **Command-and-Control (C2) communications**, the most useful telemetry is **Network Connections**.

Why? Because C2 activity typically involves the infected endpoint making unusual outbound connections — for example:

- Connecting to suspicious IPs or domains controlled by attackers.
- Using uncommon ports or protocols.
- Maintaining a persistent connection to an external server for remote commands.
- Exfiltrating data outside the organization.

By monitoring **all network connections** from endpoints, the EDR can spot these anomalies and flag potential C2 behavior.

> **Answer : Network Connections**

### Question 2 : Where are the configuration settings of a Windows system primarily stored?

On a Windows system, most of the critical **configuration settings** — such as information about hardware, installed software, system policies, user accounts, startup programs, and services — are stored in the **Windows Registry**.

The Registry acts like a **central database** for the operating system. Whenever a program is installed, a service is configured, or a system setting is changed, the Registry gets updated.

Because of this, attackers also frequently modify registry keys for:

- **Persistence** (e.g., making malware run at startup).
- **Privilege escalation** (changing security-related keys).
- **Defense evasion** (disabling security tools).

This is why EDR solutions closely monitor **registry modifications** as part of their telemetry.

> **Answer : Registry**

**Task 5 is successfully done ! ✅**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*BLCSBVLFsJ6I4_7EQQC6GA.png)

## Task 6 : Detection And Response Capabilities

### Question : Which feature of the EDR helps you identify threats based on known malicious behaviours?

One of the powerful features of an EDR is its ability to integrate with **threat intelligence feeds** and use **IOC (Indicators of Compromise) Matching** to detect threats.

An IOC can be:

- A file hash (MD5, SHA256)
- A malicious IP address or domain
- A registry key
- A known malicious process name or path

When the EDR agent collects telemetry from endpoints, it compares this data against the IOCs from threat intelligence. If there’s a match, the activity is flagged as malicious immediately.

Example: If a user downloads a file and its hash matches one published in a threat feed for a known malware campaign, the EDR will instantly detect and alert on it — even if the file hasn’t yet executed.

This feature helps analysts quickly identify **known malicious behaviors** without needing to rely only on anomaly or behavioral detection.

> **Answer : IOC Matching**

**We are now done with Task 6 as well !** ✅

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*odloCfTllirQh60BUlZG7w.png)

## Task 7 : Investigate an alert on EDR

### Question 1 : Which tool was launched by CMD.exe to download the payload on DESKTOP-HR01?

When investigating alerts in an EDR console, one of the most useful features is the **process chain view**. It shows the sequence of events from the initial execution all the way to the final payload.

Looking at the screenshot below, we can clearly trace the flow of processes:

1. **WINWORD.EXE** — Microsoft Word was launched with a macro-enabled document (`invoice.docm`).
2. **CMD.EXE** — The malicious macro spawned a Windows command shell.
3. **CURL.EXE** — From that command shell, the attacker executed `CURL.exe`, a legitimate file transfer tool built into Windows, to download a payload.
4. **INSTALL.EXE** — The downloaded file was then saved and executed as `install.exe`.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*oLgWuJy5PcB_VWpjolo5JA.gif)

Click the image to make it fullscreen

The key takeaway is that the **tool launched by CMD.exe was** `**CURL.exe**`. Attackers often abuse built-in utilities like `CURL`, `BITSAdmin`, or `PowerShell` to avoid dropping obvious malware and instead “live off the land.”

> **Answer : CURL.exe**

### Question 2 : What is the absolute path to the downloaded malware on the DESKTOP-HR01 machine?

When an attacker uses a built-in tool like **CURL.exe** to download a payload, the EDR agent records not only the parent-child relationship but also the **file path** of the newly created executable.

To find this information, you can expand the process details in the EDR console. In our case, the **process chain view** showed:

- **WINWORD.EXE → CMD.EXE → CURL.EXE → INSTALL.EXE**
- By clicking on the **INSTALL.EXE node**, the EDR provided details such as the full file path, hash, and execution time.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*H11g-s3QL6ZPY34n8JHSOg.gif)

Click the image to make it fullscreen

Press enter or click to view image in full size![](https://miro.medium.com/v2/resize:fit:1351/1*IuOpge08dcfjcpglKkWQtQ.png)

Press enter or click to view image in full size![](https://miro.medium.com/v2/resize:fit:1357/1*QoziiurmlKbIA93eRRqBJg.png)

Click the image to make it fullscreen

> **Answer : C:\Users\Public\install.exe**

### Question 3 : What is the absolute path to the suspicious syncsvc.exe on the WIN-ENG-LAPTOP03 machine?

The EDR console provides **process details** for every executable flagged as suspicious. To answer this question, we need to:

1. Go to the **Recent Detections** panel.
2. Locate the detection on **WIN-ENG-LAPTOP03**.
3. Expand the detection to view the **process details** for `syncsvc.exe`.
4. Look at the **Path field** in the **Process Info tab**.

From the telemetry, the file was located in a **Temp directory**, which is often abused by attackers for staging malware, since regular users have write access there.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*5Kg1qEGB60rt8gVczvNYRQ.gif)

Click on the image to enlarge

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*OW5SFMywfDPTOo6D9bt4Kw.png)

Click on the image to enlarge

> **Answer : C:\Users\haris.khan\AppData\Local\Temp\syncsvc.exe**

### Question 4 : On which URL was the exfiltration attempt being made on WIN-ENG-LAPTOP03?

When investigating the detection on **WIN-ENG-LAPTOP03**, the EDR console flagged a suspicious process — `syncsvc.exe` — located in the Temp directory. This tool was used for **credential dumping via LSASS memory access**, which created a dump file (`dump_2025.dmp`).

But the most critical finding came from the **Network Activity section** in the process details. As highlighted in the screenshot below, the EDR recorded that `syncsvc.exe` attempted to **exfiltrate the dump file** to an external server:

**Attempted exfil to:**  
`[https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp](https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp)`

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*QR4VCP9fXcyveicNkIKyRQ.png)

> **Answer :**  
> `[https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp](https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp)`

### Question 5 : What was UpdateAgent.exe labelled by Threat Intel on DESKTOP-DEV01?

When investigating detections, it’s important to check whether a flagged executable is truly malicious or if it is a **false positive**. This is where **Threat Intelligence integration** in the EDR becomes valuable — it provides additional context about known files and processes.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*fl-Q7hMq-7-ZND9gDX9DPA.gif)

In the screenshot below, the process **UpdateAgent.exe** (executed from the user’s AppData directory) was reviewed in the EDR console. Under the **Threat Intel** section, the file was labeled as:

**“Known internal IT utility tool.”**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*tjagl2nm66ytQK03XrCZkA.png)

This means that the EDR recognized this executable as a legitimate, internally-used application and not part of malicious activity. While the process was flagged due to its location and behavior (execution from AppData and outbound connection attempt), the threat intelligence feed clarified its safe classification.

### Task 7 Now Accomplished ! ✅

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*1DXMO9kO_W1vIe-pNK6Dbg.png)
---

## Related Notes
- [[SOC Fundamentals]]
- [[Sysmon]]
- [[Intro to Logs]]
- [[Malware Classification]]
- [[SOC Topology]]
