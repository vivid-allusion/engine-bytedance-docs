---
title: "Domain configuration"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en"
---

In BytePlus CDN, domain configurations include general configurations, origin server configurations, and CDN feature configurations.


* The domain details page displays the general configurations of the domain. You can configure the project that the domain belongs to, domain tags, policies bound to the domain, certificates associated with the domain, and Chinese Mainland Optimization.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260804134953-1717121632766.png) </span>

<span id="configure-general-domain-settings"></span>
## Configure general domain settings

The domain details page displays the general configurations of the domain. You can configure the project that the domain belongs to, domain tags, policies bound to the domain, certificates associated with the domain, and Chinese Mainland Optimization.

<span id="configure-chinese-mainland-optimization"></span>
### Configure Chinese Mainland Optimization

Chinese Mainland Optimization is a general configuration on the domain details page. It is not managed through policies. If the service region of your domain is **Outside the Chinese Mainland**, you can enable **Chinese Mainland Optimization** for the domain. After you enable this feature, traffic from the Chinese Mainland to the domain is routed through the selected accelerator's GA CNAME. This improves access performance for users in the Chinese Mainland.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can enable <strong>Chinese Mainland Optimization</strong> only after the domain is created. You cannot enable this feature while adding a domain.</div>


* <div data-tips="true" data-tips-type="tip">Before you use this feature for the first time, go to <strong>Tool Center</strong> \> <strong>Chinese Mainland Optimization</strong> and authorize BytePlus CDN to use BytePlus Global Accelerator. After authorization is complete, return to the domain details page and continue with the following steps. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/cross-mlc-border-acceleration_en-us">Manage Chinese Mainland Optimization Accelerators</a>.</div>


* <div data-tips="true" data-tips-type="tip">If no accelerator is available, you can click <strong>Create Accelerator</strong> on the domain configuration page. You can also go to <strong>Tool Center</strong> \> <strong>Chinese Mainland Optimization</strong> to create and manage accelerators. On the domain details page, you can bind an accelerator only to the current domain. To bind multiple domains to the same accelerator at a time, use the <strong>Chinese Mainland Optimization</strong> page in Tool Center. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/cross-mlc-border-acceleration_en-us">Manage Chinese Mainland Optimization Accelerators</a>.</div>



<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260804135502-880116814907.png) </span>

<span id="steps"></span>
#### Steps


1. Log in to the `https://console.byteplus.com/cdn`.

2. In the left navigation pane, click **Domain Names**.

3. On the **Domain Names** page, locate the domain you want to configure in the domain list.

4. In the **Actions** column, click **Manage**.

5. On the domain details page, enable **Chinese Mainland Optimization**.

6. For **Accelerator**, select an available accelerator.

   * If no accelerator is available, click **Create Accelerator**. After you create the accelerator, provisioning usually takes 2 to 5 minutes. Do not create another accelerator during this time.

   * Only available accelerators can be selected. If an accelerator is still being configured or is unavailable, wait until it becomes available, and then try again.

7. At the bottom of the page, click **Submit Changes** to save the domain configuration.


After the configuration takes effect, traffic from the Chinese Mainland to the domain is routed through the selected accelerator's GA CNAME. Traffic from other regions is not affected by this setting.

<span id="manage-origin-server-and-cdn-feature-configurations"></span>
## Manage origin server and CDN feature configurations

The configurations for origin server and CDN features are implemented through policies. When you associate a policy with a domain, the configurations in the policy are applied to the domain.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9bedaa983792aa380605d90d98d07b37.png) </span>

BytePlus CDN offers two methods for managing your domain's origin server and feature configurations, allowing you to choose the best approach for your needs. This guide provides step\-by\-step instructions for both per\-domain management, ideal for individual domain adjustments, and policy\-based management, which is efficient for applying consistent settings across multiple domains.


* Method 1: Manage domain configurations on a per\-domain basis, which is suitable for configuring individual domains. Modifications to one domain do not affect other domains.

