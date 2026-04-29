
What is NSLookup?
- Stands for Name Server Lookup
- Queries DNS servers to translate domain names > IP addresses
- Like a phone book: give it a name, get a number 

Powershell Commands

Find Your Ip Address
ipconfig
- shows all adapters
ipconfig | findstr "IPv4"
- show only your IP addresses
ipconfig /all 
- shows adapter descriptions (tells you which IP belongs to what)

Multiple IPs? Each one belongs toa different network adapter:
- Your real IP = Wi-Fi or Ethernet adapter (192.168.x.x)
- Extra IPs = Virtual adapters from VirtualBox, VPN, Docker
- Check the Description field in ipconfig /all to confirm which is which

Resolve-DnsName (PowerShell version of nslookup)

Resolve-DnsName domain.com - Type A
- IPv4 address
- where the site is hosted
Resolve-DnsName domain.com - Type AAAA
- IPv6 address
- where the site is hosted
Resolve-DnsName domain.com - Type MX
- who handles the email
Resolve-DnsName domain.com -Type NS
- who manages DNS
Resolve-DnsName domain.com -Type TXT
 - security records (SPF, DKIM, DMARC)
 Resolve-DnsName domain.com -Type SOA
 - www pointing root domain
 Resolve-DnsName domain -Type PTR
 - reverse lookup (IP > hostname)
Resolve-DnsName domain.com -Type ANY
- all records at once

Useful Flags

Resolve-DnsName domain.com -Server 8.8.8.8 
- query a specific DNS server
Resolve-DnsName domain.com -Tcp0nly
- force TCP instead of UDP 
Resolve-DnsName domain.com -NoRecursion
- bypass cache
 Resolve-DnsName domain.com | Format-List * 
 - show all properties (TTL, section, etc)

DNS Cache Commands

Get-DnsClientCache 
- view cached DNS records

Clear-DnsClientCache
- flush/clear the cache

What Each Record Type Means
A
- This website lives at this IPv4 address
AAAA
- This website lives at this IPv6 address
MX
- email for this domain goes to this mail server
NS
- this company manage the DNS (GoDaddy, Cloudflare, etc)
TXT 
- these servers are authorized to send email as us (SPF/DKIM/DMARC)
SOA
- this is the primary authority for this DNS zone
CNAME
- this name is an alias that points to another name
PTR
-  This IP address belongs to this hostname (revers of A record)


TTL (Time To Live)
- measured in seconds
- tells your computer how long to cache a DNS record before asking again
- 300 = 5 minutes (low - changes spread fast)
- 3600 = 1 hour (standard)
- 86400 = 24 hours (high - fewer lookups but slow to update)

DNS Troubleshooting Flow (Interview Scenario)
"A user can't reach a website"

1. ping google.com - does it resolve?
2. ping 8.8.8.8 - does raw IP work?
	- if yes > its a DNS problem
	- if no > its a network problem
3. Resolve-DnsName site.com -Server 8.8.8.8 - compare company DNS vs Google DNS
	- if google works but company DNS doesn't > internal DNS server issue
4. Clear-DnsClientCache - flush stale cache
5. ipconfig /all - verify DNS server settings are correct

---

## Related Notes
- [[Networking Core Protocols]]
- [[Networking Essentials]]
- [[Nmap - The Basics]]
