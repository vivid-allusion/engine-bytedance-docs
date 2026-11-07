---
title: "Managing product library"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams"
---

To let your AI figure host promote and explain merchandise during automated livestreams, you can manage everything through a product\-centric **Product Library** in BytePlus Live. It allows you to maintain a shared library of products, sync them from sources such as TikTok Shop, Shopify, and your own in\-house system, and automatically build a per\-product knowledge base for intelligent replies to audience questions. This guide explains how to create a product library, add products from different sources, and manage your products.

## Prerequisites

* Subscribe AI Live service: Refer to [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/subscription-billing-method) and contact sales to subscribe AI Live service.

* A BytePlus account or an IAM user with the following permissions. For more information on how to add IAM users, see [Adding IAM users, organizations, or roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

   * **Producer** \> **Edit** permission: Used to add and configure the menu for product cards.

   * **Live control** \> **View** permission: Used to configure product cards on the **Live control** page.

## Procedure

Follow these steps to set up your product library, add products, and manage them.

### (Optional) Step 1: Integrate a product library from TikTok Shop, Shopify, or your own system

To enable your AI avatar to present products synced from external platforms like TikTok Shop, Shopify, or other store systems, you must first create a product library for that channel.

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **AI Live** in the top navigation bar.

3. In the left navigation bar, click **Product Library** to open the page.

4. On the **Product Library** page, click **Product library management**.

   The **Product library management** panel opens on the right.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1487d4aca4da49c19cc9e5d42637fa26~tplv-goo7wpa0wc-image.image)

5. Click  **+Add product library**, enter a **Product Library Name**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33dd68758fc34113bd01a82cb4b96fa9~tplv-goo7wpa0wc-image.image)

6. Select the **Product library type**. Once you set the type, you cannot change it.

   **TikTok Shop**

**TikTok Shop**: Click **Save** directly and then click **Go to authorize**. Select your region and authorized shop.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48f7f444e195490b84f9eeab70e3b954~tplv-goo7wpa0wc-image.image)

   **Shopify**

Enter your domain name and public access token:

      * **Domain name**: The domain name of your Shopify store.

         To get the domain name, click Settings on the left navigation pane of your Shopify store to view the domain name under the store name. You can also click Settings \> Domains to view the domain name on the Domains page.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aa4e1b2fc5349e184af839897ce7db9~tplv-goo7wpa0wc-image.image)

      * **Public access token**: The public access token for the Storefront API of your Shopify store.

         To get the token, navigate to the **Headless sales channel** page in your Shopify store.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc45a5e3e8b4813b7218b86c6e766be~tplv-goo7wpa0wc-image.image)

         Click **Manage** to view the public access token on the Storefront API page.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/084b594a5b10486f8af763fe4f1fddfc~tplv-goo7wpa0wc-image.image)

         Click the Save icon.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f44dec36f7a94a829864eecee2d0441d~tplv-goo7wpa0wc-image.image)

   **In-house system**

Enter the request URL used to retrieve products from the product library.

   > **注意**

   > You must develop an API according to the specifications to integrate your system with BytePlus Live before adding a product library from your in\-house system. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#f4985fe1).

### Step 2: Add products manually or from a product library

You can add products from BytePlus Live, external platforms, or manually. To add products from external platforms, make sure you have completed the step above.

#### Add products from a product library

1. On the **Product Library** page, click  **+Add from product library**.

   The **Add from product library** drawer opens on the right.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/566a0f7490754882af53e3a7e5dcfc3b~tplv-goo7wpa0wc-image.image)

2. Select a product library and then add products for AI Live.

   * **Live**: Select products from live rooms. For an IAM user, make sure you have the **Live control** \> **View** permission for the target room.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c31e63eccb5436597b1862ea6099290~tplv-goo7wpa0wc-image.image)

   * **Other platforms**: After you complete step 1, you will see the product library you added. Click the product cards and then click **Add** to add them to your AI Live. The following image shows an example of selecting products from a Shopify store.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3339f06ce70b4cf49f6b8b8e05af41e8~tplv-goo7wpa0wc-image.image)

#### Create a product manually

You can also create a product manually here for your avatar to present.

1. On the **Product Library** page, click **Create manually**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2de25b7602744890b4cc955c6d2265e3~tplv-goo7wpa0wc-image.image)

   The **Create** **manually** panel opens on the right.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c25cafbe9b0b48ec99e0de854d70e930~tplv-goo7wpa0wc-image.image)

2. Fill in the product fields.

   |**Field** |**Description** |
   |---|---|
   |Product name |Display name of the product. Up to 300 characters. |
   |Product ID |Unique identifier of the product. Up to 256 characters. |
   |Product image |Main product image. Recommended 1:1 aspect ratio. Upload a JPG or PNG file no more than 2 MB. |
   |Sale price |Selling price of the product, for example `99.99`, `500 JPY`, or `100 USD`. |
   |Product description |Detailed product information. Up to 10,000 characters. |
   |Product category |The category the product belongs to. Use it to classify products. You can set 2 levels at most. |
   |Product selling points |Key selling points for the products. Up to 600 characters. |
   |Promotional information |Promotional information for the product. Up to 600 characters. |
   |Detail information |Additional product details for the knowledge base. |

3. Click **OK** to save the product to the library.

### Step 3: Manage your products

Added products appear in the list, where you can review the **Product image**, **Product name**, **Product ID**, **Sale price**, **Product category**, and **Promotional information** columns. Use the search box at the top to find products by name, ID, or category.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82f509e8d1c74eec9ad6e88c4679bd27~tplv-goo7wpa0wc-image.image)

In the **Operate** column of each product, you can:

* **Edit**: Modify any field except the **Product ID**.

* **Knowledge base**: Open the product's knowledge base page to manage or upload knowledge base files. For more information, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

* **Delete**: Remove the product. The product's associated knowledge base is also deleted. To remove several products at once, select them and click **Batch delete**.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c0e64faa48d4674937c840a0f2cb475~tplv-goo7wpa0wc-image.image)

## Next steps

When you add a product, the system automatically creates a matching product knowledge base and writes the product details into it. To upload more knowledge base content, click the product's **Knowledge base** entry in the list. For more information, see [Configuring knowledge bases](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-product-kb).

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c6f5df413da405880b55a6d067a67e0~tplv-goo7wpa0wc-image.image)

## FAQs

**Q: Can a product library be shared across multiple live rooms?**

A: Yes. A product library is scoped to an IAM user, so every live room under that user can reuse the same library.

**Q: How many product libraries can one sub\-account have?**

A: Up to 10.

**Q: Can I edit product details after syncing them from BytePlus Live?**

A: Yes. Every field except the Product ID can be edited. Your changes apply only to the copy in the product library.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bfe526467d845658f9138166b440d62~tplv-goo7wpa0wc-image.image)

**Q: What happens to a product's knowledge base when I delete the product?**

A: The knowledge base is also deleted. A product knowledge base is associated with its product, so removing the product also removes its knowledge base.
