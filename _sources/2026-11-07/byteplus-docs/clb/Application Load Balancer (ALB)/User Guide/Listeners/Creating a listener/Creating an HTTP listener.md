---
title: "Creating an HTTP listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-HTTP-listener"
---

This topic introduces how to create an HTTP listener in the ALB console. HTTP listeners are suitable for scenarios that do not involve sensitive information transmission and require data content identification.

Each ALB instance must have at least one listener to function properly. A listener accepts client requests and distributes them to backend servers based on the forwarding rules and load balancing algorithms you configure. You can create multiple listeners under a single ALB instance and configure them with different listener protocols to handle client requests using different protocols.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

* You have [created the required server group](https://docs.byteplus.com/docs/clb/Server-groups-Overview).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the Listeners tab, click Add listener.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Name |Enter the listener name. Naming rules are as follows:<br><br><br>* Can contain English letters, Chinese characters, numbers, half\-width period (.), underscore (_), and hyphen (\-).<br><br>* Must start with an English letter or a Chinese character.<br><br>* Cannot start with http:// or https://.<br><br>* A maximum of 128 characters is allowed.<br><br>* If left blank, it defaults to **Protocol\-port**, such as **HTTP\-80**. |HTTP\-80 |
   |Listening protocol |Set the listening protocol to HTTP.<br><br>HTTP listeners support the WebSocket protocol by default and do not require additional enabling. |HTTP |
   |Listening port |Set the port for the listener. Valid range: 1\-65535.<br><br>The ports for different listeners under the same ALB instance must be unique. |80 |
   |Access control |Whether to enable the Access Control feature for the listener to allow or deny requests from specific clients.<br><br>If the access control feature is not enabled, requests from all clients will be allowed. |Check |
   |Control mode |Configure access control mode. After enabling Access Control, you must select access control mode.<br><br><br>* Allowlist: Only IP addresses within the selected policy group will be permitted access to the listener.<br><br>* Denylist: IP addresses within the selected policy group will be denied access to the listener. |Denylist |
   |Policy group |Select policy group. After enabling Access Control, you must configure a policy group.<br><br>A maximum of 5 policy groups can be selected. Each policy group can contain up to 300 IP address entries. Each IP address entry can be a single IP address or a CIDR block. For more information about policy groups, see [Access Control](https://docs.byteplus.com/docs/clb/Access-control). | |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: alb\-http<br><br>* Tag value: http\-80 |
   

6. Click **Next: default backend server group**.

7. On the **Default server group** tab, select the prepared server group from the dropdown, then click **Next: confirm the configuration**.

8. After confirming the listener configuration information is correct, click **Save**.


<span id="8f09a881"></span>
## What to do next


1. [Configure personalized settings](https://docs.byteplus.com/en/docs/clb/Custom-configurations): allows you to customize configuration items such as long connection retention time, timeout, maximum client request body size, custom response headers, and custom request headers.

2. [Configure forwarding rules](https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview): ALB distributes access traffic based on the forwarding rules you set for different traffic characteristics.


&nbsp;
