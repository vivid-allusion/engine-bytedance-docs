---
title: "Notice Regarding Consolidating Access to Torch Object Storage Storage Lens Under DevMind"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Notice_Regarding_Consolidating_Access_to_Torch_Object_Storage_Storage_Lens_Under_DevMind"
---

To improve the storage data analytics experience further, the BytePlus Torch Object Storage (TOS) team plans to consolidate access to **Storage Lens** under [DevMind](https://docs.byteplus.com/en/docs/tos/DevMind-overview?lang=en). DevMind offers a centralized location for Usage Statistics, Log Analysis, Storage Lens, and Insight Assistant. Log Analysis and Storage Lens are powered by [CloudLens for TOS](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en) from Torch Log Service (TLS). Together, these features provide a one\-stop service for analyzing storage data and making informed decisions.

<span id="cYapTcjY"></span>
## Estimated Change Time

**2026\-09\-01**. Please refer to the console for the specific time.

<span id="zlBYIWF7"></span>
## Change Description

The following changes apply after access to Storage Lens is consolidated under DevMind.


|Item |Description |
|---|---|
|TOS console |Storage Lens will no longer be available as a standalone menu option. Its existing capabilities can be accessed from **DevMind** \> **Storage Lens**. |
|Billing |In the new console, **DevMind** \> **Storage Lens** is powered and billed by CloudLens for TOS from TLS. For more information, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce). |


<span id="K7j8qCMo"></span>
## Impacts


|Category |Description |
|---|---|
|Console access |Starting on **September 1, 2026**, the **Storage Lens** menu option will be removed from the console. To use this feature with newly created buckets or existing buckets that have not yet enabled Storage Lens, navigate to **DevMind** \> **Storage Lens** \> **Dashboards**. |
|Billing |* TOS charges [Storage Lens monitoring fees](https://docs.byteplus.com/docs/tos/Storage-analytics) when you use Storage Lens dashboards with advanced features in the original console.<br><br>* After Storage Lens becomes available in **DevMind** \> **Storage Lens**, TLS charges fees based on the applicable billing rules. For more information, see [Billing notes](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en#4fe96fce). |
|Features |* Unfortunately, existing Storage Lens dashboards cannot be transferred. We recommend recreating them in **DevMind \> Storage Lens** after the change **.** <br><br>* New Storage Lens dashboards provide similar capabilities to the original dashboards, but are powered and billed by [CloudLens for TOS](https://docs.byteplus.com/en/docs/tls/CloudLens_for_TOS?lang=en). |
|Existing users |* Historical data and dashboards: To maintain business continuity, historical analytics data and configured dashboard rules are retained if Storage Lens is enabled before **September 1, 2026**. Your workloads will not be affected in the short term.<br><br>* Transition period and gradual switch: The transition period ends on **November 30, 2026**. We recommend gradually starting to use the new menu and testing the upgraded analytics capabilities. After the transition period ends, the original menu will no longer be accessible or supported. |


<span id="MTzwaLZK"></span>
## Reach Us

If you have any questions about the changes, [submit a ticket](https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000245) or contact your account manager for assistance.
