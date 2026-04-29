Spam and Phishing are common social engineering attacks. In social engineering, phishing attack vectors can be a phone call, a text message, or an email. As you should have already guessed, our focus is on email as the attack vector. 

We all should be somewhat familiar with what **spam** is. No matter what, these emails somehow find their way into our inboxes. 

The first email classified as spam dates back to [1978](https://www.britannica.com/topic/spam), and it's still thriving today.   

**Phishing** is a serious attack vector that you, as a defender, will have to defend against.

An organization can follow all the recommended guidelines when it comes to building a layered defense strategy. Still, all it takes is an inexperienced and unsuspecting user within your corporate environment to click on a link or download and run a malicious attachment which may provide an attacker a foothold into the network. 

Many products help combat spam and phishing, but realistically these emails still can get through. When they do, as a Security Analyst, you need to know how to analyze these emails to determine if they're malicious or benign.

Furthermore, you will need to gather information about the email to update your security products to prevent malicious emails from making their way back into a user's inbox. 

In this room, we'll look at all the components involved with sending emails across the Internet and how to analyze email headers.

A handful of protocols are involved with the "magic" that takes place when you hit SEND in an email client. 

By now, you should already know that certain protocols were created to handle specific network-related tasks, such as email. 

There are 3 specific protocols involved to facilitate the outgoing and incoming email messages, and they are briefly listed below.

- **SMTP** (**Simple Mail Transfer Protocol)** - It is utilized to handle the sending of emails. 

- **POP3 (Post Office Protocol)** - Is responsible transferring email between a client and a mail server. 

- **IMAP (Internet Message Access Protocol)** - Is responsible transferring email between a client and a mail server. 

You should have noticed that both **POP3** and **IMAP** have the same definition. But there are differences between the two.

The difference between the two is listed below: (credit [AOL](https://help.aol.com/articles/what-is-the-difference-between-pop3-and-imap) -- _[You got mail!](https://www.youtube.com/watch?v=gFBLiHpkcOk)_)

**POP3**

- Emails are downloaded and stored on a single device.
- Sent messages are stored on the single device from which the email was sent.
- Emails can only be accessed from the single device the emails were downloaded to.
- If you want to keep messages on the server, make sure the setting "Keep email on server" is enabled, or all messages are deleted from the server once downloaded to the single device's app or software.

**IMAP**

- Emails are stored on the server and can be downloaded to multiple devices.
- Sent messages are stored on the server.
- Messages can be synced and accessed across multiple devices.

Now let's talk about how email travels from the sender to the recipient.

To best illustrate this, see the oversimplified image below:

![](https://assets.tryhackme.com/additional/phishing1/email-network-flow-4.png)  

Below is an explanation of each numbered point from the above diagram:

1. Alexa composes an email to Billy (`billy@johndoe.com`) in her favorite email client. After she's done, she hits the send button.
2. The **SMTP** server needs to determine where to send Alexa's email. It queries **DNS** for information associated with `johndoe.com`. 
3. The **DNS** server obtains the information `johndoe.com` and sends that information to the **SMTP** server. 
4. The **SMTP** server sends Alexa's email across the Internet to Billy's mailbox at `johndoe.com`.
5. In this stage, Alexa's email passes through various **SMTP** servers and is finally relayed to the destination **SMTP** server. 
6. Alexa's email finally reached the destination **SMTP** server.
7. Alexa's email is forwarded and is now sitting in the local **POP3/IMAP** server waiting for Billy. 
8. Billy logs into his email client, which queries the local **POP3/IMAP** server for new emails in his mailbox.
9. Alexa's email is copied (**IMAP**) or downloaded (**POP3**) to Billy's email client. 

Lastly, each protocol has its associated default ports and recommended ports. For example, **SMTP** is port 25.

Great! We know how an email travels from point A to point B and all the protocols involved in the process. 

This task is to understand the components of what makes up an email message when it arrives in an inbox.

This understanding is necessary if you wish to analyze potentially malicious emails manually. 

Before we begin, we need to understand that there are two parts to an email:

- the email **header** (information about the email, such as the email servers that relayed the email)
- the email **body** (text and/or HTML formatted text)

The syntax for email messages is known as the **[Internet Message Format](https://datatracker.ietf.org/doc/html/rfc5322)** (**IMF**).

Let's look at email headers first. 

What do you look for when analyzing a potentially malicious email?

Let's start with the following email header fields:

1. **From** - the sender's email address
2. **Subject** - the email's subject line
3. **Date** - the date when the email was sent
4. **To** - the recipient's email address

This is usually clearly visible in any email client. Let's look at an example of these fields in the below image.

**Warning**: This is a snippet from an actual email. The email in the below image is from a honeypot Yahoo email address. Don't engage/interact with the email addresses or IP addresses revealed in this room.

![](https://assets.tryhackme.com/additional/phishing1/email-headers-1b.png)

**Note**: The numbers in the above image correspond to the email header fields bullet list above.

Another method to obtain the same email header information, and more, is by viewing the '**raw**' email details.

When looking at an email header in detail, it can be intimidating at first, but it's not so bad if you know what to look for. 

**Note**: Depending on your email client, whether a web client or a desktop app, the steps to view these email header fields will vary, but the concept is the same. 

In the below image, you can see how to view this information within Yahoo.

![](https://assets.tryhackme.com/additional/phishing1/email-raw-headers-menu-2.png)

Below is a snippet of the raw message for the email sample.

![](https://assets.tryhackme.com/additional/phishing1/email-raw-headers-2b.png)

**Note**: The above image shows some, not all, of the information within an email's header. 

You can review this email in the `Email Samples` directory on the Desktop within the attached virtual machine. The email is titled `email1.eml`. 

From the above image, there are other email header fields of interest. 

1. **X-Originating-IP** - The IP address of the email was sent from (this is known as an **[X-header](https://help.returnpath.com/hc/en-us/articles/220567127-What-are-X-headers-)**)
2. **Smtp.mailfrom**/**header.from** - The domain the email was sent from (these headers are within **Authentication-Results**)
3. **Reply-To** - This is the email address a reply email will be sent to instead of the **From** email address

To clarify, in the email in the sample above, the **Sender** is newsletters@ant.anki-tech.com, but if a recipient replies to the email, the response will go to reply@ant.anki-tech.com, which is the **Reply-To**, and **NOT** to newsletters@ant.anki-tech.com. 

Below is an additional resource from **Media Template** on how to analyze email headers:

-  [https://web.archive.org/web/20221219232959/https://mediatemple.net/community/products/all/204643950/understanding-an-email-header](https://web.archive.org/web/20221219232959/https://mediatemple.net/community/products/all/204643950/understanding-an-email-header)


![[Pasted image 20251031083932.png]]

The email body is the part of the email which contains the text (plain or HTML formatted) the sender wants you to view. 

Below is an example of a text-only email.

![](https://assets.tryhackme.com/additional/phishing1/email-text-2.png)  

Below is an example of the HTML formatted email.

![](https://assets.tryhackme.com/additional/phishing1/email-html-2.png)  

The above email contains an image (which was blocked by the email client) and embedded hyperlinks.

HTML is what makes it possible to add these elements to an email.

To view an email's HTML code is the same approach shown below, but it may vary depending on the webmail client. 

In the example below, the screenshot is from [Protonmail](https://protonmail.com/). 

![](https://assets.tryhackme.com/additional/phishing1/email-source-code-2.png)  

A snippet of the HTML code is shown below.

![](https://assets.tryhackme.com/additional/phishing1/email-html-code.png)  

In this specific email web client, Protonmail, the option to switch back to HTML is called "**View rendered HTML**".

![](https://assets.tryhackme.com/additional/phishing1/email-render-html.png)  

Again, it will be different for other webmail clients.

Lastly, emails may contain attachments. The same premise applies; you can view an email's attachment from an email's HTML format or by viewing the source code. 

Let's look at a few examples below.

The following example is an HTML formatted email from "Netflix" with an attachment. The web client is Yahoo!

![](https://assets.tryhackme.com/additional/phishing1/email-with-attachment.png)  

1. The email body has an image.
2. The email attachment is a PDF document.

Now let's view this attachment within the source code.

![](https://assets.tryhackme.com/additional/phishing1/email-with-attachment-2.png)  

From the above example, we can see the headers associated with this attachment:

- **Content-Type** is **application/pdf**. 
- **Content-Disposition** specifies it's an **attachment**. 
- **Content-Transfer-Encoding** tells us it's **base64** encoded. 

With the base64 encoded data, you can decode it and save it to your machine.

Warning: When interacting with attachments, proceed with caution and make sure you don't double-click an email's attachment by accident.   

**Note**: Headers specific to 'content' can be found in various locations within an email message source code, and they're not only associated with attachments. For example, **Content-Type** can be **text/html,** and **Content-Transfer-Encoding** can have other values, such as **8bit**.


![[Pasted image 20251031090248.png]]

![[Pasted image 20251031092145.png]]





Before ending this room, you should know what **[BEC](https://www.proofpoint.com/us/threat-reference/business-email-compromise)** (Business Email Compromise) means.

  

A BEC is when an adversary gains control of an internal employee's account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions. 

**Tip**: You should be familiar with this term. I have heard this question asked before in a job interview. 

Within this room, we covered the following:

- What makes up an email address?
- How an email travels from sender to recipient.
- How to view the source code of an email header.
- How to view the source code of an email body. 
- Understand the pertinent information we should obtain from an email we're analyzing.
- Some common techniques attackers use in spam and phishing email campaigns.

In the upcoming Phishing Analysis series, we'll look at samples of various common techniques used in phishing email campaigns, along with tools to assist us with analyzing an email header and email body.


![[Pasted image 20251031093901.png]]
---

## Related Notes
- [[Phishing Analysis Tools]]
- [[PhishTool]]
- [[Mail Servers]]
- [[Networking Core Protocols]]
- [[Moniker Link (CVE-2024-21413)]]
