---
title: "Add a Domain"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/PU6MMV"
---

This document explains how to add your domain in BytePlus PrivateZone and associate it with your [BytePlus Virtual Private Cloud (VPC)](https://www.byteplus.com/en/product/vpc). The DNS resolution for the domain is only effective within the associated VPCs.

<span id="prerequisites"></span>
## Prerequisites

You have one or more [VPCs](https://www.byteplus.com/en/product/vpc) under your BytePlus account.

<span id="steps"></span>
## Steps

Complete the following steps to add a domain and associate the domain with one or multiple VPCs.


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, click **Add domain**.

3. In the **Add domain** dialog, configure the basic information for the domain and the details of the VPC associated with the domain.

   **Basic information**

   
   |Configuration |Description |
   |---|---|
   |**Domain** |The root domain, which can be a second\-level domain or a domain with more levels. For example, `example.com` or `internal.example.com`. There are several restrictions for the root domain:<br><br><br>* Cannot end with `ivolces.com` or `privatelink.volces.com`. These are reserved domains.<br><br>* Only English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), underscores (_), periods (.), and Chinese characters are allowed.<br><br>* Hyphens (\-) cannot be used at the beginning or end of a label.<br><br>* Multiple periods (.) cannot appear consecutively.<br><br>* The length of a label cannot exceed 63 characters. Under FQDN format, the total length of the domain cannot exceed 254 characters. |
   |**Remarks** |Remarks for the domain. |
   |**Recursive DNS** |Whether to enable recursive query.<br><br><br>* **Enabled**: If the domain in the DNS query is a subdomain of the root domain but is not in any of the root domain's DNS records, BytePlus PrivateZone will use the DNS response from the public recursive DNS server as the response. See [Implement Recursive DNS](https://docs.byteplus.com/en/docs/byteplus-dns-suite/uperuL).<br><br>* **Disabled**: (Default) If the domain in the DNS query is a subdomain of the root domain but is not in any of the root domain's DNS records, DNS resolution fails. |
   

   **Advanced DNS**

   
   |Configuration |Description |
   |---|---|
   |**Subnet\-based routing** |Whether to return a specific IP address based on the subnet from which the DNS query originates. See [Implement Subnet-based Routing](https://docs.byteplus.com/docs/byteplus-dns-suite/-Gvd2s). Domains with **Subnet\-based routing** enabled can only be associated with one VPC. After adding the domain, you cannot enable or disable **Subnet\-based routing**.<br><br><br>* **Enabled**: Returns a specific IP address based on the subnet from which the DNS query originates. To prevent IP address conflicts, domains with Subnet\-based routing enabled can only be associated with one VPC.<br><br>* **Disabled**: (Default) Returns the same IP address regardless of which subnet the DNS query comes from. |
   |**Load balancing** |Whether to enable DNS\-level load balancing for the domain. See [Implementing Load Balancing](https://docs.byteplus.com/en/docs/byteplus-dns-suite/s3g1J3).<br><br><br>* **Enabled**: Activates DNS\-level load balancing. If a record set contains multiple record values, each with a weight, BytePlus privatezone will calculate the total weight of all record values in the set and the weight proportion of each record value. Based on the weight proportion of each record value, BytePlus privatezone will return that record value in the same proportion of DNS query responses.<br><br>   For example, under `www.example.com`, there is a record set with two record values `10.0.0.1` and `10.0.0.2`, with weights of 1 and 3, respectively. If PrivateZone receives 100 DNS queries matching that record set, 25 responses will contain `10.0.0.1`, and 75 responses will contain `10.0.0.2`.<br><br>* **Disabled**: (Default) Disables DNS\-level load balancing. For any DNS query, BytePlus privatezone will return all record values in the set. The order of the record values is random. |
   

   **Resource management**

   
   |Parameter |Description |
   |---|---|
   |**Project** |The name of the project to which the domain belongs. The default is **default**. You can click the drop\-down menu to select a project. PrivateZone will display all projects for which the current primary account or IAM user has management permissions in the drop\-down menu. You can also click **Create project** to create a new project. |
   |**Tag** |Tags for the domain. Each tag is a key\-value pair. Click **Add tag** to add a tag, then enter the tag key and tag value in the two input boxes respectively, for example, `example-key` and `example-value`. Both tag keys and tag values support UTF\-8 characters. You need to press Enter after each input to confirm the content. You can add up to 20 tags for a domain. |
   

   **VPC information**

   
   |Parameter |Description |
   |---|---|
   |**VPC** |The VPC associated with the domain. The DNS resolution for the domain is only effective within the associated VPCs. You can associate one or more VPCs. See [Limits](https://docs.byteplus.com/en/docs/byteplus-dns-suite/0K0WyX) for the limit on the number of associated VPCs. A domain with **Subnet\-based routing** enabled can only be associated with one VPC. |
   

4. After configuration, click **OK**. You can see the added domain on the **Domain management** page.


<span id="next-steps"></span>
## Next Steps

After creating an domain, you can:


* [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G)

* [Update Domain Configuration](https://docs.byteplus.com/docs/byteplus-dns-suite/9iX1X2)

* [Delete a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/jjFt4b)
