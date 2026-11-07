---
title: "Load Balancing and Disaster Recovery with BytePlus CDN"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Load_Balancing_and_Disaster_Recovery_with_BytePlus_CDN"
---

[BytePlus Content Delivery Network](https://www.byteplus.com/en/product/cdn) (CDN) consists of cache nodes distributed globally. BytePlus CDN distributes site content to cache nodes close to users, allowing users to quickly get the required content from the nearest cache node, thereby effectively solving issues like network congestion and network latency, and optimizing user experience. In BytePlus CDN, you can configure multiple origin servers to achieve failover across these servers. By setting the weight of each origin server, you can achieve load balancing of origin requests.

The load balancing and failover mechanisms provided by BytePlus CDN are not customizable but can meet most business needs. However, if your business requires custom logic for origin server load balancing and failover, you can use BytePlus GTM.

Additionally, if you have CDN services from multiple cloud providers and need to distribute user requests among different cloud providers according to specific rules, you can also use BytePlus GTM.

<span id="load-balancing-health-check-and-disaster-recovery-for-origin-servers-in-byteplus-cdn"></span>
## Load balancing, health check, and disaster recovery for origin servers in BytePlus CDN

You can use BytePlus GTM to achieve load balancing, health check, and disaster recovery across origin servers in multiple AZs or regions in BytePlus CDN:


* Suppose your origin servers are deployed in multiple AZs within a region in public cloud services or self\-built IDC services. When a service in a certain AZ fails, you can perform automatic or manual failover according to the disaster recovery plan, switching user traffic to other AZs to ensure uninterrupted service or quick recovery. Refer to [Intra-region Disaster Recovery](https://docs.byteplus.com/docs/byteplus-dns-suite/5qftVh).

* When your origin servers are deployed in multiple regions, you need to achieve cross\-region disaster recovery under regional\-level failures to ensure quick recovery or continuous operation of services during failures. You can achieve traffic management and cross\-region disaster recovery under regional\-level failures through a cross\-region active\-active architecture. The cross\-region active\-active architecture supports disaster recovery both within multiple AZs in a region and across regions. Refer to [Cross-region Disaster Recovery](https://docs.byteplus.com/docs/byteplus-dns-suite/jEzSkh).


The following diagram shows the load balancing, health check, and disaster recovery solution implemented through BytePlus GTM when origin servers are deployed in multiple AZs within a region in public cloud services. The website with the domain name `www.example.com` connects to BytePlus CDN service. The domain name of the website points to the CNAME of BytePlus CDN `www.example.com.bplslb.com` through a CNAME record. At the same time, you set the origin address of the domain name in BytePlus CDN to the routing domain name of BytePlus GTM `www.example.com.byteplus.com`. When the regional node of BytePlus CDN initiates a origin request to the origin address, BytePlus GTM returns the IP address of the primary or backup origin server according to the routing policy you set. The primary and backup origin servers are located in different AZs within the same region. The distance between the origin servers is relatively short, so the impact of traffic switching on network latency is minimal. The primary and backup origin servers adopt an cross\-region active\-active mode, with the primary origin server handling 50% of the origin requests and the backup origin server handling 50% of the origin requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the origin server is a private TOS bucket, this solution is not applicable.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_24f18f733af03b4d0288e01d939a0f21.jpeg) </span>

BytePlus GTM regularly performs health checks on the servers of the primary and backup origin servers to determine whether the servers of each origin server are available:


* If all servers of the primary origin server are unavailable, the origin requests handled by the primary origin server will be fully transferred to the backup origin server.

* If the servers of the primary origin server become available again during the next health check, the recovered servers will resume handling the proportion of origin requests corresponding to their weight.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_423585b3a1d99fe2d9c090785963fabb.jpeg) </span>

<span id="steps"></span>
### Steps

Refer to the following steps to achieve load balancing and disaster recovery between multiple AZs as shown in the above diagram.

<span id="step-1-configure-byteplus-gtm"></span>
#### Step 1: Configure BytePlus GTM

Complete the following steps in BytePlus GTM:


1. Create a GTM instance. You need to set the access method to **CNAME Access**. You can set any routinh domain name.

2. Configure the GTM instance. You need to:

   * Create two pools. The addresses included in each pool are as follows:



|Pool |Address |**Weight** |
|---|---|---|
|Origin Server (Primary) |`1.11.xx.xx`<br><br>`1.21.xx.xx` |25<br><br>25 |
|Origin Server (Backup) |`2.11.xx.xx`<br><br>`2.21.xx.xx` |25<br><br>25 |



* Create a rule. Then, create 3 pool sets in the routing rule.

   * Pool Set A: Includes the pools of the primary and backup origin servers. Priority is 1.

   * Pool Set B: Includes the pool of the primary origin server. Priority is 2.

   * Pool Set C: Includes the pool of the backup origin server. Priority is 3.

3. Start the GTM instance. Once the GTM instance is successfully started, you have achieved load balancing and disaster recovery between multiple AZs.


<span id="step-2-configure-byteplus-cdn"></span>
#### Step 2: Configure BytePlus CDN

Complete the following steps in BytePlus CDN:


1. Create an domain name `www.example.com` and configure the domain name according to your needs.

2. Set the origin address to the routing domain of BytePlus GTM.


<span id="load-balancing-and-disaster-recovery-across-multiple-cdn-providers"></span>
## Load balancing and disaster recovery across multiple CDN providers

Your website needs to connect to the CDN service through a CNAME record. Different CDN providers have different CNAME domain names. In BytePlus GTM, you can set the CNAME domain names of different CDN providers as target addresses and configure routing policies. When users access the website domain name, BytePlus GTM returns an appropriate CNAME record according to the routing policy you set, thereby connecting users to the CDN provider corresponding to the CNAME record.

In the diagram below, when users access the website with the domain name `www.example.com`, BytePlus GTM returns an appropriate CNAME record according to the routing policy.

BytePlus CDN handles 70% of user requests, while third\-party CDN providers handle 30% of user requests. BytePlus GTM regularly performs health checks on the CNAME domain names. If a third\-party CDN provider is unavailable, the user requests handled by the third\-party CDN provider will be transferred to BytePlus CDN.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aaf6a160d455b2a4fffdb702a6af1b87.jpeg) </span>

<span id="steps"></span>
### Steps

Refer to the following steps to achieve load balancing and disaster recovery between multiple CDN providers as shown in the above diagram.

<span id="step-1-configure-cdn"></span>
#### Step 1: Configure CDN

Create a domain name in BytePlus CDN and other CDN providers, and configure the domain name according to your needs.

<span id="step-2-configure-byteplus-gtm"></span>
#### Step 2: Configure BytePlus GTM

Complete the following steps in BytePlus GTM:


1. Create a GTM instance. You need to set the domain name to `www.example.com`.

2. Configure the GTM Instance. You need to:

   * Create a pool. The addresses included in the pool are as follows:

   
   |Address |Weight |
   |---|---|
   |`www.example.com.bpgslb.com` |70 |
   |`www.example.com.xxx.xxx` |30 |
   

   * Create a rule. Create a pool set in the rule. The pool set includes the pool you created.

3. Start the GTM instance. Once the GTM instance is successfully started, you have achieved load balancing and disaster recovery between multiple CDN providers.
