---
title: "Preview and Custom Domains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/preview-and-custom-domains_en"
---

This document describes the preview capability in Pages and explains how to configure a custom domain for a project.

<span id="preview-the-deployment-result"></span>
## Preview the Deployment Result

After a project is created and deployed, Pages provides preview capabilities:


* You can access the project from the **Preview** entry on the project list page.

* You can also view the preview thumbnail and preview URL in the **Preview** section on the project details page.

* Even if you did not specify a custom domain when creating the project, the platform still provides a preview address that can be used to verify the deployment result.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The platform\-assigned preview URL is reset every 3 hours and cannot be used as a stable access address. If you need a stable access address, bind a custom domain.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521082343-1252205549354.png) </span>

<span id="configure-a-custom-domain"></span>
## Configure a Custom Domain

You can configure a custom domain at either of the following stages:


* When creating the project, enter the domain in **Acceleration Settings**.

* After the project is created, click **Add** in **Overview \> Domain Management**.


To configure a custom domain:


1. In the **Domain Management** section, click **Add**.

2. In the **Add Domain** dialog box, enter the domain and optionally select **Auto\-Generate Free Certificate**.

3. After you click **OK**, the system first prepares the domain configuration.

4. After preparation is complete, the corresponding `CNAME` value appears in the domain list.

5. Go to your DNS provider console and add a `CNAME` record based on the information provided by Pages.

6. Return to the Pages console and click **Verify** in the **Actions** column for the domain.

7. In the **DNS Settings** dialog box, confirm the **Record Type**, **Host**, and **Record Value**, and then click **Verify**.

8. After verification succeeds, the domain may briefly display **Publishing**. During this stage, Pages continues to complete domain publishing, certificate binding, and edge configuration distribution. After publishing is complete, the site can be accessed through the custom domain.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Immediately after a domain is added, <code>DNS Record</code> may temporarily display <strong>Configuring</strong>. The console shows the <code>CNAME</code> value for DNS configuration only after preparation is complete.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521082611-507395136996.png) </span>

<span id="example-add-a-cname-record-in-godaddy"></span>
## Example: Add a CNAME Record in GoDaddy

The following steps use GoDaddy as an example:


1. Sign in to **Domain Portfolio** in GoDaddy.

2. Select the domain to configure and open the **DNS Management** page.

3. Click **Add New Record** and set **Type** to **CNAME**.

4. Enter the following information:

   * **Name**: Enter your subdomain, for example, `www`.

   * **Value**: Enter the CNAME address provided by the Pages console.

   * **TTL**: Use the default value or adjust it as needed.

5. Click **Save**.
