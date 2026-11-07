---
title: "Create a custom inference service"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_a_custom_inference_service"
---

In ContextSearch, the system provides built\-in inference services and also supports creating user\-defined inference services. When creating a user\-defined inference service, link it with the target model and configure network, resources, and user\-defined parameters based on business needs. This topic describes how to create a user\-defined inference service.

<span id="TAVsOrJN"></span>
## Prerequisites

Identify the model linked to the inference service and obtain the target model name in advance.


* If linking a user\-defined model, create the user\-defined model first; see [Create a custom model](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_custom_model).

* If linking a common model, obtain the common model’s name, dimension, and other details in advance; see [View a public model](https://docs.byteplus.com/en/docs/cloudsearch/View_a_public_model).


<span id="74Xg3jb2"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, choose **ContextSearch \> Model and reasoning \> Inference service**, click the **Custom inference service** tab, then click **Create an inference service**.

4. In the **Create inference service** panel, configure the following parameters, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Affiliated project |Project of the inference service. Cannot be changed when creating an inference service. To modify it, close the panel and change it via the top navigation bar. |
   |Service name |Customize the name of the inference service.<br><br><br>* First character only supports letters or underscores (_).<br><br>* Can include letters, digits, and special characters with only English periods (.), underscores (_), hyphens (\-), and slashes (/), length 1–128 characters.<br><br>* Can contain only one slash (/) character. |
   |Description (optional) |Set the description for the inference service, with a maximum length of 256 characters. |
   |Tag (optional) |Add tags to inference services for easier identification and management. You can click **Add row** multiple times to add several tags. |
   |Select model |Select the public model or custom model associated with the inference service from the dropdown. Supports filtering by type or fuzzy search by model name keywords. |
   |Purchase method |Select **Exclusive resource** or **By token**. Some models do not support configuring this parameter. |
   |Resource type |Visible when **Purchase method** is set to **Exclusive resource** Select **CPU** or **GPU**. |
   |Specification |Visible when **Purchase method** is set to **Exclusive resource** Select CPU or GPU specifications from the dropdown list. |
   |Quantity |Visible when **Purchase method** is set to **Exclusive resource** Set the number of nodes for the inference service, ranging from 1 to 512. |
   |Private network |Visible when **Purchase method** is set to **Exclusive resource** Select the Virtual Private Cloud where the inference service resides. To create a new Virtual Private Cloud, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |Visible when **Purchase method** is set to **Exclusive resource** The system automatically filters available subnets based on the Virtual Private Cloud you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Model rate limiting |Visible only when **Purchase method** is set to **By token**. Current account’s rate limit for accessing the selected model. |
   |Access point rate limiting |Turn on to set rate limiting for each access point. If off, the default is to limit by model.<br><br><br>* RPM: When access point rate limiting is on, you need to configure RPM (Requests Per Minute), which is the number of requests processed per minute.<br><br>* TPM: Visible when selecting the Volcano Ark model and the **Purchase method** is set to **By token**. When access point rate limiting is on, configure TPM (Tokens Per Minute), which is the number of tokens processed per minute. |
   |User\-defined parameter (optional) |Supports configuring user\-defined parameters for inference services. Click **Add custom parameters**, then configure the parameter name and value. |
