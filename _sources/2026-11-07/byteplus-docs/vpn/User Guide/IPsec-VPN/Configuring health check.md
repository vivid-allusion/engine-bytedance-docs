---
title: "Configuring health check"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configure-health-check"
---

The IPsec\-VPN connection supports the health check feature. After configuring health check, the system promptly detects exceptions in the IPsec\-VPN connection tunnel. It reports related events via Cloud Monitor's health check. This helps you identify tunnel connectivity issues early, preventing business disruptions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Health check is not supported when the IPsec\-VPN connections are associated with the Transit Router (TR) or the dual\-tunnel VPN gateway.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* If the associated resource of the IPsec\-VPN connection to be configured with health check is VPN gateway, ensure that the VPN gateway is the latest version. If not, upgrade the VPN gateway first. For specific actions, see Upgrading a VPN gateway.

* Currently, IPsec\-VPN connections with associated resources as TR do not support configuring the health check. If needed, please create a new IPsec\-VPN connection.

* If a health check is configured for an IPsec\-VPN connection, you need to configure a remote IP that can respond to ICMP packets for the health check probe.

* Ensure that you have pre\-planned the IP addresses for the health check. **The source IP for the health check cannot be any IP address within the VPC that communicates over this IPsec connection and is scheduled to be occupied**. Otherwise, traffic through the VPN gateway may become unreachable.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5pa55byP5LiA77ya5Yib5bu6SVBzZWPov57mjqXml7bphY3nva7lgaXlurfmo4Dmn6U="></span>
### Method 1: Configure health check when creating IPsec\-VPN connection

You can directly configure the health check when creating an IPsec\-VPN connection. Here, we only introduce parameters related to the health check. For more information, please refer to Creating an IPsec\-VPN connection.


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **Create VPN Connection**.

4. After completing the basic parameter configuration, configure Health check under Advanced options.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Source IP |A Source IP is the IP address on the local VPC side. It can be accessed by the on\-premises data center or peer VPC via IPsec\-VPN connection.<br><br><br>* Do not support IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8`.<br><br>* When you need to enable the health check for multiple IPsec\-VPN connections under the same VPN gateway, please use different source IP addresses for differentiation.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not use IPs already occupied or reserved within the VPC (such as subnet gateway IPs) as source IPs, as this may cause traffic through the VPN gateway to become unreachable.</div><br> |172.16.10.10 (Unoccupied) |
   |Destination IP |A Destination IP is the IP address on the on\-premises data center or peer VPC side. It can be accessed by the local VPC via IPsec\-VPN connection.<br><br><br>* IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8` are not supported.<br><br>* The destination IP cannot be the same as the source IP. |172.16.5.10 (unoccupied) |
   |Detection interval |The time interval for performing health checks.<br><br><br>* The value ranges from 1 to 300 in seconds.<br><br>* The interval defaults to 3 seconds, which means a health check is performed on the destination IP every 3 seconds. |3 |
   |Response timeout |The maximum duration to wait for a response from a health check probe.<br><br><br>* If the destination IP does not properly respond within the specified time, the health check is determined to be Abnormal.<br><br>* The response timeout must not be longer than the probe interval. |2 |
   |Healthy threshold |The number of checks for determining the health status is normal.<br><br><br>* If the health check is performed consecutively for the specified number of times and all the results are **Normal**, the IPsec\-VPN connection is considered to be **Normal** in health check status.<br><br>* The value ranges from 1 to 10, and defaults to 3 times. |3 |
   |Unhealthy threshold |The number of checks for determining the health status is Abnormal.<br><br><br>* If consecutive health checks on an IPsec\-VPN connection fail for the specified number, the connection is declared Abnormal.<br><br>* The value ranges from 1 to 10, and defaults to 3 times. |3 |
   

5. After completing the configuration, click **Create**. The health check will take effect immediately after the IPsec\-VPN connection is created.


<span id=".5pa55byP5LqM77yaSVBzZWPov57mjqXliJvlu7rlkI7phY3nva7lgaXlurfmo4Dmn6U="></span>
### Method 2: Configure health check after IPsec\-VPN connection creation

If you did not configure a health check when creating the IPsec\-VPN connection or need to modify the health check settings, use this method.


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. In the IPsec\-VPN connection list, click the name of the target IPsec\-VPN connection.

4. In the Health check zone at the bottom of the Overview page, click Edit.

5. In the pop\-up dialog box, click Add Probe IP to configure health check arguments, and click Authorize once the configuration is complete.

   For details of the relevant parameters, refer to step 4 in Method 1: Configure the health check when creating the IPsec\-VPN connection.


<span id=".55u45YWz5pON5L2c"></span>
## Related actions

After configuring the health check for the IPsec\-VPN connection, if you no longer need the health check feature, you can directly click the IPsec\-VPN connection name in IPsec\-VPN connection list on the IPsec\-VPN connection console, and delete all health check probe IPs in Health check zone at the bottom of Overview page.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateVpnConnectionHealthCheckers](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnectionHealthCheckers): Create health check for IPsec\-VPN connection.

* [ModifyVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionHealthChecker): Modify health check configuration for IPsec\-VPN connection.
