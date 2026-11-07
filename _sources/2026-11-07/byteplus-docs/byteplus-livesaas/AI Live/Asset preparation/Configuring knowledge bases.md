---
title: "Configuring knowledge bases"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/configuring-product-kb"
---

To enable your AI figure to provide accurate, real\-time answers during livestreams, you need to create a knowledge base. This guide explains the two types of knowledge bases—product\-level and general—and provides step\-by\-step instructions on how to prepare content and upload files for each. Following these steps will ensure your AI has rich, relevant information to draw from for any audience question.

## Key features

* **Product\-level precise Q&A**: Configure a separate knowledge base for each product. The AI figure references it only when presenting that product, preventing cross\-product answers.

* **Live\-room\-wide Q&A**: A general knowledge base stays in effect throughout the entire livestream, covering cross\-product information such as brands and events.

* **Automatic product information ingestion**: When you create a product, the system automatically creates its product knowledge base and adds the product information to it—no manual setup required.

* **Multi\-file, multi\-format support**: Upload documents such as TXT, DOC, DOCX, PDF, MD, Markdown, PPT, PPTX, XLSX, CSV, and JSONL, as well as images such as JPEG, JPG, PNG, WEBP, and BMP, to give the AI rich material to learn from.

## Knowledge base types

The knowledge base for AI Live has two types, which differ in scope.

|**Knowledge base type** |**Bound to** |**Scope of effect** |
|---|---|---|
|**Product knowledge base** |An individual product |Referenced only when the AI figure is presenting that product. It is not referenced when presenting other products. |
|**General knowledge base** |The entire live room (Account\-level) |Once configured for the live room, it is referenced throughout the entire livestream, regardless of which product is being presented. |

> **说明**

> The two types of knowledge bases are meant to be used **together**: when the AI figure answers a question, it simultaneously identifies relevant content from both the current product’s knowledge base and the general knowledge bases, then selects usable information from both to generate the response.

## Preparing knowledge base content

Prepare materials according to the knowledge base type, and upload only the information relevant to its scope.

### Supported formats and limits

Knowledge base supports TXT, DOC, DOCX, PDF, MD, Markdown, PPT, PPTX, XLSX, CSV, and JSONL, as well as images such as JPEG, JPG, PNG, WEBP, and BMP. The following document formats have limits:

|**Document format** |**Size limit** |
|---|---|
|ppt (.ppt/.pptx) |up to 200 MB |
|TXT, markdown (.markdown/.md) |up to 10 MB |
|Xlsx, csv, jsonl |no more than 30,000 lines |

### Product knowledge base

When you create a product, the system automatically creates the corresponding product knowledge base and adds the product information (product name, product ID, product image, sale price, product description, product category, selling points, promotional information, and detailed information) to it. You can then upload additional content in addition to this, for example:

* **Specifications and parameters**: Detailed spec sheets, size/color/version charts, and compatibility notes.

* **Usage and after\-sales**: User manuals, installation and operation steps, warranty policy, return and exchange rules, and shipping times and coverage.

* **Selling points and differentiation**: Comparisons with similar products or your other models, certifications and test reports, and target audiences and use cases.

* **Reviews and trust**: Selected customer reviews, awards, and media coverage.

* **Product\-specific offers**: Discounts, gifts, bundles, and limited\-time deals for this product. (Put livestream\-wide event rules in a general knowledge base.)

### General knowledge base

Upload information that applies to the entire live room, for example:

* **Brand information**: Brand introduction, brand story, qualifications, and so on.

* **Livestream event information**: Event rules, promotion periods, and offer mechanics for the current livestream.

## Uploading knowledge base files

### Prerequisites

* **Activate the service**: You have activated AI Live. To activate the service, contact sales as described in [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods).

* A BytePlus account or an IAM user. For more information on how to add IAM users, see [Adding IAM users, organizations, or roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

* To upload a product knowledge base, first add the corresponding product in the **Product Library**. For details, see [Managing product library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-products-for-digital-human-livestreams).

### Step 1: Upload a product knowledge base

1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **AI Live** in the top navigation bar.

3. In the left navigation bar, click **Knowledge base** to open the page.

4. In the product list on the left, select the product for which you want to configure a knowledge base. You can use the **Search product** box at the top to find it by name.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b57ec03a48a4a638608a5a5f737a9d6~tplv-goo7wpa0wc-image.image)

5. On the right, click  **+ Upload File** to upload the knowledge base file for that product.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb7fd3f58f2a4b739e981d8ed7cc1e89~tplv-goo7wpa0wc-image.image)

6. After the upload completes, the file appears in the product's knowledge base file list, with a green checkmark on the right indicating it is in effect. To remove it, click the delete icon to the right of the file.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e74a576a68fa46b09ff27773f2846d93~tplv-goo7wpa0wc-image.image)

> **注意**

> The product knowledge base is bound to the product: when a product is deleted, its product knowledge base is deleted at the same time.

### Step 2: Upload a general knowledge base

1. On the **Knowledge base** page, click the **General** tab.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb4e75dc6e5340599c7c86248eddd31a~tplv-goo7wpa0wc-image.image)

2. Click  **+ Add** to create a new general knowledge base and give it a name.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74200cb525e84422b679438b4fa0ae03~tplv-goo7wpa0wc-image.image)

3. Select the general knowledge base you just created, and click  **+ Upload File** on the right to upload general materials such as brand information, livestream event information, and product lists. BytePlus Live provides a bilingual (Chinese and English) General Knowledge Base template for your use.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13f60195f96d42e4aab066edcef7ada1~tplv-goo7wpa0wc-image.image)

## Next steps

In the live room's **Reply Setting**, the knowledge base is enabled as follows:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbdb5b8253d347aab9a5f0d89bb1f631~tplv-goo7wpa0wc-image.image)

* **Product knowledge base**: Automatically synced with the products added to the live room. You do not need to add or remove it manually.

* **General knowledge base**: Not enabled by default. You need to manually select which general knowledge bases take effect for the current livestream.

For details, see [Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream).

## FAQs

**Q: I uploaded a knowledge base file, but why doesn't the AI reference its content when answering?**

A: Check whether the knowledge base type matches the intended scope. A product knowledge base takes effect only when the corresponding product is being presented. If you want the information to be available throughout the entire livestream, upload it to a general knowledge base.

**Q: Do I need to create the product knowledge base manually?**

A: No. When you create a product, the system automatically creates the corresponding product knowledge base and adds the product information to it. You only need to upload additional files as needed.
