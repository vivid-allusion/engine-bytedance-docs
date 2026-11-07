---
title: "Set up delivery policy and origin"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-distribution-policy-and-origin"
---

To begin delivering your site's content with BytePlus CDN, you must first create a delivery policy and configure its origin. This guide provides step\-by\-step instructions on how to create a policy, add your origin server, and publish the configuration to activate content delivery.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document is based on the scenario described in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_1">Overview</a>.</div>



1. Create a delivery policy.

   1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

   2. In the left navigation bar, click **Delivery Policies**.

   3. On the **Delivery Policies** page, click **Create Policy**.

   4. On the **Create Delivery Policy** page, enter `Test_Policy` in the **Policy Name** field, set **Project** to **default**, and then click **OK**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_10a76641b879bc3124331630ef8ac6c6.png) </span>

2. Set up the origin.

   1. On the **Origins** tab, click **Add Origin**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7ecf077ec373b953bb11b1a753e4040a.png) </span>

   2. On the **Add Origin** page, make the following settings, and then click **OK**.

      * Set **Origin Category** to **Primary Origin**.

      * Set **Origin Type** to **IP Address**.

      * Enter `203.0.113.8` in the **Origin Address** field.

         <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6ecd65b1ae01b3c95babd3e025fa9c76.png) </span>

3. On the **Delivery Policy Details** page, click **Save**.

   On the **Delivery Policies** page, the new policy appears in the policy list.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_64c6da395d5b396ff5bed25ea913f2ea.png) </span>

4. Publish the policy.

   1. In the **Actions** column for the policy, click **Publish**.

   2. In the **Confirm Operation** dialog, click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Published policies cannot be modified. If the configuration in a published policy is incorrect, you can create a new policy by duplicating it. In the new policy, you can modify the relevant settings and then publish the new policy.</div>


Next, let's upload your site's certificate to CDN.
