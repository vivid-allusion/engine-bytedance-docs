---
title: "Viewing the health check status"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Viewing-the-health-check-status"
---

<span id="13NofM3m"></span>
## Procedure


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Check the number of listeners with abnormal health check results in the Classic Load Balancer (CLB) instance list.

4. Click the Classic Load Balancer instance name to enter the **Listener** tab.

5. In the **Health Check Status** column, click the **Abnormal** tag to view the details of the abnormal backend servers.

   * Based on the prompt, you can learn the number of unhealthy servers and preliminary troubleshooting methods. For detailed configuration steps, refer to [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group) and [Configuring route entries for the secondary network interface](https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface).

   * You can click a server name to view the detailed information of the Elastic Cloud Server (ECS) instance.

   * If the listener is a Layer\-7 listener, you can also check the number of forwarding rules associated with the faulty backend server group.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">While viewing, health check status updates may display with a delay, which requires to manually refresh the page to view the latest status.   </div>
   

6. (Optional) If you need to temporarily remove a faulty server, refer to [Removing a backend server](https://docs.byteplus.com/en/docs/clb/Modifying-the-server-group).


<span id=".55u45YWz5paH5qGj"></span>
## Related document


* [DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes)

* [DescribeListenerHealth](https://docs.byteplus.com/en/docs/clb/DescribeListenerHealth)
