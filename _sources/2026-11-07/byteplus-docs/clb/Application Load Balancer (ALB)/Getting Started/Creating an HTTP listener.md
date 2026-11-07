---
title: "Creating an HTTP listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Creating-an-HTTP-listener"
---

After completing server group creation and adding servers, you need to configure a listener for the ALB instance by specifying the listener port and protocol, then associate the server group with this listener. In the simulated scenario of the [Quick Start](https://docs.byteplus.com/docs/clb/ALB-quick-start-Overview) guide, you can configure an HTTP listener for the ALB instance using port 80. The instance will communicate with clients via the HTTP protocol.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the Listeners tab, click Add listener.

5. On the **Add listener** tab, configure the basic listener information as shown below. For more field information and configuration instructions, see [Listeners > Create HTTP Listener](https://docs.byteplus.com/docs/clb/Creating-HTTP-listener).

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Name |Enter the listener name. If left blank, it defaults to protocol\-port. |HTTP\-80 |
   |Listening protocol |Select the listener protocol. |HTTP |
   |Listening port |Enter the listening port. Port range: 1 to 65535. |80 |
   |Access control |Enable access control. By configuring access control policy groups, you can filter and screen visitors to restrict access sources, effectively preventing malicious requests.<br><br>You must choose either a denylist or allowlist for the policy group—they cannot be configured simultaneously.<br><br><br>* Denylist: IP addresses within the selected policy group will be denied access to the listener.<br><br>* Allowlist: Only IP addresses within the selected policy group will be permitted access to the listener. |Do not enable |
   

6. Click **Next: Default Server Group** and select the newly created server group **alb1group1** as the default server group. When client requests do not match any custom forwarding rules, ALB will route them to this default server group.

7. Click **Next: Confirm configuration**. After verifying the configuration details, click **Configure** to complete the operation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">At this point, you have completed the basic ALB listener and forwarding configuration following the Quick Start workflow. When clients send requests to the EIP of the alb1 instance, the system will use the Weighted Round Robin (WRR) algorithm to distribute requests across the two backend servers in the alb1group1 server group. This effectively balances the load on backend servers and enhances overall service stability.</div>


* <div data-tips="true" data-tips-type="tip">If your service is exposed via a domain name, you can configure ALB's EIP as the DNS A record for your business domain. Requests to the domain will then be routed through the DNS system to the ALB instance, simplifying service operation and management.</div>



&nbsp;

&nbsp;

&nbsp;
