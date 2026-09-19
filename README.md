# NETWORKWALKS-BO83-WK2-PM1-FOOTPRINTING-RECONNAISSANCE
 ## Footprinting & Reconnaissance — README

This guide documents the WK2-PM1 Footprinting & Reconnaissance task: gathering public information about a live website (networkwalks.com) using six built-in Kali Linux command-line tools, and recording each finding as evidence.

## Task Requirements
Kali Linux (running in an Oracle VirtualBox VM)
Six reconnaissance tools, all pre-installed on Kali: whois, whatweb, nslookup, curl, wafw00f, dnsrecon
Target: networkwalks.com (authorized training domain)
A screenshot and saved text output for each tool run
## Tasks Performed
1. WHOIS domain lookup
whois networkwalks.com | tee whois_output.txt

Returned the domain's registrar (GoDaddy), registration/expiry dates, and name servers (ns6135.hostgator.com, ns6136.hostgator.com) — revealing HostGator as the hosting provider.


2. WhatWeb technology fingerprinting
whatweb networkwalks.com | tee whatweb_output.txt

Identified the web stack: Apache, WordPress 7.1, WordPress Download Manager 3.3.58, server IP 192.232.216.135, and JQuery 3.7.1.


3. Nslookup DNS resolution
nslookup networkwalks.com | tee nslookup_output.txt

Resolved the domain to 192.232.216.135, matching the IP reported by WhatWeb.



4. Curl HTTP response headers
curl -I https://networkwalks.com

Returned the HTTP response headers, including a reference to the WordPress REST API endpoint /wp-json/.

5. Wafw00f WAF detection
wafw00f networkwalks.com | tee wafw00f_output.txt

Identified ModSecurity (SpiderLabs) as the Web Application Firewall protecting the site.



6. DNSRecon DNS enumeration
dnsrecon -d networkwalks.com | tee dnsrecon_output.txt

Enumerated the domain's full DNS footprint: name servers running BIND 9.16.23-RH, mail server mail.networkwalks.com, SPF/TXT records, and confirmed no SRV records or DNSSEC response.



Quick Reference: Findings
Field	Value
Domain	networkwalks.com
Server IP	192.232.216.135
Hosting provider	HostGator
Web server	Apache
CMS / plugins	WordPress 7.1, WP Download Manager 3.3.58
Mail server	mail.networkwalks.com
DNS software	BIND 9.16.23-RH
DNSSEC	Not enabled
WAF	ModSecurity (SpiderLabs)
Notes

All six tools used here are passive, non-intrusive OSINT tools — they only read information the target has already made public, without sending any exploit or attack traffic. This makes footprinting powerful and very hard to detect from the target's side.

Based on the "Footprinting & Reconnaissance Attacks with Multiple Kali Tools" task from Networkwalks Academy — www.networkwalks.com

