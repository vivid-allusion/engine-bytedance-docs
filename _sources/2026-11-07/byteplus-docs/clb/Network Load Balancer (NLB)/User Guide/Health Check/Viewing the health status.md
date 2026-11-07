---
title: "Viewing the health status"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Viewing-the-health-status"
---

<span id="lS5c1qcc"></span>
## Action description


|Status |Explanation |
|---|---|
|Available |All backend servers in the server group are normal. |
|Abnormal |There are abnormal backend servers within the server group. |
|Not enabled |Health check is not enabled for the server group. |
|No target |No backend server is configured in the server group. |


<span id="lS5c1qcc"></span>
## Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the NLB instance name to access the NLB details page.

4. On the Listeners tab, view the health status of listener.

5. Click the Exception tag to view details of abnormal backend servers.

   * Based on the prompt, you can learn the number of abnormal servers and preliminary troubleshooting methods. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL)

   * Click the server name to go to the ECS instance details page and view detailed information about the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">While viewing, health check status updates may display with a delay, which requires to manually refresh the page to view the latest status.   </div>
   

6. (Optional) If you need to temporarily remove a faulty server, see Removing a backend server.


<span id="E7MjH9tR"></span>
## Related documents


* [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups)

* [DescribeNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroupAttributes)
