---
title: "Integrating ALB with GTM to enable cross-region traffic scheduling and disaster recovery failover"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Using-GTM-to-route-incoming-traffic-to-ALB-instances-and-implement-failover-across-Regions"
---

Application Load Balancer (ALB) can integrate with BytePlus Global Traffic Management (GTM). If you create ALB instances in multiple regions, you can integrate GTM to enable traffic scheduling and disaster recovery failover between instances in different regions.

<span id=".5Zy65pmv566A5LuL"></span>
## Scenarios

As shown below, you have created three ALB instances in two regions, China (Beijing) and China (Shanghai), to handle your business with ALB. To enable clients in different regions to access ALB nearby, you can configure GTM to route them to the nearest ALB instance. Additionally, GTM can perform intelligent traffic scheduling and disaster recovery failover between instances in different regions based on the specifications and availability of ALB instances.


* Intelligent traffic scheduling: GTM distributes access traffic proportionally to different ALB instances based on the ALB instances' specifications and your configuration.

* Disaster recovery failover: GTM performs failover based on ALB instance availability. When an ALB instance becomes unavailable, GTM automatically blocks the instance and routes traffic to other ALB instances that can provide normal service.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44562f86cad044519fcaf18ac8d390d9.png) </span>

<span id=".57uT5ZCIZ3Rt5a6e546w6Leo5Zyw5Z-f6LSf6L295Z2H6KGh"></span>
## Achieve cross\-region load balancing using GTM

<span id=".5qih5ouf5Zy65pmv"></span>
### Scenario example

Your website domain is `albtest.com`, with users distributed in Beijing and Shanghai. This topic describes how to achieve nearest access and cross\-region load balancing using ALB and GTM.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The configuration in this section is based on a simulation scenario for reference only. You need to configure appropriate resources according to your current business situation.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure

<span id=".5q2l6aqk5LiA77ya6YCa6L-HLWFsYi3lrp7njrDmtYHph4_nmoTotJ_ovb3lnYfooaHjgII="></span>
#### Step 1: Use ALB to balance traffic.


|Step |Actions |Related documents |
|---|---|---|
|1 |**Purchase and configure an ECS:** <br><br>Based on the user's regional distribution, purchase and configure at least two Elastic Compute Service (ECS) instances, each for one region. In this example, purchase one ECS instance in each of the Beijing and Shanghai regions, and deploy your website on these ECS instances. |[ECS Getting Started](https://docs.byteplus.com/docs/ecs/Getting-Started) |
|2 |**Purchase and configure an ALB instance:** <br><br>Create public ALB instances in China (Beijing) and China (Shanghai), configure listeners for each instance, and add the ECS instances from Step 1 to the server group. |[ALB Getting Started](https://docs.byteplus.com/docs/clb/ALB-Getting-Started) |


Now, you have achieved fine\-grained load balancing for traffic received by a single ALB instance. By configuring GTM, you can enable clients in Beijing and Shanghai to access the nearest ALB and intelligently schedule traffic between the two regions.

<span id=".5q2l6aqk5LqM77ya6YCa6L-HLWd0bS3lrp7njrDorr_pl65hbGLmtYHph4_nmoTlhajlsYDnrqHnkIbjgII="></span>
#### Step 2: Use GTM for global management of traffic accessing ALB.​


|Step |Actions |Related documents |
|---|---|---|
|1 |**Purchase a GTM instance**: After successful purchase, the system automatically assigns a scheduling domain.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If your domain provider is from BytePlus, you can directly select domain access.</div><br><br><br><br>1. Log in to [the GTM console](https://console.byteplus.com/TrafficRoute/gtm/instances).<br><br>2. On the **Instance management** page, click **Create instance**.<br><br>3. On the **Create Instance** page, set the access mode to **CNAME**. Type `albtest.com` in the **Domain** field.  Then click **Confirm order**. |[Create a GTM instance](https://docs.byteplus.com/en/docs/byteplus-dns-suite/A5PoZE) |
|2 |**Configure and enable a GTM instance**:<br><br><br>1. Log in to [the GTM console](https://console.byteplus.com/TrafficRoute/gtm/instances).<br><br>2. In the **Domain** column, locate **`albtest.com`**.<br><br>3. In its **Actions** column, click **Configure**.<br><br>4. In the **Basic information** section of the **Instance configuration** page, select **Performance\-optimized policy**. Then click **Next**.<br><br>5. In the **Add traffic target** section of the **Instance configuration** page, set the name for address pool 1 and set the address type to domain. Add two addresses concurrently. Type the instance domain name and address region for the two ALB instances respectively, with the address availability mode set to automatic.<br><br>6. Remain the system default configuration for health check, check **Enable instance scheduling**, and click **Submit**. |[GTM Getting Started](https://docs.byteplus.com/en/docs/byteplus-dns-suite/S1LBKo) |
|3 |**Connect your website domain to GTM**: Create a CNAME record at your DNS provider to point `albtest.com` to the GTM instance's scheduling domain.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For domain resolution entry and procedure, see the provider's documentation or contact your customer service.</div><br><br><br><div data-tips="true" data-tips-type="tip">Welcome to <a href="https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-product-overview">BytePlus TrafficRoute</a> for CNAME resolution.</div><br><br><br><div data-tips="true" data-tips-type="tip">You can view the GTM instance's scheduling domain on the <strong>Instance management \> Instance configuration </strong>page.</div><br><br><br><br>1. Log in to [the DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).<br><br>2. In the Domain column, locate `albtest.com`.<br><br>3. In the **Actions** column, click **Manage**.<br><br>4. In the **Record management** tab, click **Add record**.<br><br>5. On the **Add record** page, set **Record type** to **CNAME** and **Host record** to  **@** .<br><br>6. Click **Add record value**, set **Record value** to the GTM instance’s scheduling domain: `albtest.com.gtm.volcdns.com`, and click **Submit**.<br><br><br>After configuration, the effective time of CNAME records varies by DNS provider. On the DNS console, new CNAME records take effect upon addition, while modified CNAME records require time to live (TTL) for propagation. |[DNS Getting Started](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-tutorial-introduction) |
