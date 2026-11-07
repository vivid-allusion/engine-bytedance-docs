---
title: "Integrate LLM Application Firewall using a traffic-based approach"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Integrate_LLM_Application_Firewall_using_a_traffic-based_approach"
---

The traffic integration method is not affected by the business deployment location. After configuring the parameters for the LLM Application Firewall, you only need to modify the DNS records of the protected domain and allow traffic from the platform's origin IP addresses. This will connect the domain to the LLM Application Firewall.

<span id="b21b651a"></span>
## Background information

Integrating a website with the LLM Application Firewall using traffic redirection involves directing request traffic to the LLM Application Firewall for inspection, and then forwarding the inspected traffic to the origin server. In this mode, the firewall functions as an independent network middleware, deployed between the client and your large model application service, serving as the unified entry and exit point for all requests and responses.

The user request process is as follows:


1. **Traffic redirection**: Client requests sent to your LLM application are no longer delivered directly to the backend application, but are first routed to the LLM Application Firewall instance.

2. **Request/response inspection**: When the firewall receives a request, it performs protocol parsing. Then, using predefined security policies and intelligent models, it analyzes both the request content (prompt) and the response content (model\-generated result) to detect and assess threats such as prompt injection, sensitive information leakage, and model abuse.

3. **Real\-time decision\-making and actions**:

   * If a request or response does not trigger any protection policy, the traffic is allowed and forwarded to the backend large model application or the client.

   * If a threat is detected, the LLM Application Firewall will, in real time and according to the configured policies, take actions such as blocking the request or returning a custom response, thereby protecting your application.


<span id="bc491ac7"></span>
## Prerequisites


* You have already created a protection instance. For instructions, see[Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

* You have a registered domain for your application that has not yet been added to the LLM Application Firewall.


<span id="0837c6bf"></span>
## Step 1: Configure access parameters


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Asset management**, then click **Add asset**.

4. Select **Traffic integration** as the access method, and configure the access parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cd593120d75445e8a651864b137b6535) </span>

5. Click **Next**.


<span id="97433a16"></span>
## Step 2: Configure protection policy

After configuring the access parameters, you can directly set a protection policy for the current asset. The platform displays the default configuration of the protection policy, and the configuration is enabled.


* To complete the integration operation for the **console section**, simply submit the current configuration if no changes are required.

* To make modifications, adjust the relevant configuration directly on the current page. The modified and confirmed result will serve as the default configuration for the next access.


For a detailed introduction and configuration instructions for the corresponding strategy, refer to[Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).

<span id="dc8a9bcd"></span>
## Step 3: Allow back\-to\-origin IP addresses

After business integration, all requests will be returned to the origin server through the back\-to\-origin IP segment of the LLM Application Firewall. This results in an increased number of requests from each back\-to\-origin IP, which can easily trigger false blocking or rate limiting by security policies. Therefore, it is necessary to allow traffic for the origin IP range.

To ensure proper configuration when the origin server is protected by a firewall or security software, copy the back\-to\-origin IP addresses used by the LLM Application Firewall. Then, add these IP addresses to the firewall, access control list (ACL), or allowlist of the origin server, or to the allowlist of any other security software. This ensures that the back\-to\-origin IP is not affected by the origin server's security policies.

For detailed instructions on allowing back\-to\-origin IP addresses, see [Allow back-to-origin CIDR blocks](https://docs.byteplus.com/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks).

<span id="fca03866"></span>
## Step 4: Verify forwarding configuration

After successfully adding a protected domain name using the traffic\-based method, the LLM Application Firewall instance will forward requests received on the relevant ports to the corresponding ports of your origin server. To ensure your application remains available, we recommend verifying the forwarding configuration after integration. For detailed verification procedures, see [Verify forwarding configuration](https://docs.byteplus.com/docs/LLM-Application-Firewall/Verify_forwarding_configuration).

<span id="0550a4c2"></span>
## Step 5: Modify DNS resolution

After confirming that request forwarding is working correctly, you need to access the DNS provider for the web application, set the DNS record type to CNAME, and change the record value to the CNAME value of the LLM Application Firewall. After DNS resolution takes effect, the request traffic for the protected domain will be forwarded to the LLM Application Firewall. For detailed steps on modifying DNS resolution, see [Modify DNS resolution](https://docs.byteplus.com/docs/LLM-Application-Firewall/Modify_DNS_resolution).

<span id="e2c3a9e7"></span>
## What to do next


* **View protection details**: You can view security protection data on the **homepage**, including the number of requests, the number of protection events, as well as charts showing request trends and attack distribution. For more information, see [View the security overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_the_security_overview).

* **Analyze attack events**: When a request or response triggers a protection rule, the LLM Application Firewall generates a corresponding log entry in the **attack details** list to facilitate tracing and analysis of attack events. You can adjust or add protection rules based on attack event details and protection data, so that the detection results of the LLM Application Firewall better align with your business scenario. For example, request content that matches non\-high\-risk detection categories is only observed and not directly blocked, in order to prevent false positives. For more information, see [View details of attack events](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_details_of_attack_events).
