

Difference between Network Devices and Endpoint Devices

- imperative to understand the difference between network devices and endpoint devices. Endpoint devices refer to any device that can generate or consume data on a network, such as Laptops, Desktops, Smartphones, Tablets, Printers, Servers, and IoT Devices. 
- They are typically located at the edge of a network and interact directly with users. 
- The figure below shows the difference between endpoint and network devices based on their functionality, traffic, and configuration.

![difference between endpoint and network device](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/442f322a1e8013f07092337940676a94.png)


Common Threats and Attack Vectors of Network Devices  

- The unprecedented growth in today's Information and Communication Technology (ICT) networks has transformed the world into a global village.
- On the other hand, it has also given rise to multifarious malicious activities by cyber attackers. 
- As we have already studied, the various network devices are the backbone of modern ICT networks. To ensure confidentiality, integrity, and availability (CIA) in our networks and systems, it is imperative that we implement security hardening measures to these devices. 
- Some common goals of hardening include protection from unauthorised access & attacks/exploits, enforcement of access policies, prevention of data theft, and continuous availability of critical systems.

|                                 |                                                                                                                                                                                         |                                                                                                                                                                                                                                                             |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Threat  <br>**                | **Description  <br>**                                                                                                                                                                   | **Attack Vector**                                                                                                                                                                                                                                           |
| **Unauthorised access**         | Gain unauthorised control of a network device, and then the complete network.                                                                                                           | - Password attacks (brute force, dictionary & hybrid)<br>- Exploit known vulnerabilities, e.g. RCE<br>- Social Engineering/Phishing attack to trick network administrators into disclosing sensitive information such as usernames and passwords of devices |
| **Denial of Service (DoS)**     | Disruption of critical devices and services to make them unavailable to genuine users.                                                                                                  | - Flooding devices with fake requests<br>- Exploiting vulnerabilities in logical or resource handling<br>- Manipulating network packets                                                                                                                     |
| **Man-in-the-Middle Attacks**   | Intercept the network requests between two parties by masquerading as each other to steal sensitive information or alter/manipulate the requests.                                       | - ARP spoofing<br>- DNS spoofing<br>- Rogue access points                                                                                                                                                                                                   |
| **Privilege escalation**        | Gaining higher-level privileges or rights to perform restricted actions, e.g. accessing sensitive information or executing malicious code.                                              | - Weak passwords or use of the same passwords for user and admin accounts<br>- Exploiting vulnerabilities<br>- Misconfigurations                                                                                                                            |
| **Bandwidth theft/ hotlinking** | Linking a bandwidth-intensive resource (image or video) from an external website to its original website, without permission. This can cause increased traffic to the original website. | - Scraping large volumes of data  <br>    <br>- DoS attacks  <br>    <br>- Malware attacks                                                                                                                                                                  |

General Techniques

Hardening techniques are meant to reduce the attack surface of a system or network by removing unnecessary functionality, limiting access, and implementing various security controls. 

- **Updating & Patching**: Ensuring the latest version of the Operating System and underlying applications of all devices and systems and installing regular security patches is the core hardening measure. Outdated OS and applications contain vulnerabilities that attackers can exploit.
- **Disabling unnecessary services & ports**: Turn off all unnecessary services and block all ports (physical and virtual) that are not needed for system functionality. This will reduce the attack surface by minimising the number of entry points an attacker can exploit.
- **Principle of Least Privilege (POLP)**: Restrict users and processes to only the minimum necessary permissions required to perform their functions.
- **Logs Monitoring**: Implement a log monitoring system to monitor for unusual activity or security events.
- **Backup regularly**: Take routine backups of systems and configurations as they can help recover from a security incident or system failure.
- **Enforcing Strong Passwords**: Change default login passwords and use strong passwords that are at least ten characters long with a combination of small letters, capital letters, special characters, and numbers. These types of passwords protect against dictionary and brute-force attacks.
- **Multi-Factor Authentication (MFA)**: MFA is an additional security layer requiring two or more types of identification before accessing the account or system. The two factors are generally something we know (like passwords) and something we have (like biometrics).
Importance of Secure Protocols

