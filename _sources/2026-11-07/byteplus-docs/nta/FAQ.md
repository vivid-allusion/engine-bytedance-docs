---
title: "FAQ"
product: "Network Detection and Response"
product_code: "nta"
section: "Document"
source: "https://docs.byteplus.com/en/docs/nta/FAQs"
---

<span id="What can NTA do?"></span>
### What can NDR do?


* Intrusion detection: NDR can identify common network attack types, with a high recognition rate and a low false alarm rate. Detectable items include: SQL injection, command injection, web backdoors, weak passwords, proxy tunneling, domain names from a domain generation algorithm (DGA), and other types of threats.

* Vulnerability attack detection: NDR is capable of detecting exploits of popular, common, and high\-risk vulnerabilities, including deserialization, system, and software vulnerabilities among other types of exploits.

* Intelligent detection: Big data analysis technologies such as machine learning algorithms and behavioral analysis models are used to identify potential risks including ransomware, mining, covert tunnels, proxy penetration, DGA domain names, weak passwords, and other threats.

* File threat detection: Supports file auditing and reconstruction in HTTP protocol and identifies various types of malicious files such as exe, dll, zip, rar, elf, and gzip.

* Email data analysis: Supports auditing and restoration of email protocols such as SMTP and identifies security risks such as emails containing viruses, phishing emails, and email leaks.


<span id="Does the NTA system support attack interception?"></span>
### Does the NDR system support attack interception?

The NDR system does not directly intercept attacks. However, it can intercept and protect hosts against threats such as external attacks and abnormal outbound connections by using cloud firewalls.

<span id="How many types of protocols are supported by NTA for IP address resolution?"></span>
### What protocols does NDR support for traffic analysis?

Currently, the NDR system supports traffic analysis for over 20 protocols, including but not limited to TCP, UDP, ICMP, HTTP, HTTPS, RDP, DNS, FTP, POP3, and SMTP.

<span id="What are the differences between NTA and WAF?"></span>
### What are the differences between NDR and WAF?


* WAF adopts a static detection approach and cannot identify unknown threats. WAF protects web services only and cannot protect non\-web services.

* In addition to static detection, the NDR system also supports behavioral analysis, machine learning, correlation analysis, big data modeling, and other technologies to discover unknown, advanced threats that may escape static rules. Besides, the NDR system supports full\-data\-flow data collection and resolution and parsing of 20\-plus major protocols at Layers 2–7 to detect threats in all traffic and provide users with a visualization of full\-network security.


<span id="What are the differences between NTA and host security?"></span>
### What are the differences between NDR and host security?


* Host security detects abnormal host behaviors through agent\-aided host log collection as well as feature analysis, behavior analysis, threat intelligence, and other technologies. Abnormal host behaviors include brute force cracking, mining, command execution, and malicious files.

* The NDR system discovers known cyberattacks and unknown threats through traffic detection, using network traffic as a data source and applying techniques such as feature analysis, threat intelligence, behavior analysis, correlation analysis, and machine learning. Detectable items include: ransomware, mining, covert tunnels, vulnerability attacks, brute force cracking, zombie worms and other incidents. NDR and host security monitor network security from different perspectives, covering both network traffic and host\-level activity. They complement each other to ensure network security.


<span id="Does NTA support virus detection?"></span>
### Does NDR support virus detection?

Yes, NDR supports reconstructing and identifying various types of malicious files in the traffic, such as exe, dll, zip, rar, elf, and gzip. NDR also supports email data analysis and auditing and reconstruction of emails under protocols such as SMTP. It can identify security risks such as emails containing viruses, phishing emails, and email leaks.