* Method 2: Manage domain configurations based on policies, suitable for configuring multiple domains that are associated with the same policy.


Below are introductions to these two methods and their related operational steps.

<span id="method-1"></span>
### Method 1: Managing Domain Configurations on a Per\-Domain Basis

This method is essentially managing domain configurations based on policies, as CDN creates independent policies for domains. However, CDN provides a separate domain configuration page, making the policy mechanism transparent to you. When you manage domain configurations with this method, the configurations appear to belong to the domain itself. In fact, when you open the domain configuration page, CDN has already performed a series of [preliminary operations](https://docs.byteplus.com/en/docs/18/40495#preliminary-operations-performed-by-cdn) on the policy associated with that domain.

The domain configuration page contains multiple tabs. Each tab contains different domain configurations, as shown in the following table:


|**Tab** |**Domain Configurations** |
|---|---|
|General |Standard Origins, Conditional Origins, Origin Protocol, Origin Certificate Validation, IPv6 Origin Fetch, Origin Hostname |
|HTTPS |Certificates, Mutual TLS, Protocol Redirect, OCSP Stapling, HSTS, TLS Versions, HTTP/2, HTTP/3 (QUIC) |
|Access Restrictions |PROXY Protocol, IPv6, WebSocket, Server\-Sent Events, URL Normalization, Geographic Restrictions, IP Restrictions, Referer Restrictions, UA Restrictions, Origin Restrictions, Disabled HTTP Methods, Custom Header Restrictions, Custom Restrictions, URL Redirect, Remote Authentication, Data Rate Throttling, Bandwidth Limit, Rate Limiting |
|Signed URL Authentication |Signed URL Authentication |
|Caching |Cache Key, Caching Rules, Negative Caching, Negative Caching, Browser Caching, Client Response Headers, Custom Error Pages, Multi Range, Serve Stale |
|Origin Fetch |Range Origin Fetch, Origin Fetch Timeouts, Follow Redirects, Origin Retry, Origin Request Headers, Origin URL Rewrite, Origin Request Parameters, Origin SNI, Origin Response Headers |
|Content Optimization |File Compression, File Minification, Video Seeking |
|Performance Optimization |Smart Routing, Origin Keep\-Alive |
|AI Traffic Management |Convert HTML to Markdown |


<span id="steps"></span>
#### Steps


1. Log in to the `https://console.byteplus.com/cdn`.

2. In the left navigation pane, click **Domain Names**.

3. On the **Domain Names** page, locate the domain you want to configure in the domain list.

4. In the **Actions** column, click **Manage**.

5. On the domain details page, click **Domain\-based Configuration**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_67de1c009926a4effeda5a46140cdd46.png) </span>


6. On the domain page, click the tab containing the configuration you want to modify.

7. In the upper right corner of the page, click **Modify Settings**.

8. After completing the configuration, click **Submit Changes**.


<span id="preliminary-operations-performed-by-cdn"></span>
#### Preliminary Operations Performed by CDN

If you are using Method 1 for a domain for the **first time**, when you click **Domain\-based Configuration**, CDN performs the following operations:


1. Duplicates the policy currently associated with the domain to create a new policy.

   * The new policy ID is randomly generated by the system.

   * The new policy name is created by adding `(system-tpl)` to the end of the current policy name associated with the domain, indicating it's a system\-created policy. For example, if the current delivery policy name is `myPolicy`, the new policy name will be `myPolicy(system-tpl)`.

2. Takes you into the editing mode for the new policy, where you can modify its configuration.


If this is **not the first time** you're using Method 1 for a domain, when you click **Domain\-based Configuration**, CDN performs the following operations:


1. Creates a draft version of the policy associated with the domain.

2. Takes you into the editing mode of this draft version.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Although you are in the policy editing mode, what you actually see is a domain\-based configuration page.</div>


