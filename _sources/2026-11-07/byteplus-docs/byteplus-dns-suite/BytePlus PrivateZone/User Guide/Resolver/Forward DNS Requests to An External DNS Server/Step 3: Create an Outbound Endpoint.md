---
title: "Step 3: Create an Outbound Endpoint"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/OxDblm"
---

This document describes how to create an outbound endpoint in an outbound VPC. An outbound endpoint is the forwarding exit for DNS requests.

<span id="steps"></span>
## Steps

Follow the steps below to create an outbound endpoint.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **Outbound endpoint** tab.

2. Click **Create outbound endpoint**. On the **Create outbound endpoint** page, configure the following parameters:

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Endpoint name** |The name of the endpoint. Supports UTF\-8 characters. |
   |**Outbound VPC** |The ID of the outbound VPC you created. This parameter cannot be modified after creation. |
   |**Security group** |The name of the security group for the outbound VPC. The security group must contain at least one outbound rule. This outbound rule needs to allow TCP and UDP protocols and the IP address of the target DNS server. This parameter cannot be modified after creation. |
   |**IP addresses** |The IP address of the outbound endpoint. To ensure high availability of the service, you must add at least 2 outbound IP addresses.<br><br><br>* **Select availability zone**: The availability zone where the IP address of the outbound endpoint is located. It is recommended that the IP addresses of different outbound endpoints be located in different availability zones.<br><br>* **Select subnet**: The VPC subnet where the outbound endpoint is located.<br><br>* **IP address**: The IP address of the outbound endpoint. If you do not set an IP address, the system will automatically assign one. |
   |**Cross\-service authorization** |Click **Authorize** to authorize the PrivateZone service. You must complete the authorization to use the forwarding service of the resolver. |
   

   **Resource management**

   
   |Parameter |Description |
   |---|---|
   |**Project** |The name of the project to which the endpoint belongs. The default is **default**. You can click the drop\-down menu to select a project. BytePlus PrivateZone displays all projects for which the current primary account or IAM account has management permissions in the drop\-down menu. You can also click **Create project** to create a new project. |
   |**Tag** |Tags for the endpoint. Each tag is a key\-value pair. Click **Add tag** to add a tag, then enter the tag key and tag value in the two input boxes respectively, for example, `example-key` and `example-value`. Both tag keys and tag values support UTF\-8 characters. You need to press Enter after each input to confirm the content. You can add up to 20 tags for a endpoint. |
   

3. Click **Ok**.


The outbound endpoint will take about 30 seconds to be created. You can click the **Refresh** button on the right side after 30 seconds to check whether the outbound endpoint has been created.

<span id="next-steps"></span>
## Next steps

Next, you can [Create rules in the resolver](https://docs.byteplus.com/docs/byteplus-dns-suite/Zd7JQO).
