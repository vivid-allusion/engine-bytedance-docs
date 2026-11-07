---
title: "DeleteSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteSharedConfig_en"
---

Delete an existing universal catalog.

<span id="prerequisites"></span>
## Prerequisites

Before deleting a universal catalog, please ensure it is not associated with any domain names. To delete a universal catalog, follow these steps:


1. Call [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_en) to get the domain names associated with the universal catalog.

2. For **each** domain name associated with the universal catalog, perform the following steps:

   1. Call [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus\-cdn/reference\-duplicatetemplate https://docs.byteplus.com/en/docs/byteplus\-cdn/reference\-duplicatetemplate) to duplicate the delivery policy bound to the domain name.

   2. For the newly created policy, call [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateservicetemplate) to modify the policy, ensuring that the relevant CDN feature configurations do not reference the universal catalog. You can refer to [universal catalog](https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en) to understand which CDN features can reference universal catalogs.

   3. Call [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27) to bind the newly created delivery policy to the domain name.

3. Call DeleteSharedConfig to delete the universal catalog.


If an IAM user receives the error `The configuration is associated with domain names and cannot be deleted` when calling this API, and the IAM user does not actually find any associated domain names when calling [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_en), it is possible that the IAM user does not have permission to access the domain names associated with the universal catalog. In this case, the primary account needs to disassociate the universal catalog from the domain names, and then the IAM account can delete the universal catalog.

<span id="usage-limits"></span>
## Usage Limits

Rate Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DeleteSharedConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |Yes |Indicates the name of a universal catalog. See [Prerequisites](https://docs.byteplus.com/en/docs/18/36377#prerequisites).<br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get the names of existing universal catalogs. |`my_list` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021-03-01
{
    "ConfigName": "my_list"
}
```
