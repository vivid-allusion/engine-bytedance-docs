---
title: "Create a standard instance"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance"
---

CR provides standard instances for storage and distribution of your own container images and Helm Charts. This article describes how to create a standard instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Micro Edition instances by default support internal network and public network access, with no additional actions required. Intranet connectivity within the same region is enabled by default, which not only avoids consuming public network bandwidth but also effectively enhances the speed of image pushing and pulling.</div>


<span id="B6pEin4l"></span>
## Background

Standard instances support two specifications: Standard Edition and Micro Edition. You can select the appropriate instance type based on business scale, performance requirements, and usage scenarios. For a detailed description of instance specifications, see [Instance type](https://docs.byteplus.com/en/docs/cr/Instance_type?lang=en).

<span id="sbVg2WTO"></span>
## Prerequisites


* You have completed the account authentication. For details, see [Account authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id="uWjm3Udk"></span>
## Procedure


1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. Click **Instance list** in the left navigation bar, then in the **Instance list** area on the right page, click **Create instance**.

4. On the **Create repository instance** page, fill in the configuration information.

   
   |Parameter |Description |
   |---|---|
   |Name |Set the Instance name. Ensure that the instance name is unique within the same region.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the Instance is created successfully, the Instance name cannot be modified.</div><br> |
   |Project |The associated target project. After association, members of that project will inherit corresponding permissions for the CR services based on project authorization. For details, see [Organization Setup ](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). |
   |System Domain Name |According to the Instance name you set, the system automatically generates the Repository domain name. The system domain name is the access portal for the CR instance, used for pushing, pulling, and managing Container images within the Instance. |
   |Billing type |Select the billing type.<br><br><br>* **Pay\-as\-you\-go**: A postpaid billing model. It can be turned on and off at any time and billed based on actual usage duration.<br><br>* **Mixed Billing (Partial Prepayment)** : A mixed billing model. **Instance costs** and **quota scale\-out costs** are billed on a subscription basis, which offers more favorable discounts compared to the Pay\-as\-you\-go billing method. **Outbound public network traffic** and **storage capacity** are billed based on actual usage.<br><br><br>For billing details, please refer to [Product Billing](https://docs.byteplus.com/en/docs/cr/billing). |
   |Purchase Duration |In the mixed billing model, you can select the purchase duration for subscription resources. |
   |Automatic Renewal |Supports enabling automatic renewal services for subscription resources. For automatic renewal details, see [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   |Tag |Add tags to the instance. You can search for and select existing tags. You can also create custom ones if existing tags cannot meet your requirements.  |
   |Service\-side encryption |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only Standard Edition supports this feature.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Server level encryption can only be enabled when creating an Instance; it is not supported for existing Instances. To use this feature for existing data, create an Instance with encryption enabled, and use registry replication to migrate data from the existing Instance to the new Instance. For details, see <a href="https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions?lang=en">registry replication</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Encrypting and decrypting large images may cause some push and pull performance loss. Please enable as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After enabling, this feature cannot be turned off via the Console. To turn off, <a href="https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000208">Submit work order</a>.</div><br><br><br><br>Whether to enable server level encryption. After enabling, image data will be stored in encrypted form on the server, helping you meet some data security compliance requirements.<br><br><br>* Enable: Uploaded images will be encrypted by default after enabling.<br><br>* Disable: Default value, encryption is not enabled. |
   

5. In **Scale package**, click **Standard Edition** or **Micro Edition**.

6. (Optional) When creating a Standard Edition instance, on the **Quota increase** page, apply for additional quota as prompted. For a description of quota costs, see [Billing items](https://docs.byteplus.com/en/docs/cr/billing-items?lang=en).

7. View the instance specification comparison and configuration costs. After confirming that everything is correct, click **Confirm Order**.

8. On the **Confirm order** page, confirm the order information again, then carefully read and check **I have read and agree to Container Registry Product Terms of Service**.

9. Click **confirm** to submit the order and start creating the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the instance creation progress on the <strong>Instances</strong> page. When the <strong>Instance Status</strong> is <strong>Running</strong>, it indicates that the instance has been created successfully.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

When logging in to the CR instance for the first time, you can complete the initialization of the CR instance using the setup wizard. For operation details, see  [Initialize instance ](https://docs.byteplus.com/en/docs/cr/initialize-an-instance).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* For a detailed description of Instance billing, see [product billing](https://docs.byteplus.com/en/docs/cr/billing-overview).

* For methods to create an Instance using Terraform, see [Create instance](https://docs.byteplus.com/en/docs/cr/Creating_a_Standard_Edition_Instance?lang=en).
