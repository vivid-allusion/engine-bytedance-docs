---
title: "Configure client rate limiting in proxy mode"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-rate-limiting"
---

In proxy mode, you can enable client rate limiting to control the rate of traffic from endpoints that access services through proxy gateways. This feature supports a global default rate limit and granular rate limiting policies for specific users or devices, helping allocate cluster bandwidth resources properly.

<span id="12329bfe"></span>
## Feature Overview

Client rate limiting in proxy mode is located in the advanced configuration of proxy policies. By configuring rate limiting policies, administrators can:


* **Prevent bandwidth abuse**: Limit the maximum access rate of a single endpoint to prevent individual users from consuming excessive public egress or gateway bandwidth.

* **Ensure differentiated service quality**: Configure different rate limits for employees in different roles, such as core business staff versus regular employees, to maintain performance for critical services.


<span id="0e4518c1"></span>
## Procedure


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation pane, choose **Zero Trust Access** \> **Proxy Policy**.

3. On the **Proxy Policy** page, click the **Advanced Settings** tab.

4. In the **Client Speed Limit** section, click **Edit**. In the panel that opens, click **Edit** again to change the settings.

5. Configure the global default rate limit, and click **Save** in the upper\-right corner of the page.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/rate-default.png) </span>

   * **Client Speed Limit**: After this option is enabled, the rate is limited based on the configuration below by default. If an employee rate limiting policy is configured, the employee policy takes precedence. This switch is disabled by default.

   * **Client upload speed limit KB/s**: Set the maximum rate at which endpoints send data to gateways. Enter 0 for no rate limit.

   * **Client download speed limit KB/s**: Set the maximum rate at which gateways send data to endpoints. Enter 0 for no rate limit.

6. To configure granular rate limiting rules for different employees, click **Add Strategy** in the **Employee Speed Limit Policy** section.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/rate-policy.png) </span>

7. In the **Add Strategy** dialog box, complete the following configuration.

&nbsp;

   
   |Configuration item |Description |
   |---|---|
   |**Policy name** |A custom name used to identify the policy. |
   |**Priority** |The policy execution order. The value range is 0 to 100. A larger value indicates a higher priority. If multiple policies have the same priority value, the policy with the latest modification time takes precedence. |
   |**Upstream speed limit KB/s** |Set the maximum transmission rate at which endpoint devices within the policy scope send data to gateways. Enter 0 for no rate limit. |
   |**Download speed limit KB/s** |Set the maximum transmission rate at which gateways send data to endpoint devices within the policy scope. Enter 0 for no rate limit. |
   |**Scope** |Select the policy scope. Select **Effective by employee** to apply the policy by department, role, or member, or **Effective by device** to apply it to devices. |
   |**Exclude object** |After this option is enabled, you can specify personnel or devices that do not trigger this rate limiting policy. |
   

8. Click **Confirm** to create the policy.

9. (Optional) In the **Employee Speed Limit Policy** list, you can perform the following operations:

   * **Search policies**: Quickly search by keywords such as policy name and effective object.

   * **Adjust priority**: Click the **Priority** value of a policy to quickly modify its matching order.

   * **Edit or delete a policy**: In the **Operation** column of the target policy, click **Edit** to modify the policy configuration, or click **Delete** to remove the policy.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After a rate limiting policy is saved, it is delivered in real time to the associated proxy gateway clusters. Each gateway node enforces rate limits independently for each endpoint device. In other words, the rate limit applies to each device, and devices do not share rate limit quotas.</div>


<span id=".5p-l55yL5pel5b-X"></span>
## View logs

View the following records in [Log audit](https://docs.byteplus.com/en/docs/sealsuite/docs-zk9yxy9szc):


* **Configuration change records**: View change records for client rate limiting configurations and employee rate limiting policies in **Admin Log**.

* **Rate limit hit records**: View the matched rate limiting policies, affected employees and devices, actual upload and download rates, and configured limits in **User Log** to understand how rate limiting policies are enforced.
