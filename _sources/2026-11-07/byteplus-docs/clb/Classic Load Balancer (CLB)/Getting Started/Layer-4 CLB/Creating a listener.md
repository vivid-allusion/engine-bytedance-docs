---
title: "Creating a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-04"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

Add a listener and backend server group to enable the CLB instance to listen to requests from TCP port 80.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Configure only parameters listed in the following table, and retain default values for other parameters. If you need to learn more about parameters, refer to <a href="https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener">User Guide \> Creating a TCP listener</a>.</div>



1. On the CLB instance list page, click **Configure Listener** to the right of the instance name "clb01" to access its listener details page.

2. Click **Add Listener** button, then configure the **Protocol & Listening** settings based on the table below.

   
   |Name |Explaination |Recommended Value |
   |---|---|---|
   |Listener name |Configure the listener name. If this parameter is not specified, the system sets it to **Protocol\-Port** by default, for example, **TCP\-80**. |listener01 |
   |CLB protocol |Select the protocol type for CLB instance listening. |TCP |
   |Listening port |Specify the listening port. The listener will distribute access requests from this port to the backend server group. |80 |
   |Scheduling algorithm |Specify the rule for forwarding requests accessing TCP port 80 by this listener. |Weighted Round Robin (WRR) |
   |Timeout Period |When no requests to access TCP port 80 are received within the timeout period, the CLB instance will automatically release the connection. |900 seconds |
   

3. Click **Next** button to configure the **Server Group**.

   Select the created backend server group group01.

4. Click **Next** and configure **Health Check** parameters (use default values as shown).

5. Click **Next**, and review the configuration on the **Configuration Review** page to verify accuracy.

   * If the configuration is incorrect, click **Previous** to modify the settings.

   * If the configuration is correct, click **Confirm ** button to complete the actions.


You have now configured a CLB instance with the traffic forwarding and health check features.
