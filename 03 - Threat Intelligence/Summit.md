## Objective

After participating in one too many incident response activities, PicoSecure has decided to conduct a threat simulation and detection engineering engagement to bolster its malware detection capabilities. You have been assigned to work with an external penetration tester in an iterative purple-team scenario. The tester will be attempting to execute malware samples on a simulated internal user workstation. At the same time, you will need to configure PicoSecure's security tools to detect and prevent the malware from executing.

Following the **Pyramid of Pain's** ascending priority of indicators, your objective is to increase the simulated adversaries' cost of operations and chase them away for good. Each level of the pyramid allows you to detect and prevent various indicators of attack.

## Room Prerequisites

Completing the preceding rooms in the [Cyber Defence Frameworks module](https://tryhackme.com/module/cyber-defence-frameworks) will be beneficial before venturing into this challenge. Specifically, the following:

- [The Pyramid of Pain](https://tryhackme.com/room/pyramidofpainax)
- [MITRE](https://tryhackme.com/room/mitre)

## Machine Access

Please click **Start Machine** button below and give the machine two minutes to fully deploy the application.  Once deployed, navigate to the link [`https://LAB_WEB_URL.p.thmlabs.com`](https://lab_web_url.p.thmlabs.com/)


![[Pentest Introduction.png]]

![[sample1exe gen info.png]]

## General Info - sample1.exe

|                   |                                                                    |
| ----------------- | ------------------------------------------------------------------ |
| **File Name**     | `sample1.exe`                                                      |
| **File Size**     | 202.50 KB                                                          |
| **File Type**     | PE32+ executable (GUI) x86-64, for MS Windows                      |
| **Analysis Date** | September 5, 2023                                                  |
| **OS**            | Windows 10x64 v1803                                                |
| **Tags**          | Trojan.Metasploit.A                                                |
| **MIME**          | application/x-dosexec                                              |
| **MD5**           | `cbda8ae000aa9cbe7c8b982bae006c2a`                                 |
| **SHA1**          | `83d2791ca93e58688598485aa62597c0ebbf7610`                         |
| **SHA256**        | `9c550591a25c6228cb7d74d970d133d75c961ffed2ef7180144859cc09efca8c` |
## Hash Blocklist

Nice work! You prevented `sample1.exe` from executing by detecting its unique hash value. Check your [inbox](https://10-201-50-134.reverse-proxy-us-east-1.tryhackme.com/mail) for the next steps.


## General Info - sample2.exe

|   |   |
|---|---|
|**File Name**|`sample2.exe`|
|**File Size**|202.73 KB|
|**File Type**|PEXE - PE32+ executable (GUI) x86-64, for MS Windows|
|**Analysis Date**|September 5, 2023|
|**OS**|Windows 10x64 v1803|
|**Tags**|Trojan.Metasploit.A|
|**MIME**|application/x-dosexec|
|**MD5**|`4d661bf605d6b0b15915a533b572a6bd`|
|**SHA1**|`6878976974c27c8547cfc5acc90fb28ad2f0e975`|
|**SHA256**|`d576245e85e6b752b2fdffa43abaab1b2e1383556b0169fd04924d6cebc1cdf9`|

## Behaviour Analysis

### Malicious

METASPLOIT was detected
- sample2.exe (PID: 1927)

### Suspicious

Connects to unusual IP address
- sample2.exe (PID: 1927)

Connects to unusual port
- sample2.exe (PID: 1927)

### Info

Reads the machine GUID from the registry
- sample2.exe (PID: 1927)

The process checks LSA protection
- sample2.exe (PID: 1927)

Reads the computer name
- sample2.exe (PID: 1927)

Checks supported languages
- sample2.exe (PID: 1927)

## Network Activity

### HTTP(S) requests
1

### TCP/UDP connections
3

### DNS requests
0

### Threats

#### 0

## HTTP requests

|PID|Process|Method|IP|URL|
|---|---|---|---|---|
|1927|sample2.exe|GET|154.35.10.113:4444|http://154.35.10.113:4444/uvLk8YI32|

## Connections

| PID  | Process     | IP                 | Domain | ASN                       |
| ---- | ----------- | ------------------ | ------ | ------------------------- |
| 1927 | sample2.exe | 154.35.10.113:4444 | -      | Intrabuzz Hosting Limited |
| 1927 | sample2.exe | 40.97.128.3:443    | -      | Microsoft Corporation     |
| 1927 | sample2.exe | 40.97.128.4:443    | -      | Microsoft Corporation     |
## Active Rules

Nice work! The firewall rule prevented `sample2.exe` from connecting to the tester's command-and-control server. Check your [inbox](https://10-201-50-134.reverse-proxy-us-east-1.tryhackme.com/mail) for the next steps.

| Enabled | Type    | Source        | Destination   | Action | Settings |
| ------- | ------- | ------------- | ------------- | ------ | -------- |
| Yes     | Egress  | Any           | 154.35.10.113 | Deny   |          |
| Yes     | Egress  | 10.10.23.45   | 142.56.78.90  | Allow  |          |
| Yes     | Ingress | 88.90.123.45  | Any           | Deny   |          |
| Yes     | Ingress | 203.56.78.90  | Any           | Deny   |          |
| Yes     | Egress  | Any           | 205.78.90.12  | Allow  |          |
| Yes     | Ingress | 121.111.13.14 | Any           | Deny   |          |
| Yes     | Ingress | 187.123.45.67 | 10.10.32.45   | Allow  |          |
| Yes     | Ingress | 154.67.89.23  | 10.10.56.78   | Allow  |          |
| Yes     | Egress  | Any           | 95.123.45.67  | Deny   |          |
| Yes     | Egress  | 10.10.45.67   | 180.23.45.67  | Deny   |          |
## General Info - sample3.exe

|   |   |
|---|---|
|**File Name**|`sample3.exe`|
|**File Size**|207.12 KB|
|**File Type**|PEXE - PE32+ executable (GUI) x86-64, for MS Windows|
|**Analysis Date**|September 5, 2023|
|**OS**|Windows 10x64 v1803|
|**Tags**|Trojan.Metasploit.A|
|**MIME**|application/x-dosexec|
|**MD5**|`e31f0c62927d9d5a897b4c45e3c64dbc`|
|**SHA1**|`a92d3de6b1e3ab295f10587ca75f15318cb85a7b`|
|**SHA256**|`acb9b1260bcd08a465f9f300ac463b9b1215c097ebe44610359bb80881fe6a05`|

## Behaviour Analysis

### Malicious

METASPLOIT was detected

- sample3.exe (PID: 1021)

Downloads executable files from the Internet

- backdoor.exe (PID: 2712)

### Suspicious

Connects to unusual IP address

- sample3.exe (PID: 1021)

Connects to unusual port

- sample3.exe (PID: 1021)

### Info

Reads the machine GUID from the registry

- sample3.exe (PID: 1021)

The process checks LSA protection

- sample3.exe (PID: 1021)

Reads the computer name

- sample3.exe (PID: 1021)

Checks supported languages

- sample3.exe (PID: 1021)
## Network Activity

### HTTP(S) requests

#### 2

### TCP/UDP connections

#### 4

### DNS requests

#### 2

### Threats

#### 0

## HTTP requests

|PID|Process|Method|IP|URL|
|---|---|---|---|---|
|1021|sample3.exe|GET|62.123.140.9:1337|http://emudyn.bresonicz.info:1337/kzn293la|
|1021|sample3.exe|GET|62.123.140.9:80|http://emudyn.bresonicz.info/backdoor.exe|

## Connections

| PID  | Process      | IP                | Domain                 | ASN                     |
| ---- | ------------ | ----------------- | ---------------------- | ----------------------- |
| 1021 | sample3.exe  | 40.97.128.4:443   | services.microsoft.com | Microsoft Corporation   |
| 1021 | sample3.exe  | 62.123.140.9:1337 | emudyn.bresonicz.info  | XplorIta Cloud Services |
| 1021 | sample3.exe  | 62.123.140.9:80   | emudyn.bresonicz.info  | XplorIta Cloud Services |
| 2712 | backdoor.exe | 62.123.140.9:80   | emudyn.bresonicz.info  | XplorIta Cloud Services |

## DNS requests

| Domain                 | IP           |
| ---------------------- | ------------ |
| services.microsoft.com | 40.97.128.4  |
| emudyn.bresonicz.info  | 62.123.140.9 |

## Active Rules

Nice work! The DNS filter rule prevented `sample3.exe` from connecting to the tester's command-and-control server. Check your [inbox](https://10-201-50-134.reverse-proxy-us-east-1.tryhackme.com/mail) for the next steps.

|Rule Name|Category|Domain|Action|Settings|
|---|---|---|---|---|
|Suspicious Backdoor|Malware|emudyn.bresonicz.info|Deny||
|Cryptomining proxy server|Cryptomining|proxy4crypto.net|Deny||
|Gambling referral site|Gambling|luckylottoaffiliates.com|Deny||
|Anonymous browsing service|Anonymizer|cloakandbrowseanon.xyz|Deny||
|Conspiracy theorist cat blog|Other|catsknowthetruth.info|Allow||
|Suspicious file-sharing domain|Malware|downloadmyfilez.biz|Deny||
|C2 server associated subdomain|Botnet|commandn.ctrl.xyz|Deny||
|Fake software updates|Malware|legitsoft-updates.info|Deny||
|Bill's wedding invite (Allow)|Other|billrsvp.myweddings.io|Allow||
|Deny known phishing domain|Phishing|parrotp0st.thm|Deny||
|Ransomware associated domain|Malware|matrixlucky.sytes.net|Deny||
|No more cat videos|Other|youtube.com|Deny||
|Domain with Mirai association|Botnet|fungoods.xyz|Deny||****
## General Info - sample4.exe

|   |   |
|---|---|
|**File Name**|`sample4.exe`|
|**File Size**|219.46 KB|
|**File Type**|PEXE - PE32+ executable (GUI) x86-64, for MS Windows|
|**Analysis Date**|September 5, 2023|
|**OS**|Windows 10x64 v1803|
|**Tags**|None|
|**MIME**|application/x-dosexec|
|**MD5**|`5f29ff19d99fe244eaf5835ce01a4631`|
|**SHA1**|`cd12d2328f700ae1ba1296a5f011bfc5a49f456d`|
|**SHA256**|`a80cffb40cea83c1a20973a5b803828e67691f71f3c878edb5a139634d7dd422`|

## Behaviour Analysis

### Malicious

Disables Windows Defender Real-time monitoring

- sample4.exe (PID: 3806)

Downloads executable files from the Internet

- backdoor.exe (PID: 1367)

### Suspicious

Connects to unusual IP address

- sample4.exe (PID: 3806)

Connects to unusual port

- sample4.exe (PID: 3806)

Makes changes to the registry

- sample4.exe (PID: 3806)

### Info

Reads the machine GUID from the registry

- sample4.exe (PID: 3806)

The process checks LSA protection

- sample4.exe (PID: 3806)

Reads the computer name

- sample4.exe (PID: 3806)

Checks supported languages

- sample4.exe (PID: 3806)

## Network Activity

### HTTP(S) requests

#### 2

### TCP/UDP connections

#### 3

### DNS requests

#### 1

### Threats

#### 0

## HTTP requests

|PID|Process|Method|IP|URL|
|---|---|---|---|---|
|3806|sample4.exe|GET|102.23.20.118:1337|http://cranes0ft.iniware.xyz:1337/ab9z83ja|
|3806|sample4.exe|GET|102.23.20.118:80|http://cranes0ft.iniware.xyz/backdoor.exe|

## Connections

|PID|Process|IP|Domain|ASN|
|---|---|---|---|---|
|3806|sample4.exe|102.23.20.118:1337|cranes0ft.iniware.xyz|XplorIta Cloud Services|
|3806|sample4.exe|102.23.20.118:80|cranes0ft.iniware.xyz|XplorIta Cloud Services|
|1367|backdoor.exe|102.23.20.118:80|cranes0ft.iniware.xyz|XplorIta Cloud Services|

## DNS requests

|Domain|IP|
|---|---|
|cranes0ft.iniware.xyz|102.23.20.118|

## Registry Activity

### Total events

#### 3

### Read events

#### 1

### Write events

#### 2

### Delete events

#### 0

## Modification events

|                                        |                                                                                             |
| -------------------------------------- | ------------------------------------------------------------------------------------------- |
| **(PID) Process:** (3806) sample4.exe  | **Key:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection        |
| **Operation:** write                   | **Name:** DisableRealtimeMonitoring                                                         |
| **Value:** 1                           |                                                                                             |
| **(PID) Process:** (1928) explorer.exe | **Key:** HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced      |
| **Operation:** write                   | **Name:** EnableBalloonTips                                                                 |
| **Value:** 1                           |                                                                                             |
| **(PID) Process:** (9876) notepad.exe  | **Key:** HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.txt |
| **Operation:** read                    | **Name:** Progid                                                                            |
| **Value:** txtfile                     |                                                                                             |


##  Create Sigma Rule

### Step 1

I want to create a rule that focuses on:
Sysmon Event logs
- Sysmon is a Windows system service that monitors and logs various system activities
- it provides detailed information about command line activity, process creations, network connections, file creation and more
### Step 2: Sysmon Event Logs

I want to target this Sysmon event:
- Registry modifications
- detects changes to registry keys or values such as system settings, security policies, autorun entries, or access control configs
### Step 3: Registry Modifications

Set the rule conditions and options:

Registry Key:* HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection

Registry Name:* DisableRealtimeMonitoring

Value:* 1

ATT&CK ID: Defense Evasion (TA0005)

## General Info - sample5.exe

|   |   |
|---|---|
|**File Name**|`sample5.exe`|
|**File Size**|252.46 KB|
|**File Type**|PEXE - PE32+ executable (GUI) x86-64, for MS Windows|
|**Analysis Date**|September 5, 2023|
|**OS**|Windows 10x64 v1803|
|**Tags**|None|
|**MIME**|application/x-dosexec|
|**MD5**|`bece9deefe32e2179744d54e36277955`|
|**SHA1**|`4579aa086974b1db03d8df30d55570f2ab0990fa`|
|**SHA256**|`1fad9b93652f6498f7a4b91159a8c800e2639d035d8b3ddbbde72b762a443558`|

## Behaviour Analysis

### Malicious

Downloads executable files from the Internet

- beacon.bat (PID: 1702)

### Suspicious

Connects to unusual IP address

- sample5.exe (PID: 8374)

Connects to unusual port

- sample5.exe (PID: 8374)

High number of consequitive connections

- beacon.bat (PID: 1702)

### Info

Reads the machine GUID from the registry

- sample5.exe (PID: 8374)

The process checks LSA protection

- sample5.exe (PID: 8374)

Reads the computer name

- sample5.exe (PID: 8374)

Checks supported languages

- sample5.exe (PID: 8374)

## Network Activity

### HTTP(S) requests

#### 402

### TCP/UDP connections

#### 3

### DNS requests

#### 1

### Threats

#### 0

## HTTP requests

|PID|Process|Method|IP|URL|
|---|---|---|---|---|
|8374|sample5.exe|GET|51.102.10.19:1382|http://bababa10la.cn:1382/zz89j3uf|
|8374|sample5.exe|GET|51.102.10.19:443|https://bababa10la.cn/beacon.bat|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|1702|beacon.bat|POST|51.102.10.19:443|https://bababa10la.cn/keep-alive?hostname=WK102|
|-|Too many results to display|-|-|-|

## Connections

| PID  | Process     | IP                | Domain        | ASN                     |
| ---- | ----------- | ----------------- | ------------- | ----------------------- |
| 8374 | sample5.exe | 51.102.10.19:1382 | bababa10la.cn | XplorIta Cloud Services |
| 8374 | sample5.exe | 51.102.10.19:80   | bababa10la.cn | XplorIta Cloud Services |
| 1702 | beacon.bat  | 51.102.10.19:443  | bababa10la.cn | XplorIta Cloud Services |

## DNS requests

| Domain        | IP           |
| ------------- | ------------ |
| bababa10la.cn | 51.102.10.19 |
Outgoin_connections.log

2023-08-15 09:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 09:23:45 | Source: 10.10.15.12 | Destination: 43.10.65.115 | Port: 443 | Size: 21541 bytes
2023-08-15 09:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:14:21 | Source: 10.10.15.12 | Destination: 87.32.56.124 | Port: 80  | Size: 1204 bytes
2023-08-15 10:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 11:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 11:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 11:45:09 | Source: 10.10.15.12 | Destination: 145.78.90.33 | Port: 443 | Size: 805 bytes
2023-08-15 12:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 12:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 13:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 13:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 13:32:17 | Source: 10.10.15.12 | Destination: 72.15.61.98  | Port: 443 | Size: 26084 bytes
2023-08-15 14:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 14:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 14:55:33 | Source: 10.10.15.12 | Destination: 208.45.72.16 | Port: 443 | Size: 45091 bytes
2023-08-15 15:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 15:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 15:40:10 | Source: 10.10.15.12 | Destination: 101.55.20.79 | Port: 443 | Size: 95021 bytes
2023-08-15 16:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 16:18:55 | Source: 10.10.15.12 | Destination: 194.92.18.10 | Port: 80  | Size: 8004 bytes
2023-08-15 16:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 17:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 17:09:30 | Source: 10.10.15.12 | Destination: 77.23.66.214 | Port: 443 | Size: 9584 bytes
2023-08-15 17:27:42 | Source: 10.10.15.12 | Destination: 156.29.88.77 | Port: 443 | Size: 10293 bytes
2023-08-15 17:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 18:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 18:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 19:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 19:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 20:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 20:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 21:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes



##  Create Sigma Rule

### Step 1

I want to create a rule that focuses on:
Sysmon Event Logs
### Step 2: Sysmon Event Logs

I want to target this Sysmon event:
Network Connections
### Step 3: Network Connections

Set the rule conditions and options:

This rule will detect network connections made from a host machine with specific conditions, such as remote IP, port, size of the connection, and how often it occurs (frequency).

Remote IP:* Any

Remote Port:* Any

Size (bytes):* 97

Frequency (seconds):* 1800

ATT&CK ID:* (TA0009)Command and Control


We identified a consistent Command and Control (C2) beacon pattern originating from host 10.10.15.12. The beacon transmitted 97-byte packets to a remote server every 1800 seconds (30 minutes) over port 443. This recurring network behavior was captured using Sysmon Event ID 3 (NetworkConnect). 

To detect this, we created a Sigma rule that triggers on repeated outbound connections matching this packet size and frequency, mapped to MITRE ATT&CK Command and Control (TA0011). This behavioral detection is resilient to hash and filename changes, effectively disrupting the adversary's operational capability.

## General Info - sample6.exe

|   |   |
|---|---|
|**File Name**|`sample6.exe`|
|**File Size**|341.02 KB|
|**File Type**|PEXE - PE32+ executable (GUI) x86-64, for MS Windows|
|**Analysis Date**|September 5, 2023|
|**OS**|Windows 10x64 v1803|
|**Tags**|None|
|**MIME**|application/x-dosexec|
|**MD5**|`fc20dd3e92d637cac866c00f26eeb28b`|
|**SHA1**|`034c1d75939cf9f4eecd91b86f21aad36d9063d9`|
|**SHA256**|`853a41260626117512efaae7553514b5f96c43ca17440e3f9f2e83ab92463d1a`|

## Behaviour Analysis

### Malicious

Downloads executable files from the Internet

- sample6.exe (PID: 8374)

### Suspicious

Connects to unusual IP address

- sample6.exe (PID: 8374)

Connects to unusual port

- sample6.exe (PID: 8374)

### Info

Reads the machine GUID from the registry

- sample6.exe (PID: 8374)

The process checks LSA protection

- sample6.exe (PID: 8374)

Reads the computer name

- sample6.exe (PID: 8374)

Checks supported languages

- sample6.exe (PID: 8374)

## Network Activity

### HTTP(S) requests

#### 2

### TCP/UDP connections

#### 3

### DNS requests

#### 1

### Threats

#### 0

## HTTP requests

|PID|Process|Method|IP|URL|
|---|---|---|---|---|
|8374|sample6.exe|GET|182.44.41.12:1499|http://contr0l2hax.info:1499/kwsx92la|
|8374|sample6.exe|GET|182.44.41.12:443|https://contr0l2hax.info/sample6.exe|

## Connections

|PID|Process|IP|Domain|ASN|
|---|---|---|---|---|
|8374|sample6.exe|182.44.41.12:1499|contr0l2hax.info|XplorIta Cloud Services|
|8374|sample6.exe|182.44.41.12:80|contr0l2hax.info|XplorIta Cloud Services|
|3322|sample6.exe|182.44.41.12:443|contr0l2hax.info|XplorIta Cloud Services|

## DNS requests

|Domain|IP|
|---|---|
|contr0l2hax.info|182.44.41.12|

## Processes

### Total processes

#### 4

### Monitored processes

#### 0

### Malicious processes

#### 1

### Suspicious processes

#### 0

## Process information

|PID|CMD|Path|Parent|
|---|---|---|---|
|8374|sample6.exe|C:\Users\admin\AppData\Local\Temp\sample6.exe|explorer.exe|
|3992|cmd.exe|C:\Windows\system32\cmd.exe|sample6.exe|
|1432|cmd.exe|C:\Windows\system32\cmd.exe|sample6.exe|
|2312|cmd.exe|C:\Windows\system32\cmd.exe|sample6.exe|

## Files Activity

### Executable files

#### 0

### Suspicious files

#### 1

### Text files

#### 1

### Unknown types

#### 0

## Dropped files

| PID  | Process | Filename            | Type |
| ---- | ------- | ------------------- | ---- |
| 2312 | cmd.exe | %temp%\exfiltr8.log | text |
##  Create Sigma Rule

### Step 1

I want to create a rule that focuses on:
Sysmon EventLogs
### Step 2: Sysmon Event Logs

I want to target this Sysmon event:
Process Creation
### Step 3: Process Creation

Set the rule conditions and options:

This rule will detect the contents of the command line when a specific process is used to execute commands.

Process Name:* cmd.exe

CommandLine :Contains

String:* exfiltr8.log

ATT&CK ID: Collection (TA0009)
# Quick highlights (big wins)

- You progressed from hash-based detection → network blocking → behavioral/TTP detection (the Pyramid of Pain progression).
    
- Built and validated a **Sysmon-based Sigma rule** that detects a **30-minute, 97-byte HTTPS C2 beacon** (EventID 3 + frequency = 1800s). That’s a behavioral detection that’s hard for attackers to evade.
    
- Detected and blocked multiple staged downloaders and backdoors (samples 1 → 6) and the attacker’s automated collection (`exfiltr8.log`).
    

---

# Per-sample summary & key IOCs

**sample1.exe**

- Tags: Trojan.Metasploit.A
    
- SHA256: `9c5505...efca8c` (full hash earlier)
    
- Behaviors: Metasploit detected; reads Machine GUID; checks LSA protection; connects to unusual port.
    
- Action: Add SHA256 to Manage Hashes; create Sysmon/EDR detection on process creation + registry read + network connect.
    

**sample2.exe**

- SHA256: `d576245e...1cdf9`
    
- IOCs: Connects to `154.35.10.113:4444` (HTTP GET `/uvLk8YI32`)
    
- Action: Firewall egress block to `154.35.10.113:4444`; Suricata rule on GET path; Sigma rule for hash + network.
    

**sample3.exe**

- SHA256: `acb9b126...6a05`
    
- Behavior: Downloader that fetched `backdoor.exe` from `emudyn.bresonicz.info` (`62.123.140.9`) on ports 1337 & 80; spawned backdoor (PID 2712).
    
- Action: Block domain/IP, sinkhole DNS, create Sigma correlation rule: download then spawn.
    

**sample4.exe**

- SHA256: `a80cffb4...d422`
    
- Behavior: Disables Windows Defender realtime (`HKLM\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection\DisableRealtimeMonitoring = 1`), downloads `backdoor.exe` from `cranes0ft.iniware.xyz` (`102.23.20.118`), modifies registry.
    
- Action: Sigma rule on Sysmon EventID 13 registry write + network, Sysmon config to log RegistryEvent, PowerShell remediation to re-enable Defender.
    

**sample5.exe**

- SHA256: `1fad9b93...43558`
    
- Behavior: Downloads `beacon.bat`; `beacon.bat` posts keep-alives to `bababa10la.cn` (`51.102.10.19`) with high-frequency POSTs (`/keep-alive?hostname=WK102`) and also GETs to `/zz89j3uf`.
    
- Action: DNS sinkhole `bababa10la.cn`; firewall block `51.102.10.19` on ports 80/1382/443; built a Sysmon/Network frequency-based Sigma rule (event 3, 97 bytes, frequency corrected later).
    

**sample6.exe**

- Behavior: Downloads from `contr0l2hax.info` (`182.44.41.12`), spawns several `cmd.exe` which append discovery outputs into `%temp%\exfiltr8.log`.
    
- IOCs: GET `/kwsx92la`, GET `/sample6.exe`; dropped `%temp%\exfiltr8.log`.
    
- Action: Block domain/IP, Sigma rule for process creation detecting `cmd.exe` with commandline containing `exfiltr8.log`, harvest exfiltr8.log for flags.
    

---

# Exact rules / signatures you created (paste-ready essence)

## Sigma – Beacon (Sysmon EventID 3)

- Log source: Sysmon (Microsoft-Windows-Sysmon/Operational)
    
- EventID: `3` (NetworkConnect)
    
- DestinationPort: `443`
    
- Size (bytes): `97`
    
- Frequency (seconds): `1800`
    
- ATT&CK tactic: **Command and Control (TA0011)** (sub-technique: `T1071.001` noted in description)
    

## Sigma – exfil staging (Sysmon EventID 1)

- EventID: `1` (ProcessCreate)
    
- Image endswith: `\cmd.exe`
    
- CommandLine contains: `exfiltr8.log`
    
- ATT&CK tactic: **Collection (TA0009)** (Technique: `T1119`)
    

## Sigma – Defender disable (Sysmon EventID 13)

- EventID: `13` (RegistryEvent)
    
- TargetObject contains: `SOFTWARE\Microsoft\Windows Defender\Real-Time Protection`
    
- Details contains: `DisableRealtimeMonitoring`, `Value: 1`
    
- ATT&CK tactic: **Defense Evasion (T1562.001)**
    

## Network IDS examples (Suricata/Snort)

- Alert on HTTP GET/POST to known C2 IPs and paths (examples used):
    
    - `alert tcp any any -> 154.35.10.113 4444 (content:"GET /uvLk8YI32";)`
        
    - `alert tcp any any -> 51.102.10.19 443 (content:"POST /keep-alive?hostname=";)`
        
    - Generic large transfer alert: `dsize:>10240`
        

## YARA templates

- Use SHA256 and stable strings like domain names or unique URIs (`/backdoor.exe`, `/uvLk8YI32`, `uvLk8YI32`, `kzn293la`, etc.) — included examples earlier.
    

---

# Useful commands & tools you used / practiced

- Hash verifications:
    
    - PowerShell: `Get-FileHash .\sample1.exe -Algorithm SHA256`
        
    - Fallback: `certutil -hashfile sample1.exe SHA256`
        
- Extract strings:
    
    - Sysinternals `strings.exe -n 6 sample1.exe > sample1_strings.txt`
        
    - PowerShell fallback: read bytes & regex to extract printable sequences
        
- PE imports: `dumpbin /imports` (if available) or `objdump -x`
    
- Network inspection: `curl -Ik`, PCAP follow-stream in Wireshark
    
- Windows triage:
    
    - `netstat -ano`
        
    - `tasklist`, `Get-Process`, `Get-ScheduledTask`
        
    - Read registry: `Get-ItemProperty HKLM:\SOFTWARE\...`
        
    - Re-enable Defender: `Set-MpPreference -DisableRealtimeMonitoring $false`
        
- Log queries (examples for Splunk/Elastic/KQL) provided for hunts.
    

---

# Hunting & triage playbook (condensed)

1. **Identify**: Hash, domain, IP, process names, file paths.
    
2. **Contain**: Quarantine host, Firewall egress block, DNS sinkhole.
    
3. **Collect**: PCAP, `%temp%\exfiltr8.log`, Sysmon logs (EventID 1/3/13), memory snapshot, process trees.
    
4. **Analyze**: Inspect HTTP responses (flag likely in response or in `exfiltr8.log`), strings, YARA matches.
    
5. **Remediate**: Kill processes, remove files, remove persistence, re-enable Defender or re-image if necessary. Rotate credentials if host had sensitive access.
    
6. **Hunt**: Use Sigma/Splunk/Elastic saved searches to find other infected hosts and scan for same behaviors.
    
7. **Document**: Save evidence and update detection rule notes with MITRE references.
    

---

# MITRE mapping & Purple-team lesson

- You mapped detections to appropriate ATT&CK tactics: **Collection (TA0009)** for exfil staging, **Command & Control (TA0011)** for beaconing, **Defense Evasion** for Defender disabling.
    
- You moved detection focus from **Indicators (hashes)** → **Network IOCs (IPs/domains)** → **TTPs/behaviors** (registry writes, frequent small POSTs, automated collection). That’s the core purple-team win — raising adversary cost.
    

---

# Where flags were likely to be found in this lab

- In sandbox **HTTP response bodies** to GET requests (e.g., `/kzn293la`, `/zz89j3uf`, etc.)
    
- In **downloaded files** (backdoor.exe strings or file content)
    
- In staged file **%temp%\exfiltr8.log** (the aggregated output), which the attacker created repeatedly — you viewed and extracted it.
    

---

# Final recommendations / next steps (immediate & medium-term)

- Deploy the Sigma rules to production SIEM/EDR with tuned thresholds and allowlists for known management traffic.
    
- Enable Sysmon across endpoints (EventIDs 1,3,13 at minimum) with centralized logging.
    
- Deploy YARA rules to file-scanning sandboxes and AV/EDR where supported.
    
- Build automated containment playbooks: quarantine host, block domain/IP on firewall, collect artifacts automatically.
    
- Run an estate-wide hunt using the beacon frequency detection and `exfiltr8.log` rule to find any missed compromises.

    timeframe: 1800s
    groupby: [SourceIp, DestinationIp]
    min_count: 2
  condition: selection | groupby(SourceIp, DestinationIp) having count >= 2
level: high
fields:
  - SourceIp
  - DestinationIp
  - DestinationPort
  - DataLength
falsepositives:
  - Legitimate monitoring/management agents that poll external services; validate SourceIp and process associated.
Notes: If your platform does not expose DataLength under that name, replace with the equivalent (e.g., Bytes, dsize, Size). Use aggregation to detect >1 occurrence within 1800s (30 minutes). Adjust min_count to match your environment.

B) Exfil Staging Detection — ProcessCreate (Sysmon EventID 1)
yaml
Copy code
title: Automated collection to exfiltr8.log via cmd.exe
id: a7b2c3d4-pico-exfil-staging
status: experimental
description: Detects cmd.exe processes writing enumeration output to exfiltr8.log under %temp% (automated collection prior to exfiltration). MITRE: Collection (TA0009) - T1119.
author: PicoSecure Analyst
logsource:
  product: windows
  service: sysmon
detection:
  selection:
    EventID: 1
    Image|endswith: '\cmd.exe'
    CommandLine|contains: 'exfiltr8.log'
  condition: selection
level: high
fields:
  - Image
  - CommandLine
  - ProcessId
  - ParentImage
falsepositives:
  - Legit admin scripts writing logs; check ParentImage and initiating user context before remediation.
response:
  - Collect %temp%\exfiltr8.log; capture PCAP and process tree for the ProcessGuid; quarantine host if malicious.
C) Defender Disable Detection — RegistryEvent (Sysmon EventID 13)
yaml
Copy code
title: Disable Windows Defender real-time monitoring via registry write
id: d3e4f5a6-pico-disable-defender
status: experimental
description: Detects registry write modifying Defender Real-Time Protection DisableRealtimeMonitoring value to 1. Sysmon EventID 13 (RegistryEvent). MITRE: Defense Evasion - Disable or Modify Tools (T1562.001).
author: PicoSecure Analyst
logsource:
  product: windows
  service: sysmon
detection:
  selection:
    EventID: 13
    TargetObject|contains: 'SOFTWARE\\Microsoft\\Windows Defender\\Real-Time Protection'
    Details|contains: 'DisableRealtimeMonitoring'
  condition: selection and (Details|contains: 'Value: 1' or Details|contains: '0x1' or Details|contains: 'REG_DWORD')
level: high
fields:
  - Image
  - TargetObject
  - Details
falsepositives:
  - Admin intentionally modifying Defender settings via sanctioned tools; validate user/process.
response:
  - Quarantine host, collect registry hive and process info, re-enable Defender and investigate source process.
Import / mapping tips
Sysmon field names differ by ingestion: TargetObject / Details / Image may be named registry.key_path, registry.value.data, process.executable in your SIEM. If no matches, run a broad search for EventID with the key string and inspect actual field names for tuning.

For the Beacon rule, if your logs don’t provide DataLength, create the rule by DestinationPort: 443 + aggregator on small Bytes sized events (<= 100) with periodicity 1800s.
---

## Related Notes
- [[Pyramid of Pain]]
- [[Sysmon]]
- [[Intro to Cyber Threat Intel]]
- [[YARA]]
- [[Malware Classification]]
