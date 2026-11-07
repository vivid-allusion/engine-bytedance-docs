---
title: "Limits"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Limits"
---

The following describes the quantity limit rules for AS scaling group\-related features.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the default quotas shown in the table below do not meet your requirements, please contact your account manager for modification.</div>



|Resource type |Limit item (one region) |Quantity limit |
|---|---|---|
|Scaling group |The maximum number of scaling groups that can be created for one account |100. The maximum number is 200. You can adjust the number via the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling). |
|Scaling configuration source |The maximum number of scaling configurations that can be created for one scaling group |100 |
||The maximum number of instance types that can be selected for one scaling configuration source |10 |
||The number of scaling configuration sources that can be associated with one scaling group at the same time |1 |
|Instance |The maximum number of instances that can be created and added to one scaling group |500. The maximum number is 1000. You can adjust the number via the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling). |
||The maximum number of instance types that can be selected for one scaling configuration |10 |
|Scaling rule |The maximum number of scaling rules that can be created for one scaling group |10 |
|Lifecycle hook |The maximum number of lifecycle hooks that can be created for one scaling group |6 |
|Vertical scaling |The maximum number of vertical scaling tasks one primary account can create in one region |100. The maximum supported number is 200. You can adjust the number via the[ Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling). |
|RDS instance |The maximum number of RDS instances that can be associated with one scaling group |40 |
