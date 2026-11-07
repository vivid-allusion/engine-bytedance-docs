---
title: "Why can't instances connect via public network address, or why do commands executed after connecting via public network address get stuck?"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/command-execution-failure-via-public-address"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem


* After enabling public network access, connecting to instance via its public network address fails.

* After successfully connecting to instance via public network address, commands (for example, `show dbs`) executed get stuck.


<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible cause

Public network bandwidth has reached its peak, preventing connection to instances via public network address or causing commands to get stuck after connecting.

<span id=".5aSE55CG5pa55rOV"></span>
## Solution

Log in to [EIP Console](https://console.byteplus.com/eip/region:eip+cn-beijing/eips), and locate the public IP that the target MongoDB instance's public network address is associated with. View the public IP's bandwidth monitoring data (such as outbound and inbound bandwidth) to confirm if bandwidth usage has reached its peak.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To view EIP monitoring data, refer to <a href="https://docs.byteplus.com/en/docs/eip/Viewing-monitoring-data">Viewing monitoring data</a>.</div>


If bandwidth usage has reached its peak, you can try the following solutions:


1. If bandwidth usage occasionally peaks, find the time of the peak in the public IP's monitoring data chart and investigate if there are any abnormal operations in your business during that period.

2. If bandwidth usage continuously peaks, adjust the bandwidth limit. To adjust the bandwidth limit, refer to [Modifying maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

3. If the problem persists after trying above suggestions, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.
