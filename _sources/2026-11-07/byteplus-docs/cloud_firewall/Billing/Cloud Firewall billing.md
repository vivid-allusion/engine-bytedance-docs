---
title: "Cloud Firewall billing"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Pricing"
---

This topic introduces how you will be charged for the use of BytePlus Cloud Firewall service. A pricing example will also be given for your reference.

<span id="0e3c1c87"></span>
### Billing model

Cloud Firewall supports monthly or yearly subscriptions. You are charged based on your selection of the items on the purchasing page.

<span id="74b5495c"></span>
### **Billable items**


|**Feature or billable item** |**Premium Edition** |**Enterprise Edition** |**Ultimate Edition** |**Description** |
|---|---|---|---|---|
|Basic price |USD 420 per month. |USD 1,450 per month. |USD 3,900 per month. |The basic price covers only the default specifications. Additional quotas or value\-added items are not covered. |
|Protected Internet Traffic |The basic price covers 20 Mbit/s of bandwidth. Valid values: 50 to 2000. Unit: Mbit/s. |The basic price covers 50 Mbit/s of bandwidth. Valid values:50 to 10000. Unit: Mbit/s. |The basic price covers 200 Mbit/s of bandwidth. Valid values: 10 to 20000. Unit: Mbit/s. |The peak Internet traffic that can be protected. Metering metric: the peak outbound or inbound Internet traffic, whichever is greater.<br><br>Extra fee: USD 7 per month for each 1 Mbit/s of additional bandwidth. |
|Protected Public IP Addresses |The basic price covers 1000 public IP addresses. |The basic price covers 2000 public IP addresses. |The basic price covers 5000 public IP addresses. |None. |
|Protected VPC firewalls |Not supported |The basic price covers 2 VPC firewalls. Valid values: 2 to 200. |The basic price covers 2 VPC firewalls. Valid values: 5 to 200. |The number of VPC firewalls that can be created. Extra fee: USD 580 per month for each additional VPC firewall. |
|Protected VPC Traffic |Not supported |The basic price covers 200 Mbit/s of bandwidth. Valid values: 200 to 5000. Unit: Mbit/s. |The basic price covers 2000 Mbit/s of bandwidth. Valid values: 2000 to 20000. Unit: Mbit/s. |The peak cross\-VPC traffic that can be protected.<br><br>Extra fee: USD 0.8 for each 1 Mbit/s of additional bandwidth. |
|Additional Policy |The basic price covers the following number of access control policies for each type of firewall:<br><br>Internet firewall: 4,000.<br><br>Valid values for an additional quota: 0 to 100000. |The basic price covers the following number of access control policies for each type of firewall:<br><br>Internet firewall: 10,000.<br><br>VPC firewall: 10,000.<br><br>Valid values for an additional quota: 0 to 200000. |The basic price covers the following number of access control policies for each type of firewall:<br><br>Internet firewall: 20,000.<br><br>VPC firewall: 20,000.<br><br>Valid values for an additional quota: 0 to 300000. |The Quota for Additional Policy that can be protected.<br><br>Extra fee: USD 0.02 per month for each additional access control policy in this tier. |
|Additional Domain Access Blocking Policy |The basic price does not cover this specification. Valid values for an additional quota: 0 to 10000. |The basic price does not cover this specification. Valid values for an additional quota: 0 to 20000. |The basic price does not cover this specification. Valid values for an additional quota: 0 to 50000. |The Quota for Additional Domain Access Blocking Policy that can be protected.Extra fee: USD 0.6 per month for each additional domain access blocking policy. |
|Storage capacity for log analysis |The basic price does not cover this specification. Valid values: 1000 to 500000. Unit: GB. |The basic price does not cover this specification. Valid values: 1000 to 500000. Unit: GB. | |Extra fee: USD 80 per 1,000 GB\-month. |


<span id="99247b68"></span>
### **Pricing example**

Take a Enterprise Edition as an example. The protected internet traffic bandwidth is 100 Mbps.Storage capacity for log analysis is 2000GB. The total monthly cost for your configuration for one month is USD $1960 , which is the sum of the following items.


* USD $1450 for Premium Edition

* USD $350 for 50 Mbit/s of additional bandwidth ：（100\-50）\* USD $7 = USD $350

* USD $160 for 2000GB storage capacity for log analysis：2 \* USD $80 = USD $160
