---
title: "Quota Overview"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Quota_Overview"
---

The quota center is used to centrally manage the resource quotas of each cloud service under an account. You can check the quota limit and resource usage in the quota center, and apply to change the quotas and set alert rules as needed.

<span id="basic-concept"></span>
## Basic concept


|Concept |Description |
|---|---|
|Quota |The maximum amount of cloud resources that can be used by a BytePlus account. Resources cannot be purchased or created after this limit is exceeded. |
|Quota parameter |The object of quota management for a cloud service. For example, vpc, vpc/subnet, vpc/route_table, and other quota parameters of private network products. |
|Quota dimension |Quota parameters can be managed in a more granular manner based on three dimensions: region, payment type, and regional attribute. A quota parameter can be subdivided into different quota items based on different dimensions. |
|General quota |The default quota type, in which the quota item contains only one quota dimension, namely, region. |
|Instance quota |Quota items of this type contain three quota dimensions, namely, region, regional attribute, and payment type. |
|Resource usage |The resource usage corresponding to the current quota item. |
|Quota application |The application initiated when you want to increase the quota. The backend administrators will review your quota application, and the corresponding quota can be increased after approval. |
|Quota alert |The quota alert policy configured when you want to receive an alert message once the usage reaches the threshold. |
|Quota template |The template used to automatically submit multiple quota change applications at one time for new members under the organization for your enterprise account. |


<span id="quota-support"></span>
## Quota support

Only cloud products that support quota management can be managed in the quota center. For information about products that support quota management, go to [Quota center](https://console.byteplus.com/quota/productList).
