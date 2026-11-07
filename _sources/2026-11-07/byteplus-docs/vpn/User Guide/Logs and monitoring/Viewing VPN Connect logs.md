---
title: "Viewing VPN Connect logs"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Viewing-IPsec-VPN-connection-logs"
---

The service supports viewing IPsec\-VPN connection and SSL\-VPN server logs via Torch Log Service (TLS), helping you troubleshoot VPN Connect issues on your own using these logs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If Connection Log is disabled for all​ VPN Connect in the same region, and no new​ VPN Connect Log is enabled within 30 days, the corresponding log topic will be automatically deleted.</div>


* <div data-tips="true" data-tips-type="default">SSL VPN connection log function is in beta testing. Please contact your account manager to activate it if needed.</div>



<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Term |Description |
|---|---|
|Torch Log Service |A one\-stop service provided by the platform for log data, offering functionalities such as log collection, massive storage, search and analysis, monitoring and alerting, and data visualization. |
|Log Project |A log project is the fundamental resource management unit within TLS, used to isolate and control access to log resources across multiple users, projects, or products. |
|Log Topic |A log topic is the carrier object for log information and the basic unit for log management (e.g., collection, storage, query, and analysis) in TLS. |


<span id=".5pON5L2c5YmN5o-Q"></span>
## Prerequisites

The VPN Connect Log feature depends on TLS. Before using it, ensure that TLS is enabled.

<span id=".5q2l6aqk5LiA77ya5byA6YCa6Leo5pyN5Yqh6K6_6Zeu5o6I5p2D"></span>
## Step 1: Enable cross\-service authorization


1. Log in to [the VPN Connect console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **VPN Connection** or **SSL VPN Server**.

4. Hover your mouse over **View Logs**​ in the Actions​ column for the target instance. In the tooltip that appears, click **Authorize**​. This will automatically navigate you to the cross\-service access request page.

5. Click **Authorize** to complete cross\-service access authorization.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you delete cross\-service access authorization later, VPN Connect with the connection log feature enabled will be unable to deliver logs normally.</div>


<span id=".5q2l6aqk5LqM77ya5byA5ZCvSVBzZWPov57mjqXml6Xlv5c="></span>
## Step 2: Enable VPN Connect Log


1. Log in to [the VPN Connect console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **VPN Connection** or **SSL VPN Server**.

4. In the instance list, hover over **View Logs** to the right of the target instance, then click **Enable** in the tooltip.

5. In the pop\-up dialog box, click **Enable Log** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5p-l55yLSVBzZWPov57mjqXml6Xlv5c="></span>
## Step 3: View VPN Connect logs


1. Log in to [the VPN Connect console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **VPN Connection** or **SSL VPN Server**.

4. Click **View Logs** to the right of the target instance. You can then adjust the log time range to view logs from the corresponding period.

   The VPN Connect logs are displayed as key\-value pairs, i.e., {key: value}. The fields contained in the logs and their meanings are as follows:

   
   |Field |Description |
   |---|---|
   |`__path__` |A reserved field for the original log. For IPsec Connection Log, `__path__` is fixed as `ipsec.log`. |
   |`__source__` |A reserved field for the original log. For IPsec Connection Log, `__source__` is fixed as the ID of the current IPsec\-VPN connection. |
   |`message` |The detailed text of the log. |
   |`vpn_connection_id` |The ID of the IPsec\-VPN connection. |
   |`vss_id` |The ID of the SSL\-VPN connection. |
   |`tunnel_id` |The tunnel ID of the dual\-tunnel IPsec\-VPN connection. |
   


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After you obtain the SSL\-VPN connection logs, you can match the log keywords to find corresponding troubleshooting methods. For details, see <a href="https://docs.byteplus.com/en/docs/vpn/SSL-VPN-connection-FAQs">How to troubleshoot common errors by checking the SSL\-VPN connection server logs</a>.</div>
