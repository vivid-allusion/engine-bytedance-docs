---
title: "Implement Load Balancing"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/s3g1J3"
---

This document introduces how to implement DNS\-based load balancing in BytePlus PrivateZone.

<span id="feature-overview"></span>
## What is load balancing

If a record set contains multiple record values, and each record value has a weight, BytePlus PrivateZone will calculate the sum of the weights of all record values in the record set and determine the weight ratio of each record value. Based on the weight ratio of each record value, BytePlus PrivateZone will return the record value when responding to the same proportion of DNS queries.

For example, if there is a record set under `www.example.com` containing two record values `10.0.0.1` and `10.0.0.2` with weights of 1 and 3 respectively, BytePlus PrivateZone will return `10.0.0.1` in the response of 25 out of 100 DNS queries matching the record set, and `10.0.0.2` in the response of 75 out of 100 DNS queries.


* In the BytePlus PrivateZone console, BytePlus PrivateZone automatically manages the record set for you. You can create multiple record values for a DNS record. Then, you can achieve DNS\-based load balancing by setting weights for the record values.

* In the BytePlus PrivateZone OpenAPI, you can achieve DNS\-based load balancing through the record set.


BytePlus PrivateZone has the following limitations for load balancing:


* **A and AAAA record types**: You can enable or disable load balancing. When load balancing is disabled, BytePlus PrivateZone will return all record values upon receiving a DNS query request. The order of the record values is random.

* **CNAME record type**: BytePlus PrivateZone automatically enables load balancing for CNAME records. You cannot disable load balancing for CNAME records. Thus, even if you add multiple CNAME records for a domain name, BytePlus PrivateZone will only return one CNAME record each time it receives a DNS query request.

* **TXT, MX, and PTR record types**: Load balancing is disabled by default and cannot be enabled.


Refer to [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/0K0WyX) to understand the limitations of BytePlus PrivateZone on the number of DNS records and the range of weight values in a record set.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you enable load balancing, the cache of the recursive DNS server in BytePlus PrivateZone will be unavailable for your domain. Therefore, the number of DNS query requests received by the authoritative DNS server will increase, which will also increase billing.</div>


For example:


* You set the weights of two record values to 4 and 1 respectively. 4/(4+1) = 80% of DNS queries will be routed to the first record value; 1/(4+1) = 20% of DNS queries will be routed to the second record value.

* You set the weights of three record values to 8, 6, and 3 respectively. 8/(8+6+3) = 47% of DNS queries will be routed to the first record value; 6/(8+6+3) = 35% of DNS queries will be routed to the second record value; 3/(8+6+3) = 18% of DNS queries will be routed to the third record value.


<span id="operation-scenarios"></span>
## Example scenario

A common scenario is the canary release of a new service. The new service has an independent IP address. You can set a smaller weight for the new service initially, so that a small amount of traffic is routed to the IP address of the new service. After monitoring and testing, you can gradually increase the weight to increase the traffic routed to the IP address of the new service, and eventually achieve the full release of the new service.

Suppose your domain name is `ecs.example.com`. The IP address pointed to by this domain name is `10.0.0.128`. You need to canary release a new service. The IP address of the new service is `10.0.0.1`. You want 22% of the traffic to be routed to `10.0.0.1` and 78% of the traffic to be routed to `10.0.0.128`.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e84aa8a1820de0819cd7ca23bbddcc95.jpeg) </span>

<span id="operation-steps"></span>
## Steps

<span id="step-one-add-domain"></span>
### Step 1: Create a domain

Create the domain `example.com`. You need to enable load balancing when creating the domain. Refer to [Create a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV) to learn how to create a domain.

<span id="step-two-implement-load-balancing"></span>
### Step 2: Implement load balancing

Refer to the following steps to implement the example scenario.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you did not enable load balancing when creating the domain, the console will not display weight\-related settings when you create DNS records for the domain.</div>



1. Open the **Edit record set** page for the `ecs.example.com` DNS record. Refer to [Update DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/pkPnV9).

2. On the **Edit record set** page, set the following parameters.

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Domain** |Set to `ecs`. |
   |**Record type** |Set to **A**. |
   |**TTL** |Set to **10 minutes**. |
   |**Line** |Set to **Default line**. |
   |**Load balancing** |Set to **Enabled**. |
   

   **Record value**

   
   |Record value |Weight |Enabled |
   |---|---|---|
   |10.0.0.1 |22 |Enabled |
   |10.0.0.128 |78 |Enabled |
   

3. Click **Submit**.
