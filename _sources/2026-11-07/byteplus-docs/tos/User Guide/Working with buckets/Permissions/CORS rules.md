---
title: "CORS rules"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-cross-origin-resource-sharing-settings"
---

You can set cross\-origin resource sharing (CORS) rules in the TOS console. When TOS receives a cross\-origin request or OPTIONS request, it will read the CORS rules of the bucket, perform permission checks, and return corresponding headers to ensure the security of cross\-origin data transmission.

<span id="9vvkPdf1"></span>
## Notes

By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).


* Configure/Delete CORS rules: `tos:PutBucketCORS`

* View CORS configurations: `tos:GetBucketCORS`


<span id="c9021420"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission Management \> CORS rules**. On the **CORS rules** page, click **Create Rule**.

4. On the **Create CORS Rule** page, configure the following parameters:

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |Origin |Yes |Specify the allowed origins of cross\-origin requests. Restrictions:<br><br><br>* List IP addresses or domains, where port numbers are allowed.<br><br>* The https:// or http:// prefix must be carried.<br><br>* You can type multiple items that are separated by pressing Enter. Each item occupies one line.<br><br>* Each line can contain only one wildcard asterisk ( `*` ).<br><br>* You can type up to 1,000 items. |
   |Operation methods |Yes |Specify one or more cross\-origin request methods that are allowed, including **PUT**, **GET**, **POST**, **DELETE**, and **HEAD**. |
   |Allow\-Headers |No |Specify allowed cross\-origin request headers. Restrictions:<br><br><br>* You can type multiple items that are separated by pressing Enter. Each item occupies one line.<br><br>* You can type up to 1,000 items.<br><br>* We recommend that you use the wildcard asterisk ( `*` ) to indicate that all headers are allowed, if applicable. |
   |Expose\-Headers |No |Specify additional headers in CORS responses exposed to clients to provide extra information. Restrictions:<br><br><br>* You can type multiple items that are separated by pressing Enter. Each item occupies one line.<br><br>* The wildcard asterisk ( `*` ) cannot be used. |
   |Cache Max\-Age |No |Specify the maximum amount of time before the OPTIONS request response remains fresh in the client. Unit: seconds. Default value: 3,600. |
   |Return Vary:Origin |No |Specify whether to return the Vary:Origin header. If a browser has both CORS and non\-CORS requests, you can enable this feature to avoid cross\-origin issues. However, enabling it may increase browser access requests or CDN back\-to\-origin traffic. |
   

5. Click **Create**.

   The created CORS rule will be displayed in the rule list.


<span id="b0038e34"></span>
## Further operations


* **Editing a CORS rule**: Click **Edit** in the **Actions** column of the target rule.

* **Deleting a CORS rule**: Click **Delete** in the **Actions** column of the target rule and then click **Delete** in the pop\-up dialog box.
