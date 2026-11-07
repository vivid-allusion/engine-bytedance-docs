---
title: "Creating O11yAgent endpoints"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/creating_o11yagent_privatelink"
---

The O11yAgent collection add\-on supports accessing the plugin management platform via [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01) to enable add\-on status display, upgrade, and other features. This topic describes how to configure PrivateLink connections for the O11yAgent collection add\-on.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the BytePlus account (root user) to configure and use this feature. When an IAM user creates an endpoint, it may be unable to select an available endpoint service. For details, see <a href="https://docs.byteplus.com/en/docs/privatelink/FAQs">PrivateLink FAQs</a>.</div>


<span id="TrhKCk8A"></span>
## Background

By default, the O11yAgent collection add\-on allows you to access the add\-on management platform by using `the CIDR block 100.xxx.xxx.xxx`. The platform achieves features, such as add\-on status display and add\-on upgrade.

In some scenarios, the O11yAgent collection add\-on may be unable to access `the add-on management platform by using the `100.xxx.xxx.xxx CIDR block caused by CIDR block conflicts or other reasons. In this case, you can configure PrivateLink connections for the O11yAgent collection add\-on and use PrivateLink to upgrade the add\-on and achieve other features.

The following figure shows the technical principle of the O11yAgent collection add\-on using PrivateLink.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2032538d4ee5513c64b5b118b0d58dc.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about PrivateLink, see <a href="https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01">What is PrivateLink?</a></div>


<span id="M9fLzYho"></span>
## Considerations


* Fees are incurred for using PrivateLink, and additional bills are generated for creating endpoints. For details, see [Billing Overview](https://docs.byteplus.com/en/docs/privatelink/Billing-rules).

* You need to open Port `443` for the security group of the endpoint. Otherwise, access may fail.


<span id="8Bd7E7J0"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, select ECS.

3. In the drop\-down list above the ECS instances list, select **O11yAgent endpoint**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fca6cdff80e2ac9fa50cbbeb00679e7c.png) </span>

4. In the pop\-up dialog box, click **Create endpoint** and configure the endpoint information. For more configurations and detailed parameter descriptions, see [Creating interface endpoints](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02).

   * **Basic information**: Select the region where the endpoint is located, specify a name for the endpoint, and then select the **Interface** type.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56b2c183739d7a2fa7d302707ef5a505.png) </span>

   * **Endpoint Service**: Select **BytePlus service** for the **Add method** parameter, and select the service that corresponds to the O11yAgent add\-on for the **Endpoint Service** parameter. The name of the service is in the format of `com.volces.privatelink.<region-id>.o11yagent-platform`, where `<region-id>` indicates the region ID of the service.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can use the <code>o11yagent-platform</code> keyword to search for the service that corresponds to the O11yAgent add\-on from the service list.      </div>
      

   * **Network configuration**: Select your VPC, availability zone, subnet, and security group.

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After you configure the endpoint, the O11yAgent add\-on in this VPC will access the add\-on management platform by using the endpoint. The O11yAgent add\-on in other VPCs still directly accesses the add\-on management platform by the <code>100.xxx.xxx.xxx</code> CIDR block.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You need to open Port <code>443</code> for the security group of the endpoint. Otherwise, access may fail.      </div>
      

   * **Advanced options**: When you create an endpoint for the first time, you need to **enable** Private DNS name. When you delete the endpoint and reconfigure it, you do not need to **enable** this configuration.

5. Click **Buy now** and check again to complete the configuration.


<span id="koNdnIgv"></span>
## Verifying results

<span id="1nAevtvJ"></span>
### Viewing connection status

After the endpoint is configured, you can view the connection status in the endpoint list. If **Connected** is displayed in the **Connection status** column that corresponds to the endpoint, the connection is successful. In this case, the O11yAgent add\-on can access the add\-on management platform by using the endpoint.

You can also view the status of the corresponding endpoint in the Cloud Monitor console.

<span id="x0ZoGxRy"></span>
### Testing network connectivity


1. Log in to the [endpoint console](http://console.volcengine.com/pl).

2. In the endpoint list, find the target endpoint and click the name of the endpoint to go to the endpoint details page. On the **Overview** tab, view the domain name of the endpoint.

3. In an ECS instance within the VPC bound to the endpoint, run the following command to check whether the endpoint, domain name, and network are in normal status.

   ```bash
   ping ep-2byzj***.o11yagent-platform.cn-shanghai.privatelink.volces.com
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The endpoint domain name in the preceding code is used for illustration purposes only. In actual use, replace the domain name in the code with your endpoint domain name.   </div>
   

   The expected result is as follows: If you can successfully ping the endpoint domain name, the network is connected.

   ```bash
   PING ep-2byzj***.o11yagent-platform.cn-shanghai.privatelink.volces.com (192.168.0.4): 56 data bytes
   64 bytes from 192.168.0.4: icmp_seq=0 ttl=46 time=0.053 ms
   64 bytes from 192.168.0.4: icmp_seq=1 ttl=46 time=0.122 ms
   64 bytes from 192.168.0.4: icmp_seq=2 ttl=46 time=0.055 ms
   64 bytes from 192.168.0.4: icmp_seq=3 ttl=46 time=0.079 ms
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99fcfbee4aefed5da6e9606219e0df27.png) </span>


&nbsp;

&nbsp;

&nbsp;

&nbsp;
