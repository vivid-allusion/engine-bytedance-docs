---
title: "Create image signature"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Create_image_signature"
---

Image signature for container images attaches a digital signature to container images using cryptographic algorithms. This is used to verify the integrity (not tampered with) and authenticity (trusted source) of the image, and is an important means to ensure the security of the image supply chain.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This feature is currently in beta. To use it, please submit an application. Part of the product features are provided in beta. To use beta features, please contact <strong>your account manager or after\-sales engineer</strong>.</div>


* <div data-tips="true" data-tips-type="default">This action is only applicable to Standard Edition instances.</div>



<span id="ml1cG0su"></span>
## Background

CR supports the image signature feature for container images, integrating asymmetric keys from [Key Management Service (KMS)](https://docs.byteplus.com/en/docs/kms/What_is_Key_Management_Service) to enable automatic signing, binding and unbinding at the namespace level, as well as manual signing for individual image tags.

<span id="C9wDDKpb"></span>
## Comparison of signing methods


|**Item** |**Create a signature rule (namespace level)**  |**Manual signing (image tag)**  |
|---|---|---|
|Application scenario |To enable global policy\-based management of image signatures. To automatically sign all **newly pushed** images under the namespace. This is suitable for pipeline\-based automatic release processes to ensure image security and reliability. |To flexibly sign or supplement the signature for specified image tags. To sign **existing images** or specific image tags individually. This is suitable for on\-demand signing or supplementing signatures for historical images. |
|Signing method |After the signature rule is created, it is triggered automatically; no manual intervention is required. |On the image tag list page, manually select the target image tag to add a signature. |
|Signing scope |At the namespace level, after the rule takes effect, all newly pushed images under the namespace are automatically signed. |Image tag level; supports signing a single image tag. |
|Prerequisites |An image signature rule must be created first. |The target namespace must have an associated image signature rule. |


<span id="NhuXP3OG"></span>
## Create signature rule

After creating a signature rule, new images pushed under the namespace will be automatically signed.

<span id="pWL8oKx4"></span>
### Prerequisites


* Created a namespace. For operation details, see [Create namespace](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

* Created an asymmetric key with key type RSA_2048 and key purpose SIGN_VERIFY. For creation methods, see [Key Management](https://docs.byteplus.com/en/docs/kms/Key_hosting).


<span id="J5FhjIjE"></span>
### Considerations


* Only one signature rule can be associated with a namespace.

* After the signature rule is created successfully, all new images pushed under the namespace will automatically trigger signing.

* Signature rules cannot be modified after creation. To make changes, delete the original rule and re\-create it.


<span id="PH75zQvM"></span>
### Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. Select a rule to create a path.

   
   <Tabs>
   <Tab zoneid="yzhnYPHH" title="Image signature module">
   <TabTitle>Image signature module</TabTitle>
   
   1. Click **Image signature** in the left navigation bar.
   
   2. On the **Image signature** page, click **Create image signature**.
   
   
   </Tab>
   <Tab zoneid="KxuUJ24NUJ" title="Namespace module">
   <TabTitle>Namespace module</TabTitle>
   
   1. Click **namespace** in the left navigation bar.
   
   2. On the **namespace** page, click **Actions** in the target namespace column, then click **Image signature**.
   
   
   </Tab>
   </Tabs>
   

3. Configure the image signature rule parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule name |Enter the signature rule name. |
   |Signature scope |Select the namespace where the image signature rule will take effect. |
   |KMS key |Select the KMS asymmetric key used for signing. |
   

4. Click **Confirm** to complete creation.


<span id="AWeQ42g6"></span>
## Manual signing

For image tags that existed before the creation of the image signature rule (existing images), or when it is necessary to sign a specific artifact repository tag, use the manual signing feature.

<span id="by9ni3Pk"></span>
### Prerequisites

The image signature rule has been created. For operation details, see [Create image signature rule](https://docs.byteplus.com/en/docs/cr/Create_image_signature#NhuXP3OG).

<span id="k0B80biU"></span>
### Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the namespace list, click the OCI artifact repository under the target namespace to enter the image tag list page.

3. Select the target image tag, and click **Actions** in the Actions column, then **Image signature**.

4. In the secondary confirmation dialog box, click **Confirm** to complete the signing operation.
