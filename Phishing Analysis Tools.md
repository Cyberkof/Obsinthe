
Remember from [Phishing Room 1](https://tryhackme.com/room/phishingemails1tryoe); we covered how to manually sift through the email raw source code to extract information. 

In this room, we will look at various tools that will aid us in analyzing phishing emails. We will: 

- Look at tools that will aid us in examining email header information.
- Cover techniques to obtain hyperlinks in emails, expand the URLs if they're URL shortened.
- Look into tools to give us information about potentially malicious links without directly interacting with a malicious link.
- Cover techniques to obtain malicious attachments from phishing emails and use malware sandboxes to detonate the attachments to understand further what the attachment was designed to do.

Warning: The samples throughout this room contain information from actual spam and/or phishing emails. Proceed with caution if you attempt to interact with any IP, domain, attachment, etc.


In this task, we will outline the steps performed when analyzing a suspicious or malicious email. 

Below is a checklist of the pertinent information an analyst (you) is to collect from the email header:

- Sender email address
- Sender IP address
- Reverse lookup of the sender IP address
- Email subject line
- Recipient email address (this information might be in the CC/BCC field)
- Reply-to email address (if any)
- Date/time

Afterward, we draw our attention to the email body and attachment(s) (if any).

Below is a checklist of the artifacts an analyst (you) needs to collect from the email body:

- Any URL links (if an URL shortener service was used, then we'll need to obtain the real URL link)
- The name of the attachment
- The hash value of the attachment (hash type MD5 or SHA256, preferably the latter)

**Warning**: Be careful not to click on any links or attachments in the email accidentally.

Some of the pertinent information that we need to collect can be obtained visually from an email client or web client (such as Gmail, Yahoo!, etc.). But some information, such as the sender's IP address and reply-to information, can only be obtained via the email header.

In [Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe), we saw how to obtain this information manually by sifting through an email's source code.

Below we'll look at some tools that will help us retrieve this information.

First up to bat is a tool from Google that can assist us with analyzing email headers called **Messageheader** from the Google Admin Toolbox. 

Per the [site](https://toolbox.googleapps.com/apps/main/), "_Messageheader analyzes SMTP message headers, which help identify the root cause of delivery delays. You can detect misconfigured servers and mail-routing problems_".

**Usage**: Copy and paste the entire email header and run the analysis tool. 

- **Messageheader**: [https://toolbox.googleapps.com/apps/messageheader/analyzeheader](https://toolbox.googleapps.com/apps/messageheader/analyzeheader)

![](https://assets.tryhackme.com/additional/phishing2/messageheader.png)  

Another tool is called **Message Header Analyzer**. 

- **Message Header Analyzer**: [https://mha.azurewebsites.net/](https://mha.azurewebsites.net/)

![](https://assets.tryhackme.com/additional/phishing2/mha.png)  

Lastly, you can also use [mailheader.org](https://mailheader.org/).

![](https://assets.tryhackme.com/additional/phishing2/mailheader.png)  

Even though not covered in the previous Phishing rooms, a Message Transfer Agent (MTA) is software that transfers emails between sender and recipient. Read more about MTAs [here](https://csrc.nist.gov/glossary/term/mail_transfer_agent). Since we're on the subject, read about MUAs (Mail User Agent) [here](https://csrc.nist.gov/glossary/term/mail_user_agent). 

**Note**: The option on which tool to use rests ultimately on you. It is good to have multiple resources to refer to as each tool might reveal information that another tool may not reveal. 

The tools below can help you analyze information about the sender's IP address:

- IPinfo.io: [https://ipinfo.io/](https://ipinfo.io/)[](https://ipinfo.io/)

Per the [site](https://ipinfo.io/), "_With IPinfo, you can pinpoint your users’ locations, customize their experiences, prevent fraud, ensure compliance, and so much more_".

![](https://assets.tryhackme.com/additional/phishing2/ipinfo.png)  

- URLScan.io: [https://urlscan.io/](https://urlscan.io/)[](https://urlscan.io/)

Per the [site](https://urlscan.io/about/), "_urlscan.io is a free service to scan and analyse websites. When a URL is submitted to urlscan.io, an automated process will browse to the URL like a regular user and record the activity that this page navigation creates. This includes the domains and IPs contacted, the resources (JavaScript, CSS, etc) requested from those domains, as well as additional information about the page itself. urlscan.io will take a screenshot of the page, record the DOM content, JavaScript global variables, cookies created by the page, and a myriad of other observations. If the site is targeting the users one of the more than 400 brands tracked by urlscan.io, it will be highlighted as potentially malicious in the scan results_".

![](https://assets.tryhackme.com/additional/phishing2/urlscan.png)

Notice that urlscan.io provides a screenshot of the URL. This screenshot is provided, so you don't have to navigate to the URL in question explicitly.

You can use other tools that provide the same functionality and more, such as [URL2PNG](https://www.url2png.com/) and [Wannabrowser](https://www.wannabrowser.net/).

- Talos Reputation Center: [https://talosintelligence.com/reputation](https://talosintelligence.com/reputation)

![](https://assets.tryhackme.com/additional/phishing2/talos.png)

![[Pasted image 20251102165103.png]]




![[Pasted image 20251102165331.png]]

![[Pasted image 20251102165606.png]]


A tool that will help with automated phishing analysis is [PhishTool](https://www.phishtool.com/).

Yes, I saved this for last! What is PhishTool?

Per the site, "_Be you a security researcher investigating a new phish-kit, a SOC analyst responding to user reported phishing, a threat intelligence analyst collecting phishing IoCs or an investigator dealing with email-born fraud._

_PhishTool combines threat intelligence, OSINT, email metadata and battle tested auto-analysis pathways into one powerful phishing response platform. Making you and your organisation a formidable adversary - immune to phishing campaigns that those with lesser email security capabilities fall victim to._"

Note: There is a free community edition you can download and use. :)

I uploaded a malicious email to PhishTool and connected VirusTotal to my account using my community edition API key. 

Below are a few screenshots of the malicious email and the PhishTool interface. 

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/0dcc25c992ddfdfc60532f6fb9416a70.png)  

From the image above, you can see the PhishTool conveniently grabs all the pertinent information we'll need regarding the email.

- Email sender
- Email recipient (in this case, a long list of CCed email addresses)
- Timestamp
- Originating IP and Reverse DNS lookup

We can obtain information about the SMTP relays, specific X-header information, and IP info information.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/9665b8957923a892e721a0e02e42ea9f.png)  

Below is a snippet of Hop 1 of 6 (SMTP relays).

![](https://assets.tryhackme.com/additional/phishing2/phish-smtp.png)  

Notice that the tool notifies us that '**Reply-To no present**' although it provides the alternative header information, **Return-Path**.

To the right of the PhishTool dashboard, we can see the email body. There are two tabs across the top that we can toggle to view the email in text format or its HTML source code. 

Text view:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/94366a297a0abb9b7f680e006c421b45.png)  

HTML view:  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e5eb24859d263b8d233f52c1502aaed4.png)  

The bottom two panes will display information about attachments and URLs.

The right pane will show if any URLs were found in the email. In this case, no emails were found.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/a737376ca1243a926f7a41a765cb7a1e.png)  

The left pane will show information about the attachment. This particular malicious email has a zip file.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/685f9bb5291973038d55aca7c09ffd1e.png)  

We can automatically get feedback from VirusTotal since our community edition API key is connected.

Here we can grab the zip file name and its hashes without manually interacting with the malicious email.

 There is an ellipsis at the far right of the above image. If that is clicked, we are provided additional actions that we can perform with the attachment.

Below is a screenshot of the additional options sub-menu.

![](https://assets.tryhackme.com/additional/phishing2/phish-options.png)  

Let's look at the Strings output.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/e1f11b62dbd9ed415177bdbc44a13d2d.png)  

Next, let's look at the information from VirusTotal.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/5c0556b15a803638a2d289915edc8946.png)  

Since the VirusTotal API key is the free community edition, an analyst can manually navigate to VirusTotal and do a file hash search to view more information about this attachment. 

Lastly, any submissions you upload to PhishTool, you can flag as malicious and resolve with notes. Similar to how you would if you were a SOC Analyst.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/31728d39e79f36340ab8bcdd740940d6.png)

The attachment file name and file hashes will be marked as malicious. Next, click on **Resolve**.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de58e2bfac4a912bcc7a3e9/room-content/64c5e32e65919e17e352161594fbb627.png)  

In the next screen, an analyst can mark the email based on dropdown selections. Refer to the GIF below.

![](https://assets.tryhackme.com/additional/phishing2/resolve-case.gif)  

**Note**: I didn't perform further analysis on the domain name or the IP address. Neither did I perform any research regarding the root domain the email originated from. The attachment can further be analyzed by uploading it to a malware sandbox to see what exactly it's doing, which I did not do. Hence the reason why additional Flag artifacts and Classifications codes weren't selected for this malicious email. :) 

To expand on classification codes briefly, not all phishing emails can be categorized as the same. A classification code allows us to tag a case with a specific code, such as Whaling (high-value target). Not all phishing emails will target a high-value target, such as a Chief Financial Officer (CFO).

![[Pasted image 20251102172252.png]]


![[Pasted image 20251102172552.png]]


![[Pasted image 20251102172737.png]]










The tools covered in this room are just some that can help you with analyzing phishing emails. 

As a defender, you'll come up with your own preferred tools and techniques to perform manual and automated analysis. 

Here are a few other tools that we have not covered in detail within this room that deserve a shout:

- [https://mxtoolbox.com/](https://mxtoolbox.com/)
- [https://phishtank.com/?](https://phishtank.com/?)
- [https://www.spamhaus.org/](https://www.spamhaus.org/)[](https://www.spamhaus.org/)

That's all, folks! Happy Hunting!
---

## Related Notes
- [[Phishing]]
- [[PhishTool]]
- [[Threat Intelligence Tools]]
- [[Intro to Cyber Threat Intel]]
- [[Mail Servers]]