<span id="method-2"></span>
### Method 2: Managing Domain Configurations Based on Policies

In this method, you configure the policy and then publish it. After the policy is published, the configurations in the policy are applied to all domains associated with that policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Policy updates and publishing are based on policy versions. Before using Method 2, it's recommended to understand <code>https://docs.byteplus.com/en/docs/byteplus-cdn/policy-versioning_zh-cn</code>.</div>


In CDN, there are three types of policies: delivery policies, encryption policies, and rules engine policies. For information about rules engine policies, see `https://docs.byteplus.com/en/docs/byteplus-cdn/rules-engine_en`. The following sections describe the configurations in delivery policies and encryption policies.


* The delivery policy configuration page includes **Origin Configuration** and **Policy Configuration** tabs.

* The encryption policy configuration page includes the **Policy Configuration** tab.



|**Delivery Policy** |**Encryption Policy** |
|---|---|
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1de87261f53b200783cbe77dd3af9dd2.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d486ef5b57f0b9b9f332ca118482f6dd.png) </span> |


On the **Policy Configuration** tab, click **Add** to add CDN features you want to configure. On the **Add Feature** page, CDN features are categorized by configuration type, as shown in the following table:


|**Policy Type** |**Tab** |**Configuration Category** |**Included Configurations** |
|---|---|---|---|
|Delivery Policy |Origins |Origins |Standard Origins, Conditional Origins, Origin Protocol, Origin Certificate Validation, IPv6 Origin Fetch, Origin Hostname |
||CDN Features |Protocols and Methods |IPv6, Disabled HTTP Methods, WebSocket, Server\-Sent Events, PROXY Protocol |
|||Access Restrictions |Geographic Restrictions, IP Restrictions, UA Restrictions, Referer Restrictions, Origin Restrictions, Remote Authentication, Custom Restrictions |
|||Throttling |Data Rate Throttling, Rate Limiting |
|||CDN Responses |Client Response Headers, Custom Error Pages, URL Normalization |
|||Cache |Caching Rules, Cache Key, URL Redirect, Negative Caching, Browser Caching, Serve Stale |
|||Content Optimization |File Compression, Video Seeking, File Minification |
|||Origin Fetch |Origin Fetch Timeouts, Origin Request Headers, Range Origin Fetch, Redirect Follow, Origin Retry, Origin Request Parameters, Origin SNI, Origin URL Rewrite, Origin Response Headers |
|||AI Traffic Management |Convert HTML to Markdown |
|||Performance Optimization |Smart Routing, Origin Keep\-Alive |
||Signed URL Authentication |Signed URL Authentication |The following authentication types are available: Type A, Type B, Type C, Type D, Type E, and Type F. |
|Encryption Policy |CDN Features |Protocols |HTTP/3 (QUIC), HTTP/2, Protocol Redirect |
|||SSL/TLS |OCSP Stapling, HSTS, TLS Versions, Mutual TLS |


<span id="steps"></span>
#### Steps


1. Log in to the `https://console.byteplus.com/cdn`.

2. In the left navigation pane, depending on the policy type you want to edit, click either **Delivery Policies** or **Security** \> **Encryption Policies**.

3. In the policy list, locate the policy you want to configure.

4. In the **Actions** column, click **Modify**.

5. If the **Create Version** button is active (not grayed out), click it.

6. Click the **History** tab, then click the **Policy Versions** tab.

7. On the **Policy Versions** tab, find the version with the "Draft" status.

8. In the **Actions** column, click **Modify**.

9. Configure the draft version accordingly.

   * On the **Origins** tab, you can configure origin server settings. Encryption policies don't have an **Origins** tab.

   * On the **CDN Features** tab, you can configure CDN features. To configure a CDN feature, you need to first click **Add** to add the feature, and then configure it.

10. After completing the configuration, click **Save** at the bottom right of the page.

11. On the **Policy Versions** tab, locate the draft version.

12. In the **Actions** column, click **Publish**.
