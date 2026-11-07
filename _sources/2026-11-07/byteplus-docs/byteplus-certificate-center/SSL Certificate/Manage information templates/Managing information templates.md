---
title: "Managing information templates"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-managing-information-templates"
---

When submitting a certificate request, you need to provide contact information so that the CA can contact you to verify your certificate request. You can save the contact information and enterprise information as an information template in the Certificate Center, making it convenient for you to use when submitting certificate requests next time. This article introduces how to manage information templates in the Certificate Center console.

You can manage information templates on the **Information template** page.

<span id="creating-a-template"></span>
## Creating a template


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation bar, select **SSL Certificate** \> **Templates**.

3. On the **Information templates** page, click **Create template**.

4. In the **Create information template** panel, select the **Type**.

   * If you plan to use the template to request a DV certificate, select **Individual**.

   * If you plan to use the template to request an OV or EV certificate, select **Organization**.

5. In the **Basic information** section, enter the template name, contact person's name, email, and phone number.

6. In the **Organization information** section, enter the organization name, department, and country where the organization is registered, and other information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Organization information</strong> section only appears when the <strong>Type</strong> is <strong>Organization</strong>.   </div>
   

7. Click **Create**.


After the template is created successfully, you can view the created templates in the information template list.

<span id="modifying-a-template"></span>
## Modifying a template

If you need to modify the information in an information template, you can find the template in the information template list and click **Edit** in the **Actions** column. After updating the information in the template, click **Save**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying an information template will not affect the certificate requests that have already been submitted using the template. The information template is only for your convenience when entering relevant information when submitting certificate requests. Once the certificate request is submitted, it is no longer associated with the information template.</div>


<span id="deleting-a-template"></span>
## Deleting a template

If you no longer need an information template, you can find the template in the information template list and click **Delete** in the **Actions** column.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting an information template will not affect the certificate requests that have already been submitted using the template.</div>
