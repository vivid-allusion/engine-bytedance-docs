---
title: "Adding third-party product library"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/adding-third-party-product-library"
---

BytePlus Live supports adding products from external platforms like TikTok Shop, Shopify, or other store systems so that your AI figure host is able to promote and explain merchandise during livestreams. This guide provides step\-by\-step instructions on how to configure and authorize product libraries from platforms like TikTok Shop, Shopify, or your own in\-house system.

<span id="8ee628bc"></span>
## Prerequisite

Subscribe to the AI Live service: Refer to [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method) and contact sales to subscribe to the AI Live service.

<span id="187bcea3"></span>
## Procedure

Follow these steps to set up your product library.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Authorization** in the top navigation bar.

3. In the left navigation bar, click **Integrations** \> **Product Library** to open the page.

4. On the **Product Library** page, click **Product library management**.

   The **Product library management** panel opens on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5994cec42d74a01983101dceb49c279~tplv-goo7wpa0wc-image.image) </span>

5. Click  **+Add product library** and enter a **Product Library Name**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33dd68758fc34113bd01a82cb4b96fa9~tplv-goo7wpa0wc-image.image) </span>

6. Select the **Product library type**. Once you set the type, you cannot change it.

   
   <Tabs>
   <Tab zoneid="V4Sc8LthS9" title="TikTok Shop">
   <TabTitle>TikTok Shop</TabTitle>
   
   Click **Go to authorize**. Select your region and authorized shop.
   
   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de817af0167e46d788639e1791d30e2d~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="RkyeXL2OU3" title="Shopify">
   <TabTitle>Shopify</TabTitle>
   
   Enter your domain name and public access token:
   
   
      * **Domain name**: The domain name of your Shopify store.
   
         To get the domain name, click Settings on the left navigation pane of your Shopify store to view the domain name under the store name. You can also click Settings \> Domains to view the domain name on the Domains page.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aa4e1b2fc5349e184af839897ce7db9~tplv-goo7wpa0wc-image.image) </span>
   
      * **Public access token**: The public access token for the Storefront API of your Shopify store.
   
         To get the token, navigate to the **Headless sales channel** page in your Shopify store.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc45a5e3e8b4813b7218b86c6e766be~tplv-goo7wpa0wc-image.image) </span>
   
         Click **Manage** to view the public access token on the Storefront API page.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/084b594a5b10486f8af763fe4f1fddfc~tplv-goo7wpa0wc-image.image) </span>
   
         Click the Save icon.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f44dec36f7a94a829864eecee2d0441d~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="dlCiTDo6XN" title="In-house system">
   <TabTitle>In-house system</TabTitle>
   
   Enter the request URL used to retrieve products from the product library.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">You must develop an API according to the specifications to integrate your system with BytePlus Live before adding a product library from your in\-house system. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#f4985fe1">Integrating your system with BytePlus Live</a>.</div>
   
   
   
   </Tab>
   </Tabs>
   


<span id="2295e0c8"></span>
## Next step

Now you can add products to BytePlus Live from the product library. For details, see [Step 2: Add products manually or from a product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams#c85b3d40).
