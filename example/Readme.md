# Infomaniak Candidate Test – Answers

___

## 1. Which position are you applying to?
**Answer:**  
*Site Reliability Engineer – Database and Monitoring*

___

## 2. Are you living or willing to relocate in Geneva's region (Romandy/Neighboring French departments)?
**Answer:**  
I’m currently based in Alsace, but I’m open to relocating to Romandy or to a nearby French border area.

___

## 3. What is the list of IPs present in infomanihack.ch SPF (*)?
**Answer:**  

**Method:**  
The `dig` command in Linux/Unix is used for DNS lookup. I recursively retrieved all included SPF records for `infomaniak.ch` and consolidated duplicates.

```bash
nla@Nabils-MBP ~ % dig +short TXT infomaniak.ch

"v=DMARC1;p=reject;sp=reject;rua=mailto:dmarc-report@infomaniak.com;ruf=mailto:dmarc-report@infomaniak.com"
"google-site-verification=Xu--JCr0xQrSN5NyRs1oJRPPt-6Mz1zGwaHTcN9Nuk0"
"google-site-verification=DCTpLg4xrd9HhvJ8-Zpz9p_soPj28VJDlOmVzBSSR7I"
"google-site-verification=u-9CxpEBZH3tMFWrWk3TU_DYr8ow56pXeaNDRhLYekI"
"google-site-verification=1r3y1ZR46R0pqXDE4aG6DOgkc3tBm6E6kew6LefC_wo"
"v=DMARC1"
"v=spf1 ip4:164.128.163.171 include:spf.infomaniak.ch -all"
nla@Nabils-MBP ~ %
```
```bash
nla@Nabils-MBP ~ % dig +short TXT spf.infomaniak.ch
"v=spf1 ip4:84.16.68.96 ip4:84.16.68.94 include:relay.mail.infomaniak.ch include:app.mail.infomaniak.ch include:newsletter.infomaniak.com -all"
nla@Nabils-MBP ~ %
```
```bash
nla@Nabils-MBP ~ % dig +short TXT relay.mail.infomaniak.ch
"v=spf1 ip4:45.157.188.8/29 ip4:185.125.25.8/29 ip4:83.166.143.168/29 ip4:84.16.66.168/29 ip4:128.65.197.100 ip4:128.65.197.101 ip6:2001:1600:4:17::/64 ip6:2001:1600:7:10::/64 ip6:2001:1600:4:2d::c565 ip6:2001:1600:7:10::c564 -all"
```
```bash
nla@Nabils-MBP ~ % dig +short TXT app.mail.infomaniak.ch
"v=spf1 ip4:84.16.68.109 ip4:84.16.68.110 ip4:84.16.68.111 ip4:84.16.68.112 ip4:185.125.25.16/29 ip4:45.157.188.16/29 ip4:84.16.66.176/29 ip4:83.166.143.176/29 ip6:2001:1600:4:17::/64 ip6:2001:1600:7:10::/64 -all"
```
```bash
nla@Nabils-MBP ~ % dig +short TXT newsletter.infomaniak.com
"v=spf1 include:amazonses.com ?all"
```

```bash
nla@Nabils-MBP ~ % dig +short TXT amazonses.com
"yahoo-verification-key=OL6T0cZm2ykeymVyCj7mnvnTL3zAtLwrRXGAgBFtvFw="
"mailru-verification: 71ab435de908d6ed"
"google-site-verification=aOJq8aXEtCO23r176f6iOTGt-RVuPv81XPtBuIzRTx0"
"v=spf1 ip4:199.255.192.0/22 ip4:199.127.232.0/22 ip4:54.240.0.0/18 ip4:69.169.224.0/20 ip4:23.249.208.0/20 ip4:23.251.224.0/19 ip4:76.223.176.0/20 ip4:54.240.64.0/18 ip4:76.223.128.0/19 ip4:216.221.160.0/19 ip4:206.55.144.0/20 ip4:24.110.64.0/18 -all"
nla@Nabils-MBP ~ %
```

Quick summary (I’ve consolidated and removed duplicate entries Some IPv6 /64 addresses appeared multiple times in the includes, so I’ve listed them only once)

**Liste of SPF records (infomaniak.ch)**

***IPv4:***
164.128.163.171/32
84.16.68.96/32
84.16.68.94/32
84.16.68.109/32
84.16.68.110/32
84.16.68.111/32
84.16.68.112/32
45.157.188.8/29
45.157.188.16/29
185.125.25.8/29
185.125.25.16/29
83.166.143.168/29
83.166.143.176/29
84.16.66.168/29
84.16.66.176/29
128.65.197.100/32
128.65.197.101/32

**Amazon SES (via include:amazonses.com)**

***IPv4:***
199.255.192.0/22
199.127.232.0/22
54.240.0.0/18
54.240.64.0/18
69.169.224.0/20
23.249.208.0/20
23.251.224.0/19
76.223.176.0/20
76.223.128.0/19
216.221.160.0/19
206.55.144.0/20
24.110.64.0/18

***IPv6:***
2001:1600:4:17::/64
2001:1600:7:10::/64
2001:1600:4:2d::c565/128
2001:1600:7:10::c564/128

___

## 4. Where can you usually find DNS information on a Linux system ?
**Answer:**  

- On a Linux system, DNS information is usually stored in */etc/resolv.conf*.
  `cat /etc/resolv.conf`

- We can also check DNS configuration with:
  `systemd-resolve --status`     *on systemd systems*
  `nmcli dev show | grep DNS`    *on NetworkManager systems*


- Directly in the configuration file of the systemd-resolved service or view its status
  `cat /etc/systemd/resolved.conf`
  `sudo systemctl status systemd-resolved.service`

___

## 5. What is the abuse address of the 185.181.161.0/24 range (*) ?
**Answer:**  
	--> The abuse adress is registred in public IP/network databases. We can found it with `whois` command

```bash
nla@Nabils-MBP ~ % whois 185.181.161.0 | grep -E 'inetnum|abuse-mailbox' |tail -2    
abuse-mailbox:  abuse@infomaniak.ch
nla@Nabils-MBP ~ %
```
*We also use tail to keep only the infomaniak inetnum and the abuse-mail*
___

## 6. Do you prefer using Vim or Emacs ?
**Answer:**  
I prefer Vim; it’s simpler and lighter to use.

___
