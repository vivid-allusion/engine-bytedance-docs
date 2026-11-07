---
title: "Add your domain name"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-your-domain-name"
---

To have BytePlus CDN accelerate the distribution of your site's content, you first need to add your site's domain name to the CDN service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This guide provides step\-by\-step instructions for adding and configuring your domain name in the BytePlus CDN console.</div>



1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Domain Names**.

3. On the **Domain Names** page, click **Add Domain Name**.

4. On the **Add Domain Name** page, enter `www.example.com` in the **Domain Name** field.

5. Under **Delivery Policy**, select the delivery policy you just created.

6. Set **Encryption** to **Enabled**, select the certificate you just uploaded from the certificate list, and then click **OK**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_71960deb9b81a3df4c7ba7755f98f77e.png) </span>


On the **Domain Names** page, the domain name you just added will appear in the domain list.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_16924d30c9e640a1dd34ff05085714a8.png) </span>

Please note the **CNAME** column, which contains **www.example.com.bplslb.com**. This CNAME is used to route requests for your site through CDN. At the end of this tutorial, we will guide you on how to set this up.

Next, we will test your domain name.
