---
title: "Viewing abnormal behavior information"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Viewing-abnormal-behavior-information"
---

Network Detection and Response (NDR) utilizes behavioral analysis technology to detect abnormal behaviors of different hosts in the network to facilitate the discovery of potential risks and advanced threats. The abnormal behavior page displays the overall trend of abnormal behavior of the current network host, including mining behavior analysis, proxy penetration analysis, remote tool analysis, login behavior analysis, covert tunnel analysis, file threat analysis, and email data analysis.

<span id="b02ba27b"></span>
## Prerequisites

Risk detection is already enabled for your assets.

<span id="22c56996"></span>
## Procedure


1. Log in to the NDR console.

2. Select **Threat center** ＞ **Abnormal behavior** in the left navigation pane.

3. View abnormal behavior information.

   * Overview: Displays trends in the volume of various threat types.

   * Mining behavior: The mining behavior analysis page provides a scenario\-based analysis of mining hosts across your network. Use this page to identify mining activities and perform further analysis using data such as the top 5 mining pool IP addresses, top 5 mining pool domain names, and a list of alerts for affected assets.

   * Proxy penetration: The proxy penetration analysis page displays the top 5 proxy IP addresses and the top 5 internal IP addresses accessed through proxies to help you identify potential hosts at risk in your private network.

   * Remote tools: The remote tool analysis page checks for any remote tools used for outbound communication on the network, including Sunflower and TeamViewer.

   * Login behavior: The login analysis page displays all the hosts with a weak password in the network. Weak passwords are a common vulnerability exploited by attackers. This page displays information about assets with weak passwords so that you can take corrective action or apply security hardening.

   * Covert tunnels: The covert tunnel analysis page provides a risk overview of covert tunnels in assets on the entire network, including asset IP address, external control IP address, direction, tunnel type, uplink traffic, and downlink traffic. Use this data to investigate security risks on the affected hosts such as covert tunnel communication and data theft.

   * File threats: File threat analysis can effectively identify different types of malicious files such as exe, dll, zip, rar, elf, and gzip. The file threat analysis page displays the distribution of file types on the current network and the top 5 most downloaded files. It also provides a detailed list of malicious files, including asset IP address, external IP address, direction, file name, file MD5 value, virus type, and the time of the last alert. You can download malicious files. Warning: To ensure your network security, only open downloaded malicious files in an isolated environment, such as a sandbox.

   * Email data: This feature supports auditing email traffic over protocols like SMTP and reconstructing messages for review and identifies security risks such as virus emails, phishing emails, and email leaks. The page displays the top recipients and senders by email volume. The email audit content includes: sender's email address, recipient's email address, email subject, attachment name, attachment MD5 value, email type, and the time of the last alert.
