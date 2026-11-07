---
title: "Implement Subnet-based Routing"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/-Gvd2s"
---

This document introduces how to implement subnet\-based routing in BytePlus PrivateZone.

<span id="what-is-subnet-based-routing"></span>
## What is subnet\-based routing

The subnet\-based routing feature allows you to select the service address corresponding to the domain name based on the subnet where the client is located.

For domains with subnet\-based routing enabled, you need to configure a line for each record set of that domain. When receiving a DNS query for the domain, BytePlus PrivateZone retrieves the client IP address information from the DNS query and matches this information with the lines of all record sets under the domain. If the client IP address is within a subnet corresponding to a line, the record set associated with that line is successfully matched. BytePlus PrivateZone will return the record value from the successfully matched record set.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Except for the default line, each line corresponds to a subnet of a <a href="https://www.byteplus.com/en/product/vpc">BytePlus Virtual Private Cloud (VPC)</a>. The default line corresponds to all subnets of the VPC.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you enable subnet\-based routing for your domain:</div>



* <div data-tips="true" data-tips-type="warning">The cache of the recursive DNS server in BytePlus PrivateZone will be unavailable for your domain. Therefore, the number of DNS query requests received by the authoritative DNS server will increase, which will also increase billing.</div>


* <div data-tips="true" data-tips-type="warning">Your domain can only be associated with only one VPC, because if a root domain is associated with multiple VPCs, the subnets of different VPCs may have overlapping IP ranges.</div>


* <div data-tips="true" data-tips-type="warning">It is recommended to set a default line as a fallback. This ensures that DNS queries from any subnet can be processed by BytePlus PrivateZone. Otherwise, DNS resolution will fail for subdomains without configured lines.</div>



<span id="example-scenario"></span>
## Example scenario

You have created a VPC with multiple subnets. For subnet\-1 and subnet\-2, you need to implement disaster recovery between availability zones. Therefore, you need to deploy different subnets in different availability zones:


* The IP range of subnet\-1 is `10.0.1.0/24`, located in Availability Zone A.

* The IP range of subnet\-2 is `10.0.2.0/24`, located in Availability Zone B.


Meanwhile, you have added two BytePlus ECS instances to the VPC, associated with subnet\-1 and subnet\-2 respectively.


* The IP address of the ECS instance associated with subnet\-1 is `10.0.1.128`.

* The IP address of the ECS instance associated with subnet\-2 is `10.0.2.128`.


You need to use BytePlus PrivateZone to implement the following:


* Resources within the VPC in subnet\-1 can only access the ECS instance with the IP address `10.0.1.128` through `ecs.example.com`.

* Resources within the VPC in subnet\-2 can only access the ECS instance with the IP address `10.0.2.128` through `ecs.example.com`.

* Resources within the VPC in other subnets can access the ECS instances with the IP addresses `10.0.1.128` or `10.0.2.128` through `ecs.example.com`.


The architecture of the example scenario is shown in the figure below:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_466f65487b300ac78e84897d5f1d47cd.jpeg) </span>

<span id="steps"></span>
## Steps

<span id="step-1-create-a-domain"></span>
### Step 1: Create a domain

Create the domain `example.com`. You need to enable subnet\-based routing when creating the domain. Refer to [Create a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV) to learn how to create a domain.

<span id="step-2-create-a-dns-record"></span>
### Step 2: Create a DNS Record


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, find your domain and click **Manage** in the **Actions** column.

3. On the **Record management** page, click **Create record set** to create a DNS record for subnet\-1.

4. On the **Create record set** page, configure the basic information for the DNS record of subnet\-1.

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Domain** |Set domain prefix to `ecs`. |
   |**Record type** |Set to **A**. |
   |**TTL** |Set to **10 minutes**. |
   |**Line** |Set to subnet\-1. |
   

   **Record value**

   
   |Record value |Enabled |
   |---|---|
   |10.0.1.128 |Enabled |
   

5. Click **Submit**. You can see the created DNS record for subnet\-1 on the **Record management** page.

6. On the **Record management** page, click **Create record set** to create a DNS record for subnet\-2.

7. On the **Create record set** page, configure the basic information for the DNS record of subnet\-2.

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Domain** |Set the domain prefix to `ecs`. |
   |**Record type** |Set to **A**. |
   |**TTL** |Set to **10 minutes**. |
   |**Line** |Set to subnet\-2. |
   

   **Record value**

   
   |Record value |Enabled |
   |---|---|
   |10.0.2.128 |Enabled |
   

8. Click **Submit**. You can see the created DNS record for subnet\-2 on the **Record Management** page.

9. On the **Record management** page, click **Create record set** to create a DNS record for subnets other than subnet\-1 and subnet\-2.

10. On the **Create record set** page, configure the basic information for the DNS record for subnets other than subnet\-1 and subnet\-2.

* **Domain**: Set the domain prefix to `ecs`.

* **Record type**: Set to **A**.

* **Line**: Set to **Default**.

* **Record value**: For the default line, set two record values: `10.0.1.128` and `10.0.2.128`, so that resources in different subnets can resolve to the corresponding IP addresses.

11. Click **Submit**.


<span id="verify-subnet-based-routing"></span>
### Verify subnet\-based routing

Verify the results of subnet\-based routing through the following steps.


1. Log in to the ECS instance in subnet\-1. Enter the following command in the command line to resolve the domain name:

   ```shell
      nslookup ecs.example.com
   ```
   

   If the IP address in the result is `10.0.1.128`, it indicates that subnet\-based routing in subnet\-1 is effective.

2. Log in to the ECS instance in subnet\-2. Enter the following command in the command line to resolve the domain name:

   ```shell
   nslookup ecs.example.com
   ```
   

   If the IP address in the result is `10.0.2.128`, it indicates that subnet\-based routing in subnet\-2 is effective.

3. Log in to the ECS instance in other subnets. Enter the following command in the command line to resolve the domain name:

   ```shell
   nslookup ecs.example.com
   ```
   


If the result contains `10.0.1.128` and `10.0.2.128`, it indicates that the subnet\-based routing function of the default line is effective.
