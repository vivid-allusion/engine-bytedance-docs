---
title: "Step 3: Create an Inbound Endpoint"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/EddkeA"
---

This document describes how to add an inbound endpoint in an inbound VPC. An inbound endpoint is the forwarding entry point for DNS requests.

<span id="steps"></span>
## Steps

Follow the steps below to add an inbound endpoint.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **Inbound endpoint** tab.

2. Click **Create inbound endpoint**. On the **Create inbound endpoint** page, configure the following parameters:

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Name** |The name of the endpoint. Supports UTF\-8 characters. |
   |**Inbound VPC** |The ID of the inbound VPC you created. This parameter cannot be modified after creation. |
   |**Security group** |The name of the security group for the inbound VPC. The security group must contain at least one outbound rule. This outbound rule needs to allow TCP and UDP protocols and the IP address of the target DNS server. This parameter cannot be modified after creation. |
   |**IP Addresses** |The IP address of the inbound endpoint. To ensure high availability of the service, you must add at least 2 IP addresses.<br><br><br>* **Select availability zone**: The availability zone where the IP address of the inbound endpoint is located. It is recommended that the IP addresses of different inbound endpoints are located in different availability zones.<br><br>* **Select subnet**: The VPC subnet where the inbound endpoint is located.<br><br>* **IP address**: The IP address of the inbound endpoint. If you do not set an IP address, the system will automatically assign one. |
   |**Cross\-service authorization** |Click **Authorize** to authorize the PrivateZone service. You must complete the authorization to use the forwarding service of the resolver. |
   

   **Resource management**

   
   |Parameter |Description |
   |---|---|
   |**Project** |The name of the project to which the endpoint belongs. The default is **default**. You can click the drop\-down menu to select a project. BytePlus PrivateZone displays all projects for which the current primary account or IAM account has management permissions in the drop\-down menu. You can also click **Create project** to create a new project. |
   |**Tag** |Tags for the endpoint. Each tag is a key\-value pair. Click **Add tag** to add a tag, then enter the tag key and tag value in the two input boxes respectively, for example, `example-key` and `example-value`. Both tag keys and tag values support UTF\-8 characters. You need to press Enter after each input to confirm the content. You can add up to 20 tags for a endpoint. |
   

3. Click **Ok**.


The inbound endpoint will take about 30 seconds to be created. You can click the **Refresh** button on the right side after 30 seconds to check if the inbound endpoint has been created.

<span id="097e9eef"></span>
## Next Steps

Next, you can [create rules in the DNS Server of the on-premise IDC/third-party cloud services](https://docs.byteplus.com/docs/byteplus-dns-suite/8NimQy).
