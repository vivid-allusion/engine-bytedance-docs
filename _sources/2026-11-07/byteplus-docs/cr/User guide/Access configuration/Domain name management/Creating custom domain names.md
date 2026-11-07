---
title: "Creating custom domain names"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Create_a_custom_domain_name"
---

Custom domain names enable unified enterprise\-level service management. By creating a custom domain name, you can ensure the domain name of a CR instance remains unchanged before and after migration, thereby guaranteeing service continuity. This topic describes how to create a custom domain name in CR.

<span id="HSSAvpCH"></span>
## <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is only available for Standard Edition instances.</div>


<span id="jhElNinF"></span>
## Background

When creating a custom domain name, you can select from two types. Different types require different subsequent configuration steps:


|**Creation type** |**Description** |**Subsequent operations** |
|---|---|---|
|TrafficRoute type |Create using the domain name suffix managed by BytePlus TrafficRoute. The system automatically configures public and private network resolution records. No manual operation is required. |Once creation is complete, it can be used immediately. To confirm the resolution state, you can view it via [View TrafficRoute resolution records](https://docs.byteplus.com/en/docs/cr/View_TrafficRoute_resolution_records?lang=en). |
|Custom type (third\-party domain name) |Use a registered third\-party domain name to create. The system does not automatically configure resolution records. The user must manually add a CNAME record with the DNS service provider to point the custom domain name to the instance's system domain name. |After creation, internal network (VPC) access is supported by default. To enable public network access, [Add public network access resolution records](https://docs.byteplus.com/en/docs/cr/Add_resolution_records_for_public_network_access) is required. |


<span id="3WPpKLRB"></span>
## Considerations


* When images are pulled by using the encryption\-free addon, custom domain names are not supported. Use the default domain name instead.

* Disabling public network access has a **21\-minute** delay. If ICP filing has been completed for a custom domain name with a third\-party cloud service provider and **Public network** is not selected for **Referrer** of the custom domain name, public network access will be disabled at least 21 minutes after the custom domain name is created.


<span id="HNdekSqI"></span>
## Prerequisites

An SSL certificate has been uploaded. For operation methods, see [Certificate center getting started](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-get-started-with-ssl-certificate-service).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **list of instances**and select the entry according to the instance type:

      * Standard instance: Click **standard instance**, find the target instance, and click **enter instance**.

      * Proxy repository: Click **proxy repository**, and click the target domain name to enter the instance details page.

2. In the left navigation bar, click **Domain name management**. On the **Domain name management** page, click **Add custom domain name**.

3. Configure custom domain name parameters.

   
   |Parameter |Description |
   |---|---|
   |Type |Select the method for creating a custom domain name.<br><br><br>* TrafficRoute: Create using the domain name suffix managed by BytePlus TrafficRoute. The system automatically configures public and private network resolution records. No manual operation is required.<br><br>* Custom: Use a registered third\-party domain name to create a custom domain name. |
   |Domain name |Configure custom domain name.<br><br><br>* When selecting **TrafficRoute ** : Enter the prefix of the custom domain name, then select the suffix based on TrafficRoute resolution.<br><br>* When selecting **Custom**: Enter the registered custom domain name. You can register a domain name through [Domain Name Service](https://console.byteplus.com/domain-service/search?promotion=new-account&zone=.com). |
   |Certificate |Select the uploaded certificate. For official upload instructions, see [Certificate center getting started](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-get-started-with-ssl-certificate-service). |
   |Referrer |VPC access and public network access are supported. After you select **Custom** for "Type" to create a domain name, to enable public network access, you need to add a domain name resolution record on the corresponding domain name provider platform. For information about how to add a domain name resolution record, see [Adding public network access resolution records](https://docs.byteplus.com/en/docs/cr/Add_resolution_records_for_public_network_access). |
   

4. Click **Check and submit**. After the check is passed, the custom domain name is created.
