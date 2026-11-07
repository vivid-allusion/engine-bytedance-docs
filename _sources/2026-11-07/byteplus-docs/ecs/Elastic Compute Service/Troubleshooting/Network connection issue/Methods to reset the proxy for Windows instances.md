---
title: "Methods to reset the proxy for Windows instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_resetting_the_proxy_in_a_Windows_instance"
---

To handle service access failure after proxy settings are modified by malicious software, you can reset the network proxy. This topic describes how to reset the network proxy service.

In this example, 2022 Datacenter Edition 64\-bit Chinese is used for illustration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Operations may vary by version. The actual version shall prevail.</div>


* <div data-tips="true" data-tips-type="tip">This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.</div>



<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Since certain malicious software may change the Internet Explorer proxy setting, this prevents you from accessing Windows update sites or any Microsoft security site.

<span id=".5pON5L2c6K-05piO"></span>
## Usage note


* Improper modification of the Windows Registry may cause severe system issues. We recommend that only personnel with a basic understanding of the Windows operating system perform such modifications.

* To prevent system issues or data loss caused by incorrect registry operations, make sure to back up data on both the system volume and data volume before modifying the registry, for example, by [creating a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. In the search box at the lower left corner of the desktop, enter "Run".

3. In the "Run" dialog box, enter the following content, and click the "OK" button.

   `reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings /v ProxyEnable /t REG_DWORD /d 0 /f`

4. Reopen the "Run" dialog box and enter the following content.

   `reg delete HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings /v ProxyServer /f`

5. Click the "OK" button to complete the operation.
