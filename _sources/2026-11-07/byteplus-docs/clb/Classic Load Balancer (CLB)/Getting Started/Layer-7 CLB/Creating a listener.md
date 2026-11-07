---
title: "Creating a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-04"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

Enable the CLB instance to listen to requests from the HTTPS port 443.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Configure only parameters listed in the following table, and retain default values for other parameters. If you need to learn more about more parameters, refer to the <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener">User Guide \> Creating an HTTPS listener</a>.</div>



1. On the instances list page, click **Configure Listener** to the right of the instance clb01 to access the listener details page.

2. Click **Add Listener**, and refer to the table below to configure the basic configuration for **Protocol & Listening**.

   
   |Name |Explaination |Recommended Value |
   |---|---|---|
   |Listener name |Configure the listener name. If this parameter is not specified, the system sets it to **Protocol\-port** by default, for example, HTTPS\-443. |listener\-1 |
   |CLB protocol |Select the protocol type for CLB instance listening. |HTTPS |
   |Listening port |Specify the listening port. The listener will distribute access requests from this port to the backend server group. |443 |
   |Scheduling algorithm |Specify the rule that the listener observes when forwarding requests to the HTTPS port 443. |Weighted Round Robin (WRR) |
   

3. Configure the timeout period by referring to the table below.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Client connection idle timeout period |Input the long connection timeout period between the client and CLB. If there is no access request within the timeout period, CLB will terminate the current connection until a new connection is established when the next request arrives. |75 seconds |
   |Client request header timeout period |Input the timeout period for reading the client's request header. The client initiates a request to the CLB. If the client does not transmit the entire header within the timeout period, the CLB will return a 408 error code to the client, indicating that the request has timed out. |60 seconds |
   |Client request body timeout period |Input the timeout period for reading the client request body. The client initiates a request to the CLB. If the client does not send any request body within the timeout period, the CLB will return a 408 error code to the client, indicating that the request timed out. |60 seconds |
   |Client forwarding response timeout period |Input the timeout period for CLB to send responses to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be disabled. |60 seconds |
   |Backend response timeout period |Input the timeout period for CLB to read the response from the backend server. CLB initiates a request to the backend server. If the backend server receiving the request does not respond within the timeout period, it will disable this connection. |60 seconds |
   |Backend server request forwarding timeout period |Input CLB to transmit requests to backend server's timeout period. CLB sends requests to the backend server, and if the backend server does not receive any content within the timeout period, this connection will be disabled. |60 seconds |
   |Backend server connection timeout period |Input the connection establishment timeout period between CLB and the backend server. If the connection between the CLB and the backend server is not established within the timeout period, terminate the connection establishment action. |4 seconds |
   

4. Click **Next** to configure the SSL certificate.

   On the SSL certificate configuration page, select the server certificate.

5. Click **Next** to configure the default backend server group.

   Select the created server group **group01**.

6. Click **Next** and configure health check parameters (use default values as shown).

7. Click **Next**, and review the configuration on the **Configuration Review** page to verify accuracy.

   * If there are configuration errors, click **Back** to modify.

   * If everything is correct, click **Confirm** to complete the action.


You have now configured a CLB instance with the traffic forwarding and health check features, and all inbound requests are forwarded according to the default forwarding rules.
