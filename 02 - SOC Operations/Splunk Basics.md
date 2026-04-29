Splunk is one of the leading SIEM solutions in the market. It allows users to collect, analyze, and correlate network and machine logs in real time. In this room, we will explore the basics of Splunk and its functionalities, and how it provides better visibility of network activities and helps speed up detection.

## Learning Objectives

This room covers the following learning objectives:

- Understanding the components of Splunk
- Exploring some available options in Splunk
- Understanding log ingestion in Splunk
- Practically ingesting some Logs in Splunk and analyzing them

## Room Prerequisites

If you are new to SIEM, please complete the [Introduction to SIEM](https://tryhackme.com/jr/introtosiem) room.

## Splunk Forwarder

Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored, and its main task is to collect the data and send it to the Splunk instance. It does not affect the endpoint's performance as it takes a few resources to process. Some of the key data sources are:

- Web server generating web traffic.
- Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
- Linux host generating host-centric logs.
- Database generating DB connection requests, responses, and errors.

![Splunk Forwarder](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/2369fa2efc856b793f1ecbf415681d4d.png)

The forwarder collects the data from the log sources and sends it to the Splunk Indexer. 

## Splunk Indexer

Splunk Indexer plays the main role in processing the data it receives from forwarders. It parses and normalizes the data into field-value pairs, categorizes it, and stores the results as events, making the processed data easy to search and analyze.

![Splunk Indexer](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/e699eaa9af523513e9c6a6ab8aaaa6a2.png)

Now, the data, which is normalized and stored by the indexer, can be searched by the Search Head, as explained below.

## Search Head

Splunk Search Head is the place within the **Search & Reporting App** where users can search the indexed logs, as shown below. The searches are done using the **SPL** (Search Processing Language), a powerful query language for searching indexed data. When the user performs a search, the request is sent to the indexer, and the relevant events are returned as field-value pairs.

![Image showing Splunk Search Head](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/0f7738f88ca807d1edf2ac7d84f6951c.png)

The Search Head also allows you to transform results into presentable tables and visualizations such as pie, bar, and column charts, as shown below:

![Image showing the Visualization tab](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/ce38f9780efac6e22af23c2574367255.png)


Splunk can ingest any data. According to the Splunk documentation, when data is added to Splunk, the data is processed and transformed into a series of individual events. The data sources can be event logs, website logs, firewall logs, etc. The data sources are grouped into categories.

 Below is a chart listing from the Splunk documentation detailing each data source category.

![Data sources supported by Splunk](https://assets.tryhackme.com/additional/splunk-overview/splunk-data-sources.png)

In this task, we're going to focus on **VPN logs**. We're presented with the following screen when we click on the `Add Data` link on the Splunk home screen.

![Data sources Option](https://assets.tryhackme.com/additional/splunk-overview/splunk-add-data.png)

We will use the `Upload` Option to upload the data from our local machine.

## Practical

Download the log file `VPN_logs` from the `Download Task Files` button below and upload it to the Splunk instance we started in Task #2. If you are using the AttackBox, the log file is available in the `/root/Rooms/SplunkBasic/` directory.

Download Task Files

To upload the data successfully, you must follow five steps, which are explained below:

1. **Select Source:** Choose the Log file and the data source.
2. **Select Source Type:** Select what type of logs are being ingested, e.g, JSON, syslog.
3. **Input Settings:** Select the index where these logs will be dumped and the HOSTNAME to be associated with the logs.
4. **Review:** Review all the configurations.
5. **Done:** Complete the upload. Your data will be uploaded successfully and ready to be analyzed.

![Data Ingestion Example](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/c36a6f1c70007602251f331aee914d5c.gif)


Well done! In this room, you learned about Splunk's core components, explored the Splunk interface, and practiced uploading data to Splunk. You have gained the foundational knowledge of Splunk SIEM.

If you'd like to dig deeper, you can explore the following Splunk walkthrough and challenge rooms to understand how Splunk is effectively used in investigating incidents.

- [Splunk: Exploring SPL](https://tryhackme.com/room/splunkexploringspl)
- [Incident Handling with Splunk](https://tryhackme.com/room/splunk201)
- [Investigating With Splunk](http://tryhackme.com/jr/investigatingwithsplunk)
- [Benign - Challenge](http://tryhackme.com/jr/benign)
- [PoshEclipse - Challenge](http://tryhackme.com/jr/posheclipse)
---

## 🧠 Splunk Basics (TryHackMe VPN Logs Lab)

### 🏁 Setup

- Connect to **TryHackMe VPN** with OpenVPN.
    
- Verify the target is reachable:
    
    `ping <MACHINE_IP> Test-NetConnection -ComputerName <MACHINE_IP> -Port 80`
    
- Access Splunk Web:  
    `http://<MACHINE_IP>`  
    (Use `admin / changeme` if prompted for credentials.)
    

---

## 🔍 Searching Logs in Splunk

**Default Search Format:**

`index="<index_name>" sourcetype="<sourcetype>"`

Example (VPN logs):

`index="vpn_logs" sourcetype="_json"`

**To include specific filters:**

`source="VPN_logs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json"`

---

## 📊 Event Counting and Filtering

### 1️⃣ Count All Events

`index="vpn_logs" sourcetype="_json" | stats count AS "Total Events"`

→ Returns total number of log events (e.g., `2,812`).

---

### 2️⃣ Count Events for a Specific User

`index="vpn_logs" sourcetype="_json" UserName="Maleena" | stats count AS "Maleena Event Count"`

→ Shows total events tied to user _Maleena_.

---

### 3️⃣ Identify Username by IP

`index="vpn_logs" sourcetype="_json" Source_ip="107.14.182.38" | stats values(UserName) AS "Associated Username"`

→ Displays the username(s) linked to IP `107.14.182.38`.

---

### 4️⃣ Count Events Excluding a Country

`index="vpn_logs" sourcetype="_json" NOT Source_Country="France" | stats count AS "Events (Non-France)"`

→ Returns the total number of events from all countries _except France_.

---

### 5️⃣ Break Down Counts by Field

**By action:**

`index="vpn_logs" sourcetype="_json" | stats count BY action`

**By country:**

`index="vpn_logs" sourcetype="_json" | stats count BY Source_Country`

**By user:**

`index="vpn_logs" sourcetype="_json" | stats count BY UserName`

---

## 📈 Visualization Tips

Once your query runs:

- Click **Visualization** tab → choose **Bar**, **Pie**, or **Timechart**.
    
- For trends over time:
    
    `index="vpn_logs" sourcetype="_json" | timechart span=1h count BY action`
    

---

## 🧩 General Notes

- `index` = data repository
    
- `sourcetype` = log format definition
    
- `source` = actual file or input
    
- `host` = machine that sent the logs
    
- `stats` = aggregation command (like SQL `COUNT`, `GROUP BY`)
    
- `timechart` = visualize data over time
    
- Always verify your **time range** (top right → “All time”) if events seem missing.
---

## Related Notes
- [[Introduction to SIEM]]
- [[SOC Fundamentals]]
- [[Intro to Logs]]
- [[MITRE]]
- [[Anomaly Grid]]
