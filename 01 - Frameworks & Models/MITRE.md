For those that are new to the cybersecurity field, you probably never heard of MITRE. Those of us that have been around _might_ only associate MITRE with CVEs ( [**Common Vulnerabilities and Exposures**](https://cve.mitre.org/) ) list, which is one resource you'll probably check when searching for an exploit for a given vulnerability. But MITRE researches in many areas, outside of cybersecurity, for the 'safety, stability, and well-being of our nation.'  These areas include artificial intelligence, health informatics, space security, to name a few.

From [**Mitre.org**](https://www.mitre.org/about/corporate-overview) : " _At MITRE, we solve problems for a safer world. Through our federally funded R&D centers and public-private partnerships, we work across government to tackle challenges to the safety, stability, and well-being of our nation._ "

In this room, we will focus on other projects/research that the US-based non-profit MITRE Corporation has created for the cybersecurity community, specifically:

- ATT&CK _®_  ( A dversarial  T actics,  T echniques,  and   C ommon  K nowledge) Framework
- CAR ( C yber  A nalytics  R epository) Knowledge Base
- ENGAGE  (sorry, not a fancy acronym)
- D3FEND ( D etection,  D enial, and  D isruption  F ramework  E mpowering  N etwork  D efense)
- AEP ( A TT&CK  E mulation  P lans)

Before diving in, let's briefly discuss a few terms that you will often hear when dealing with the framework, threat intelligence, etc.

APT   is an acronym for  Advanced Persistent Threat .  This can be considered a team/group ( **_threat group_** ), or even country ( **_nation-state group_** ), that engages in long-term attacks against organizations and/or countries. The term 'advanced' can be misleading as it will tend to cause us to believe that each APT group all have some super-weapon, e.i. a zero-day exploit, that they use. That is not the case. As we will see a bit later, the techniques these APT groups use are quite common and can be detected with the right implementations in place. You can view FireEye's current list of APT groups [**here**](https://www.fireeye.com/current-threats/apt-groups.html) .  

TTP is an acronym for  Tactics, Techniques, and Procedures,  but what does each of these terms mean?

- The  Tactic  is the adversary's goal or objective.
- The  Technique  is how the adversary achieves the goal or objective.
- The  Procedure  is how the technique is executed.



ATT&CK Framework

What is the ATT&CK® framework? According to the  [website](https://attack.mitre.org/) , "MITRE ATT&CK® is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations." In 2013, MITRE began to address the need to record and document common TTPs ( Tactics, Techniques, and Procedures ) that APT ( Advanced Persistent Threat ) groups used against enterprise Windows networks. This started with an internal project known as FMX ( Fort Meade Experiment ). Within this project, selected security professionals were tasked to emulated adversarial TTPs against a network, and data was collected from the attacks on this network. The gathered data helped construct the beginning pieces of what we know today as the ATT&CK® framework.

The ATT&CK® framework has grown and expanded throughout the years. One notable expansion was that the framework focused solely on the Windows platform but has expanded to cover other platforms, such as macOS and Linux. The framework is heavily contributed to by many sources, such as security researchers and threat intelligence reports. Note this is not only a tool for blue teamers. The tool is also useful for **red teamers** .

If you haven't done so, navigate to the ATT&CK®  [website](https://attack.mitre.org/) .

Direct your attention to the bottom of the page to view the  ATT&CK® Matrix for Enterprise . Across the top of the matrix, there are 14 categories. Each category contains the techniques an adversary could use to perform the tactic. The categories cover the seven-stage Cyber Attack Lifecycle (credit Lockheed Martin for the Cyber Kill Chain).

![](https://assets.tryhackme.com/additional/mitrev2/t3-attackv11.png)

(ATT&CK Matrix v11.2)

Under  Initial Access , there are 9 techniques. Some of the techniques have sub-techniques, such as Phishing. 

![](https://assets.tryhackme.com/additional/mitre/attack2.png)

If we click on the gray bar to the right, a new layer appears listing the sub-techniques. 

![](https://assets.tryhackme.com/additional/mitre/attack3.png)

To get a better understanding of this technique and it's associated sub-techniques, click on Phishing.

We have been directed to a page dedicated to the technique known as Phishing and all related information regarding the technique, such as a brief description,  Procedure Examples , and  Mitigations . 

![](https://assets.tryhackme.com/additional/mitre/attack4.png)

You can alternatively resort to using the Search feature to retrieve all associated information regarding a given technique, sub-technique, and/or group. 

![](https://assets.tryhackme.com/additional/mitre/attack5.png)

Lastly, the same data can be viewed via the  MITRE ATT&CK® Navigator : " _The ATT&CK® Navigator is designed to provide basic navigation and annotation of ATT&CK® matrices, something that people are already doing today in tools like Excel. We've designed it to be simple and generic - you can use the Navigator to visualize your defensive coverage, your red/blue team planning, the frequency of detected techniques, or anything else you want to do_ ."

You can access the Navigator view when visiting a group or tool page. The ATT&CK® Navigator Layers button will be available.

![](https://assets.tryhackme.com/additional/mitre/attack8.png)

In the sub-menu select  view .

![](https://assets.tryhackme.com/additional/mitrev2/t3-attack-navigator.png)

Let's get acquainted with this tool. Click  [here](https://mitre-attack.github.io/attack-navigator//#layerURL=https%3A%2F%2Fattack.mitre.org%2Fgroups%2FG0008%2FG0008-enterprise-layer.json)  to view the ATT&CK® Navigator for Carbanak. 

At the top left, there are 3 sets of controls:  selection controls ,  layer controls , and  technique controls . I encourage you to inspect each of the options under each control to get familiar with them. The question mark at the far right will provide additional information regarding the navigator. 

![](https://assets.tryhackme.com/additional/mitrev2/t3-attack-navigator2.png)

To summarize, we can use the ATT&CK Matrix to map a threat group to their tactics and techniques.  There are various methods the search can be initiated. 

The questions below will help you become more familiar with the ATT&CK®.  It is recommended to start answering the questions from the  [Phishing page](https://attack.mitre.org/techniques/T1566/) . Note, that this link is for version 8 of the  ATT&CK Matrix.

[Cyber Analytics Repository](https://car.mitre.org/)

The official definition of  CAR  is " _The MITRE Cyber Analytics Repository (CAR) is a knowledge base of analytics developed by MITRE based on the MITRE ATT&CK_ ®  _adversary model. CAR defines a data model that is leveraged in its pseudocode representations but also includes implementations directly targeted at specific tools (e.g., Splunk, EQL) in its analytics. With respect to coverage, CAR is focused on providing a set of validated and well-explained analytics, in particular with regards to their operating theory and rationale._ "

Instead of further attempting to explain what CAR is, let's dive in. With our newly acquired knowledge from the previous section, we should feel comfortable and understand the information that CAR is providing to us.

Let's begin our journey by reviewing  [CAR-2020-09-001: Scheduled Task - File Access](https://car.mitre.org/analytics/CAR-2020-09-001/) .

Upon visiting the page, we're given a brief description of the analytics and references to ATT&CK ( technique ,  sub-technique , and  tactic ).

[Cyber Analytics Repository](https://car.mitre.org/)

The official definition of  CAR  is " _The MITRE Cyber Analytics Repository (CAR) is a knowledge base of analytics developed by MITRE based on the MITRE ATT&CK_ ®  _adversary model. CAR defines a data model that is leveraged in its pseudocode representations but also includes implementations directly targeted at specific tools (e.g., Splunk, EQL) in its analytics. With respect to coverage, CAR is focused on providing a set of validated and well-explained analytics, in particular with regards to their operating theory and rationale._ "

Instead of further attempting to explain what CAR is, let's dive in. With our newly acquired knowledge from the previous section, we should feel comfortable and understand the information that CAR is providing to us.

Let's begin our journey by reviewing  [CAR-2020-09-001: Scheduled Task - File Access](https://car.mitre.org/analytics/CAR-2020-09-001/) .

Upon visiting the page, we're given a brief description of the analytics and references to ATT&CK ( technique ,  sub-technique , and  tactic ).

![[splunksearch.png]]

Full Analytic List
In the Full Analytic List view, we can see what implementations are available for any given analytic at a single glance, along with what OS platform it applies to.

CAR ATTACK Navigator

![[car attack navigator.png]]


Let's look at another analytic to see a different implementation,  [CAR-2014-11-004: Remote PowerShell Sessions](https://car.mitre.org/analytics/CAR-2014-11-004/) .

Under Implementations, a pseudocode is provided and an EQL version of the pseudocode. EQL (pronounced as 'equal'), and it's an acronym for Event Query Language. EQL can be utilized to query, parse, and organize Sysmon event data. You can read more about this  [here](https://eql.readthedocs.io/en/latest/) .

![[EQL.png]]

MITRE ENGAGE

Per the website, " _MITRE Engage  is a framework for planning and discussing adversary engagement operations that empowers you to engage your adversaries and achieve your cybersecurity goals._ "

MITRE Engage is considered an  Adversary Engagement Approach . This is accomplished by the implementation of  Cyber Denial  and  Cyber Deception . 

With  Cyber Denial  we prevent the adversary's ability to conduct their operations and with  Cyber Deception  we intentionally plant artifacts to mislead the adversary. 

The Engage website provides a  [starter kit](https://engage.mitre.org/starter-kit/)  to get you 'started' with the Adversary Engagement Approach. The starter kit is a collection of whitepapers and PDFs explaining various checklists,  methodologies, and  processes  to get you started. 

As with MITRE ATT&CK, Engage has its own matrix.  Below is a visual of the  Engage Matrix .

![[engage-matrix table.png]]

Let's quickly explain each of these categories based on the information on the Engage website.

- Prepare  the set of operational actions that will lead to your desired outcome (input)
- Expose  adversaries when they trigger your deployed deception activities 
- Affect  adversaries by performing actions that will have a negative impact on their operations
- Elicit  information by observing the adversary and learn more about their modus operandi (TTPs)
- Understand  the outcomes of the operational actions (output)

Refer to the  [Engage Handbook](https://engage.mitre.org/wp-content/uploads/2022/04/EngageHandbook-v1.0.pdf)  to learn more. 

You can interact with the  [Engage Matrix Explorer](https://engage.mitre.org/matrix) . We can filter by information from  [MITRE ATT&CK](https://attack.mitre.org/) . 

Note that by default the matrix focuses on  Operate , which entails  Expose ,  Affect , and  Elicit .


D3FEND

What is this MITRE resource?  Per the  [D3FEND](https://d3fend.mitre.org/)  website, this resource is " _A knowledge graph of cybersecurity countermeasures._ "

D3FEND is still in beta and is funded by the Cybersecurity Directorate of the NSA. 

D3FEND  stands for  D etection,  D enial, and  D isruption  F ramework  E mpowering  N etwork  D efense.  

At the time of this writing, there are 408 artifacts in the D3FEND matrix. See the below image.

![[decoy-file2.png]]

As you can see, you're provided with information on what is the technique ( definition ), how the technique works ( how it works ), things to think about when implementing the technique ( considerations ), and how to utilize the technique ( example ).

Note, as with other MITRE resources, you can filter based on the ATT&CK matrix. 

Since this resource is in beta and will change significantly in future releases, we won't spend that much time on D3FEND. 

The objective of this task is to make you aware of this MITRE resource and hopefully you'll keep an eye on it as it matures in the future.


ATT&CK ®  Emulations Plans

If these tools provided to us by MITRE are not enough, under  [MITRE ENGENUITY](https://mitre-engenuity.org/) , we have  Adversary Emulation Library , and ATT&CK ®  Emulation Plans .

CTID

MITRE formed an organization named The  [Center of Threat-Informed Defense](https://mitre-engenuity.org/cybersecurity/center-for-threat-informed-defense/)  ( CTID ). This organization consists of various companies and vendors from around the globe. Their objective is to conduct research on cyber threats and their TTPs and share this research to improve cyber defense for all. 

Some of the companies and vendors who are participants of CTID:

- AttackIQ (founder)
- Verizon
- Microsoft (founder)
- Red Canary (founder)
- Splunk

Per the website, " _Together with Participant organizations, we cultivate solutions for a safer world and advance threat-informed defense with open-source software, methodologies, and frameworks. By expanding upon the MITRE ATT&CK knowledge base, our work expands the global understanding of cyber adversaries and their tradecraft with the public release of data sets critical to better understanding adversarial behavior and their movements._ "

![[SoftwareFlow Sandwomr Team.jpeg]]

ATT&CK and Threat Intelligence

**Threat Intelligence (TI)**  or **Cyber Threat Intelligence (CTI)** is the information, or TTPs, attributed to the adversary. By using threat intelligence, as defenders, we can make better decisions regarding the defensive strategy. Large corporations might have an in-house team whose primary objective is to gather threat intelligence for other teams within the organization, aside from using threat intel already readily available. Some of this threat intel can be open source or through a subscription with a vendor, such as [**CrowdStrike**](https://www.crowdstrike.com/) . In contrast, many defenders wear multiple hats (roles) within some organizations, and they need to take time from their other tasks to focus on threat intelligence. To cater to the latter, we'll work on a scenario of using ATT&CK® for threat intelligence. The goal of threat intelligence is to make the information actionable.

An advanced persistent threat (APT) is a stealthy threat actor, typically a nation state or state-sponsored group, which gains unauthorized access to a computer network and remains undetected for an extended period.
---

## Related Notes
- [[Pyramid of Pain]]
- [[Cyber Kill Chain]]
- [[Unified Kill Chain]]
- [[Diamond Model]]
- [[Intro to Cyber Threat Intel]]
- [[Splunk Basics]]
- [[Sysmon]]