Secure protocols play a critical role in network device hardening by protecting against unauthorised access and data breaches. They ensure that sensitive data transmitted between devices is encrypted and cannot be intercepted by malicious actors. Moreover, secure protocols also help prevent man-in-the-middle attacks and other network-based exploits. Using secure protocols, network administrators can ensure that only authorised personnel can access sensitive information and perform system administration tasks. Necessary security protocols include HTTPS, SSH, SSL/TLS, and IPsec. You can learn more about secure network protocols in [this](http://tryhackme.com/jr/networksecurityprotocols) room.

Removal/Blocking of Insecure Protocols 

In addition to using secure protocols, removing and blocking access to those insecure protocols is equally essential, which will decrease an attacker's attack surface. Most important are the protocols that transmit data in clear text without encrypting them, like FTP, HTTP, Telnet, SMTP, and more. Moreover, there are inherently secure protocols (e.g. LDAP, RDP, SIPS); however, they can allow attackers to exploit the network if configured incorrectly.

- **Syslog**: A protocol to standardise the transfer of log messages, with the purpose of storing and analysing log messages to a central server.
- **SNMP**: Traps a notification sent by a network device to a management system when a predefined event occurs.
- **NetFlow**: A protocol used to collect and analyse network traffic data for monitoring and security analysis.
- **Packet Captures**: Capturing network traffic and storing it for analysis using a tool like Wireshark.

Virtual private networks (VPNs) are now needed in the age of remote work and online communication to protect sensitive data and preserve privacy. Yet, hardening VPNs is crucial to ensure their efficiency as cyberattacks continue to develop. Hardening VPNs entails adopting additional security measures, such as multi-factor authentication and encryption techniques, to make it more challenging for hackers to access the network. By taking these extra precautions, businesses can better safeguard their data and defend against cyberattacks, raising their security level and bringing them more peace of mind. 

This task will cover hardening a VPN server by focusing on secure authentication, strong encryption, and proper update. We cover the different configuration options available and which are considered the safest by the industry.

Connecting to the Machine  
We will be using an Ubuntu machine with OpenVPN installed throughout the room. You can start the virtual machine by clicking `Start Machine`. The machine will start in a split-screen view. In case the VM is not visible, use the blue `Show Split View` button at the top-right of the page. Please wait 3-5 minutes to make sure the VM is fully booted.

Standard Hardening Practices  
Usually, all the VPN servers consist of server-side and client-side configurations through a standard config file. System administrators must understand the file's content and edit it as per best security practices. You will be using the following commands in the upcoming exercises:

- The OpenVPN server config file is located at `/etc/openvpn/server/server.conf`. Once the machine is loaded, open the terminal and load the file by issuing the command `sudo nano /etc/openvpn/server/server.conf`. 
- Once you made the desired changes in the file, press `Ctrl+O` and hit `Enter`, then press `Ctrl+X` to exit.
- The command `sudo systemctl restart openvpn-server@server.service` can restart the OpenVPN service. 

Moving forward, the following are some of the significant hardening practices for a VPN server:

- Use strong encryption algorithm: Configure the VPN gateway to use strong encryption to protect data in transit. The **cipher** directive in the config file can be used to select the encryption scheme. The possible options for [cipher](https://community.openvpn.net/openvpn/wiki/CipherNegotiation) include AES, Blowfish, Camellia, and more. For example, **AES-128-CBC** mode means to use the AES encryption algorithm with a key size of 128-bit in Cipher Block Chaining (CBC) mode, as seen below. **AES-256-CBC** is typically considered one of the strongest cipher encryption nowadays.
    

OpenVPN Configuration

```shell-session
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local 10.80.184.37 
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
cipher AES-128-CBC #cipher options can be modified
dh dh.pem
auth SHA256 tls-crypt tc.key
topology subnet
```

  
- **Keep VPN gateway software up-to-date**: Ensure that the VPN gateway software is always updated with the latest security patches and updates. Every VPN software has a different method for it. You can use `sudo apt upgrade openvpn` to update OpenVPN (please note that the attached VM does not have an internet connection).
    
- Implement strong authentication: Use strong authentication mechanisms such as a combination of Transport Layer Security (TLS) and a secure hashing algorithm. We can use the `auth` directive to specify the exact algorithm in the OpenVPN configuration file to ensure that a secure hashing algorithm will be used for packet authentication. Some of the [options](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage#--auth%20alg) for auth directive are **SHA1, SHA128, SHA256, SHA512 and MD5**. You can set the auth directive through the following command:
    

OpenVPN Configuration

```shell-session
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local 10.80.184.37 
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
auth SHA256 #use this to change the auth parameter
tls-crypt tc.key
topology subnet
```

  
- **Change default settings**: Change the default usernames and passwords to something unique to reduce the risk of unauthorised access to the VPN gateway.
    
- **Enable Perfect Forward Secrecy (PFS)**: Perfect Forward Secrecy (PFS) in OpenVPN generates unique session keys for each session to strengthen the security of the VPN connection. Because of this, even if a hacker successfully obtained a session key, they could not use it to decode more sessions. For each session, PFS generates a new set of encryption keys, preventing the possibility of remotely decrypting previously acquired material. As a result, it is far more challenging for an attacker to spoof the VPN connection and steal sensitive data. We can use the `tls-crypt` directive in the OpenVPN configuration file to enable PFS. The `tls-crypt` directive requires a key that can be generated using the command `sudo openvpn --genkey --secret my.key` and should be placed in the same directory on the server. Choosing the appropriate cipher and auth, like **cipher AES-256-CBC** and **auth SHA 256**, supports PFS if combined with tls-crypt. The exact configuration is mentioned below:
    

OpenVPN Configuration

```shell-session
thm@machine$ sudo nano /etc/openvpn/server/server.conf
local 10.80.184.37 
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
cipher AES-256-CBC 
auth SHA256 
tls-crypt my.key #use this to change the tls-crypt parameter
tls-version-min 1.2  #use this to change the TLS version
topology subnet
```

  
- **Dedicated Users for VPN Server:** Limit user access by creating a dedicated user account and group with restricted permissions specifically for running the OpenVPN server.
    

Plenty of other options can help you secure and harden an OpenVPN server; it all depends on the organisation's requirements. However, by default providing restricted access to the users enables a limited attack surface for the attacker.
---

## Related Notes
- [[Networking Secure Protocols]]
- [[Networking Concepts]]
- [[Introduction to SIEM]]
