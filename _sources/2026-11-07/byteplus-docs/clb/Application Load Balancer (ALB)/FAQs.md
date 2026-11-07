---
title: "FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/FAQ"
---

This topic describes common questions about Application Load Balancer (ALB).

<span id=".YWxiLeacgOWkp-inhOagvOWunuS-i-WPr-S7peaUr-aMgeWkmuWwkeW5tuWPkeivt-axgu-8nw=="></span>
## What is the maximum concurrent request capacity supported by the largest ALB instance?

ALB instances are not categorized by specifications. You do not need to worry about specification limits or usage. ALB instances auto\-scale to handle fluctuations in your application traffic.

<span id=".YWxiLeWFrOe9keWunuS-i-aYr-WQpuaUr-aMgeiwg-mrmOWFrOe9keW4puWuveS4iumZkO-8nw=="></span>
## Does the public ALB instance support increasing its internet bandwidth cap?

Yes, supported. You can access the [EIP console](https://console.byteplus.com/eip) to adjust the bandwidth for the ALB's EIP. For procedure, see [Changing the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

<span id=".YWxiLeWunuS-i-Wfn-WQjeino-aekOWIsOWkmuS4quWPr-eUqOWMuuS4iu-8jOa1gemHj-aYr-Wdh-WIhueahOWQl--8nw=="></span>
## When an ALB instance domain is resolved to multiple availability zones, is the traffic evenly distributed?

Yes. After you create an ALB instance, the system automatically assigns an instance domain to it. You can configure the ALB instance domain as a CNAME record for your business domain in your DNS to integrate the ALB. When the ALB instance is deployed across multiple availability zones (AZs), its instance domain resolves in a round\-robin manner to the instance IPs in each AZ.

<span id=".YWxiLeWunuS-i-aYr-WQpuaUr-aMgeS9v-eUqOaMh-WumueahOWFrOe9kWlw77yf"></span>
## Does the ALB instance support using a designated Elastic IP address (EIP)?

Yes, supported. You can flexibly associate or disassociate EIPs for ALB instances. Associating an EIP to a private ALB instance converts it to public. Disassociating the EIP from a public instance converts it back to private. For procedure, see [Changing network type for an ALB instance](https://docs.byteplus.com/docs/clb/Associating-and-disassociating-an-elastic-IP).

<span id=".YWxiLeWFrOe9kWlw5piv5ZCm5pSv5oyB5Yqg5YWl5YWx5Lqr5bim5a695YyF77yf"></span>
## Does the ALB's EIP support being added to a Bandwidth Package?

Yes, supported. You can go to the [EIP console](https://console.byteplus.com/eip) to add the ALB EIP to a bandwidth package. For detailed steps, see [Adding an EIP to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package).

<span id=".YWxiLeaYr-WQpuaUr-aMgS13ZWJzb2NrZXQt5Y2P6K6u77yM5aaC5L2V5byA5ZCvLXdlYnNvY2tldC3ljY_orq7vvJ8="></span>
## Does the ALB support the WebSocket protocol, and how can I enable the protocol?

Yes, supported. The ALB HTTP listener supports WebSocket protocol access by default. The HTTPS listener supports the WebSocket Secure protocol by default. No additional action is required to enable the WebSocket protocol.

<span id=".YWxiLeWQjOS4gOS4quebkeWQrOWZqOaYr-WQpuaUr-aMgemFjee9ruWkmuS4quWfn-WQjeivgeS5pu-8nw=="></span>
## Does a single ALB listener support configuring multiple domain certificates?

Yes, supported. The ALB supports the multi\-domain certificate feature. You can configure up to 20 domain certificates for the same HTTPS listener. For procedure, see [Configuring multiple certificates for a HTTPS listener (Basic)](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener) or [Configuring multiple certificates for a HTTPS listener (Standard)](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition).

<span id=".YWxiLeaYr-WQpuWPr-S7peiOt-WPluWIsOWuouaIt-err-a6kGlw77yf"></span>
## Can the ALB obtain the client source IP?

Yes. The ALB inserts the client's real IP address into the X\-Forwarded\-For field of the HTTP header. The first IP address in this field is the real client source IP.

<span id=".YWxiLeWvueWuouaIt-err-ivt-axgmJvZHnlpKflsI_mmK_lkKblrZjlnKjpmZDliLbvvJ8="></span>
## Does the ALB limit the body size of the client request?

Yes. Through custom configuration, you can adjust the client request body size limit, supporting up to 30 GiB. For procedure, see [Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations).

<span id=".YWxiLeaYr-WQpuaUr-aMgS10bHN2MS0y77yf"></span>
## Does the ALB support TLSv1.2?

Yes, supported. You can select the TLS protocol version and encryption suite through custom configuration. For procedure, see [Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations).

<span id=".YWxiLeaYr-WQpuaUr-aMgeiwg-aVtOi2heaXtuaXtumXtO-8nw=="></span>
## Does the ALB support adjusting the timeout period?

Yes, supported. Through custom configuration, you can adjust the timeout period for interactions between the client and the ALB, as well as between the ALB and the backend server. For procedure, see [Custom configuration](https://docs.byteplus.com/docs/clb/Custom-configurations).

<span id="3e90fcc4"></span>
## Does the ALB support compression?

Yes, supported. ALB supports gzip compression by default. No manual activation is required. Brotli compression is currently not supported.


* If a client request includes `Accept-Encoding: gzip`, ALB will perform gzip compression on the backend response content. If the request does not contain `Accept-Encoding: gzip`, ALB will not compress the response.

* Supported compressed content types: `text/plain`, `text/css`, `text/xml`, `application/xml`, `text/javascript`, `application/x-javascript`, `application/json`, `application/javascript`, `application/x-protobuf`, and `application/octet-stream; ssmix=a`.

* ALB compression does not apply in the following scenarios.

   * If the response returned by the backend server is already compressed, ALB will not perform secondary compression.

   * The compression feature will not take effect on the response content of 200B or less. ALB only compresses response content when its size exceeds 200B. 

   * ALB does not currently support brotli compression. If a client request includes `Accept-Encoding: br`, ALB will not compress the backend response content.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Compression alters the MD5 hash of the content. If the backend server has an MD5 verification mechanism configured and the client needs to verify the MD5 value of the original response, ensure that the client request header does not contain <code>Accept-Encoding: gzip</code> to avoid MD5 verification failure.</div>


<span id="1dd7ece2"></span>
## Does the ALB support the QUIC protocol?

Standard ALB instances support QUIC listeners. If you need a trial, please contact your account manager. For details, see [Creating a QUIC listener](https://docs.byteplus.com/docs/clb/Creating-a-QUIC-listener).

<span id="17bf4508"></span>
## Does the ALB support IPv6 client access?

Yes, supported. The ALB allows authorized users to create dual\-stack IPv4&IPv6 instances that forward IPv4 and IPv6 client traffic to IPv4 backend servers. For more information, see [Implementing IPv4+IPv6 traffic load balancing via ALB](https://docs.byteplus.com/docs/clb/ALB-achieves-load-balancing-of-IPv4-IPv6-traffic).

To create a dual\-stack instance, please contact your account manager.

<span id="4e2234c2"></span>
## Does the ALB support the feature of obtaining the client source IP?

Yes, supported. You can configure the backend server to obtain the client's real IP address through X\-Forwarded\-For. For more information, see [Obtaining client source IP via backend server](https://docs.byteplus.com/docs/clb/Configuring-back-end-servers-for-retrieving-client-IP-addresses).

<span id="AcT3M8V2"></span>
## **If the account associated with an ALB instance on BytePlus is overdue, will charges still be incurred?** 

Yes. If the account associated with an ALB instance is overdue but the ALB instance is still operating normally, charges will continue to be incurred. Charges stop only after the ALB instance enters the "Stopped" state.

If you still need to use the ALB instance, please Recharge your account promptly. If you no longer need it, it is recommended to delete the ALB instance as soon as possible.

<span id="1WaXIvxh"></span>
## Does ALB support configuring certain domains to directly return a 403 status code?

The Standard Edition ALB forwarding rules can specify a domain name and set the forwarding action to return a fixed response (e.g., a 403 status code). When a client accesses that domain name, the ALB will directly return the preset response content. For instructions, see [Creating a forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition).

<span id="SraTQv0s"></span>
## Why can't IAM users view monitoring data?

If an IAM user is only granted ALB permissions but not CloudMonitor permissions, they will be unable to view the ALB service's monitoring data. Please use the root user (to which the IAM user belongs) to add the system\-predefined CloudMonitor policy permissions to the IAM user according to your actual needs.


|Policy name |Supported action |
|---|---|
|CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
|CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |


&nbsp;
