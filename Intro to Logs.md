
Working with Logs: Scenario

**Scenario:** A web server of **SwiftSpend Financial** is constantly bombarded with scans from an adversary. As a systems administrator of this organisation tasked to address this predicament, you must identify what the adversary is doing by configuring logging and analysing collected logs.

**IMPORTANT:** The user **damianhall** has limited sudo privileges. Issue the command _**sudo -l**_ to check what commands can be run by this user. These limited commands are all that are needed to complete the subsequent tasks.

Connecting to the machine

Start the virtual machine in split-screen view by clicking the green **Start Machine** button below.

If the VM is not visible, use the blue **Show Split View** button at the top-left of the page. Alternatively, using the credentials below, you can connect to the VM via RDP or SSH.

![THM Key Credentials](https://tryhackme-images.s3.amazonaws.com/user-uploads/63588b5ef586912c7d03c4f0/room-content/be629720b11a294819516c1d4e738c92.png)

|   |   |
|---|---|
|**Username**|damianhall|
|**Password**|Logs321!|
|**IP**|10.80.190.214|

  

**IMPORTANT:** The attached VM contains artefacts to help us better understand logs and the implications of their analysis to the detection engineering and incident response practices. Work on the subsequent tasks and experiment with the VM through a case example. Escalation of Privileges is **NOT** necessary to answer the questions in this room.

In the Heart of Data: Logs

Just as a physical tree's rings reveal its life story – indicating good years with thick curls and challenging ones with thin – a digital log provides a historical record of system activity.

Both embody a fundamental principle of growth over time and serve as living records in their respective domains – physical and digital.

In the digital world, every interaction with a computer system – from authentication attempts, granting authorisation, accessing a file, and connecting to a network to encountering a system error – will always leave a digital footprint in the form of logs.

|   |   |
|---|---|
|![Components of a digital log](https://tryhackme-images.s3.amazonaws.com/user-uploads/63da722f2d207d0049da10b1/room-content/624b4e33606f8b0e1dc2ff887eb70c3f.svg)|Logs are a record of events within a system. These records provide a detailed account of what a system has been doing, capturing a wide range of events such as user logins, file accesses, system errors, network connections, and changes to data or system configurations.<br><br>While the specific details may differ based on the type of log, a log entry usually includes the following information:<br><br>- A timestamp of when an event was logged<br>- The name of the system or application that generated the log entry<br>- The type of event that occurred<br>- Additional details about the event, such as the user who initiated the event or the device's IP address that generated the event<br><br>This information is typically stored in a **log file**, which contains aggregated entries of what occurred at any given time on a system.|

However, since digital interactions are continuous and fast-paced, the log file's size may exponentially grow depending on the activities logged on a system.

The True Power of Logs: Contextual Correlation

A single log entry may seem insignificant on its own. But when log data is aggregated, analysed, and cross-referenced with other sources of information, it becomes a potent investigation tool. Logs can answer critical questions about an event, such as:

- **What** happened?
- **When** did it happen?
- **Where** did it happen?
- **Who** is responsible?
- **Were** their actions **successful**?
- **What** was the result of their action?

The following hypothetical scenario can illustrate this aspect. Suppose a student allegedly accessed inappropriate content on a University network. By reviewing the logs, a systems administrator could then answer the following:

|Question|Answer|
|---|---|
|What happened?|An adversary was confirmed to have accessed SwiftSpend Financial's GitLab instance.|
|When did it happen?|Access started at 22:10 on Wednesday, September 8th, 2023.|
|Where did it happen?|The event originated from a device with an IP address of 10.10.133.168 within the VPN Users' segment (10.10.133.0/24).|
|Who is responsible?|Upon examining the network logs, it was observed that the device, identified by the User-Agent "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0", was allocated the IP address 10.10.133.168.|
|Were they successful?|Yes, since an API Key was found to be publicly exposed on the GitLab instance. Moreover, the web proxy logs confirm that the adversary device reached _gitlab.swiftspend.finance_ and maintained access through their uploaded web shell.|
|What is the result of their action?|The adversary achieved remote code execution on _gitlab.swiftspend.finance_ and performed post-exploitation activities.|

The example above emphasises how logs are instrumental in piecing together a complete picture of an event, thereby enhancing our understanding and ability to respond effectively.



Log Types

Specific log types can offer a unique perspective on a system's operation, performance, and security. While there are various log types, we will focus on the most common ones that cover approximately 80% of the typical use cases.

Below is a list of some of the most common log types:

|   |   |
|---|---|
|![A screen with various log types](https://tryhackme-images.s3.amazonaws.com/user-uploads/63da722f2d207d0049da10b1/room-content/dd8471228f690b259b22b69d39b18acc.svg)|- **Application Logs:** Messages about specific applications, including status, errors, warnings, etc.<br>- **Audit Logs:** Activities related to operational procedures crucial for regulatory compliance.<br>- **Security Logs:** Security events such as logins, permissions changes, firewall activity, etc.<br>- **Server Logs:** Various logs a server generates, including system, event, error, and access logs.<br>- **System Logs:** Kernel activities, system errors, boot sequences, and hardware status.<br>- **Network Logs:** Network traffic, connections, and other network-related events.<br>- **Database Logs:** Activities within a database system, such as queries and updates.<br>- **Web Server Logs:** Requests processed by a web server, including URLs, response codes, etc.|

  

Understanding the various log types, formats, and standards is critical for practical log analysis. It enables an analyst to effectively parse, interpret, and gain insights from log data, facilitating troubleshooting, performance optimisation, incident response, and threat hunting.

Log Formats

A log format defines the structure and organisation of data within a log file. It specifies how the data is encoded, how each entry is delimited, and what fields are included in each row. These formats can vary widely and may fall into three main categories: Semi-structured, Structured, and Unstructured. We'll explore these categories and illustrate their usage with examples.

- **Semi-structured Logs:** These logs may contain structured and unstructured data, with predictable components accommodating free-form text. Examples include:
    
    - **Syslog Message Format:** A widely adopted logging protocol for system and network logs.
        
        Example of a log file utilising the Syslog Format
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat syslog.txt
        May 31 12:34:56 WEBSRV-02 CRON[2342593]: (root) CMD ([ -x /etc/init.d/anacron ] && if [ ! -d /run/systemd/system ]; then /usr/sbin/invoke-rc.d anacron start >/dev/null; fi)
        ```
        
          
        
    - **Windows Event Log (EVTX) Format:** Proprietary Microsoft log for Windows systems.
        
        Example of a log file utilising the Windows Event Log (EVTX) Format
        
        ```shell-session
        PS C:\WINDOWS\system32> Get-WinEvent -Path "C:\Windows\System32\winevt\Logs\Application.evtx"
        
        
           ProviderName: Microsoft-Windows-Security-SPP
        
        TimeCreated                      Id LevelDisplayName Message
        -----------                      -- ---------------- -------
        31/05/2023 17:18:24           16384 Information      Successfully scheduled Software Protection service for re-start
        31/05/2023 17:17:53           16394 Information      Offline downlevel migration succeeded.
        ```
        
          
        
- **Structured Logs:** Following a strict and standardised format, these logs are conducive to parsing and analysis. Typical structured log formats include:
    
    - **Field Delimited Formats:** Comma-Separated Values (CSV) and Tab-Separated Values (TSV) are formats often used for tabular data.
        
        Example of a log file utilising CSV Format
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat log.csv
        "time","user","action","status","ip","uri"
        "2023-05-31T12:34:56Z","adversary","GET",200,"34.253.159.159","http://gitlab.swiftspend.finance:80/"
        ```
        
          
        
    - **JavaScript Object Notation (JSON):** Known for its readability and compatibility with modern programming languages.
        
        Example of a log file utilising the JSON Format
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat log.json
        {"time": "2023-05-31T12:34:56Z", "user": "adversary", "action": "GET", "status": 200, "ip": "34.253.159.159", "uri": "http://gitlab.swiftspend.finance:80/"}
        ```
        
          
        
    - **W3C Extended Log Format (ELF):** Defined by the World Wide Web Consortium (W3C), customizable for web server logging. It is typically used by Microsoft Internet Information Services (IIS) Web Server.
        
        Example of a log file utilising W3C Extended Log Format (ELF)
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat elf.log
        #Version: 1.0
        #Fields: date time c-ip c-username s-ip s-port cs-method cs-uri-stem sc-status
        31-May-2023 13:55:36 34.253.159.159 adversary 34.253.127.157 80 GET /explore 200
        ```
        
          
        
    - **eXtensible Markup Language (XML):** Flexible and customizable for creating standardized logging formats.
        
        Example of a log file utilising an XML Format
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat log.xml
        <log><time>2023-05-31T12:34:56Z</time><user>adversary</user><action>GET</action><status>200</status><ip>34.253.159.159</ip><url>https://gitlab.swiftspend.finance/</url></log>
        ```
        
          
        
- **Unstructured Logs:** Comprising free-form text, these logs can be rich in context but may pose challenges in systematic parsing. Examples include:
    
    - **NCSA Common Log Format (CLF):** A standardized web server log format for client requests. It is typically used by the Apache HTTP Server by default.
        
        Example of a log file utilising NCSA Common Log Format (CLF)
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat clf.log
        34.253.159.159 - adversary [31/May/2023:13:55:36 +0000] "GET /explore HTTP/1.1" 200 4886
        ```
        
          
        
    - **NCSA Combined Log Format (Combined):** An extension of CLF, adding fields like referrer and user agent. It is typically used by Nginx HTTP Server by default.
        
        Example of a log file utilising NCSA Combined Log Format (Combined)
        
        ```shell-session
        damianhall@WEBSRV-02:~/logs$ cat combined.log
        34.253.159.159 - adversary [31/May/2023:13:55:36 +0000] "GET /explore HTTP/1.1" 200 4886 "http://gitlab.swiftspend.finance/" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
        ```
        
          
        

**IMPORTANT:** Custom-defined formats can be crafted to meet specific applications or use cases. These formats provide flexibility but may necessitate specialised parsing tools for effective interpretation and analysis.

Log Standards

A log standard is a set of guidelines or specifications that define how logs should be generated, transmitted, and stored. Log standards may specify the use of particular log formats, but they also cover other aspects of logging, such as what events should be logged, how logs should be transmitted securely, and how long logs should be retained. Examples of log standards include:

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| - **[**Common Event Expression (CEE):**](https://cee.mitre.org/)** This standard, developed by MITRE, provides a common structure for log data, making it easier to generate, transmit, store, and analyse logs.<br>- **[OWASP Logging Cheat Sheet:](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)** A guide for developers on building application logging mechanisms, especially related to security logging.<br>- **[Syslog Protocol:](https://datatracker.ietf.org/doc/html/rfc5424)** Syslog is a standard for message logging, allowing separation of the software that generates messages from the system that stores them and the software that reports and analyses them.<br>- **[NIST Special Publication 800-92:](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-92.pdf)** This publication guides computer security log management.<br>- **[Azure Monitor Logs:](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/data-platform-logs)** Guidelines for log monitoring on Microsoft Azure.<br>- **[Google Cloud Logging:](https://cloud.google.com/logging/docs)** Guidelines for logging on the Google Cloud Platform (GCP).<br>- **[Oracle Cloud Infrastructure Logging:](https://docs.oracle.com/en-us/iaas/Content/Logging/Concepts/loggingoverview.htm)** Guidelines for logging on the Oracle Cloud Infrastructure (OCI).<br>- **[Virginia Tech - Standard for Information Technology Logging:](https://it.vt.edu/content/dam/it_vt_edu/policies/Standard_for_Information_Technology_Logging.pdf)** Sample log review and compliance guideline. |     |



---

## Related Notes
- [[Introduction to SIEM]]
- [[Splunk Basics]]
- [[Sysmon]]
- [[SOC L1 Alert Triage]]
- [[Introduction to EDR]]
