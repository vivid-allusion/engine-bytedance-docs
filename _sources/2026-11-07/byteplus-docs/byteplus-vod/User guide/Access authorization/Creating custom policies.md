---
title: "Creating custom policies"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-custom-policy"
---

If the default system policies for BytePlus VOD do not meet your needs, you can create custom policies for more precise permission management. This guide provides step\-by\-step instructions for creating a custom policy, details the required JSON syntax, and offers practical examples to help you get started.

<span id="4fa40efc"></span>
## **Prerequisites**

Before reading this article, make sure you have a solid understanding of the key concepts of access authorization. For details, see [Creating a sub-account ](https://docs.byteplus.com/docs/byteplus-vod/docs-creating-iam-users).

<span id="4a8f887a"></span>
## **Procedure**


1. Sign in to the [BytePlus IAM console](https://console.byteplus.com/iam/create_user/name).

2. On the left navigation pane, click **Policy management**.

3. Click **New Custom Policy**.

4. Enter the policy description and content. For how to write the policy content, see [Policy syntax](https://docs.byteplus.com/docs/byteplus-vod/docs-creating-custom-policy#c7747c5f).

5. Click **Submit**.


<span id="c7747c5f"></span>
## Policy syntax

Policies are described through PolicyDocument in JSON format. A policy syntax includes the following elements:


|**Element** |**Description** |
|---|---|
|Statement |The `Statement` element is the main and required element of a policy. It can contain an individual statement only or an array of individual statements.<br><br>Each individual statement block must be placed in curly brackets ({ }). For multiple statements, the array must be placed in square brackets ([ ]). |
|Effect |The `Effect` element is required. It indicates the result of the statement. Its valid values are `Allow` or `Deny`. |
|Action |The `Action` element describes the specific action. It has the same meaning as the `Action` parameter in a cloud service API. Therefore, when describing the `Action` element, it is necessary to describe the specific cloud service in the prefix `{service}:{action}`. `*` and `?` are supported when describing the `Action` element. For BytePlus VOD, the prefix is `vod`. |
|Resource |The `Resource` element specifies the resource that the `Action` element covers. It is described in TRN format: `trn:{service}:{region}:{account}:{resourceType}/{resourceID}`. The components of the format are as follows:<br><br><br>* `trn`: The fixed prefix.<br><br>* `{service}`: The abbreviation of the cloud service's name. For BytePlus VOD, the prefix is `vod`.<br><br>* `{region}`: The region where the cloud service is deployed.<br><br>* `{account}`: The ID of the account that the cloud resource belongs to.<br><br>* `{resourceType}`: The type of cloud resource. For BytePlus VOD, the resource type can be:<br><br>   * `space`: For this type, you need to specify the space name. See [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).<br><br>      * Format: `trn:{service}::{account}:{resourceType}/{spaceName}`<br><br>      * Example: `trn:vod::3000000004:space/test`<br><br>   * `app`: For this type, you need to specify the app ID. See [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).<br><br>      * Format: `trn:{service}::{account}:{resourceType}/{appId}`<br><br>      * Example: `trn:vod::3000000004:app/123456`<br><br>   * `license_group`: For this type, you need to specify the license package ID. See [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).<br><br>      * Format: `trn:{service}::{account}:{resourceType}/{licenseId}`<br><br>      * Example: `trn:vod::3000000004:license_group/1123456` |


<span id="0b5df0f3"></span>
## **Policy examples**


|**Policy name** |**Policy content** |
|---|---|
|`${ProductName}FullAccess` |Grants full access to all APIs within the BytePlus VOD service. Wildcard `*` can be used to represent all APIs. Example:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "vod:*"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
|`${ProductName}ReadOnlyAccess` |Grants access only to read APIs within the BytePlus VOD service, excluding write APIs. Based on the API naming convention, read APIs are prefixed with "List" or "Get". Example:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "vod:List*",```<br>```        "vod:Get*"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
|`${ProductName}${ModuleOrRole}Access` |Grants access to APIs within the specified module. Wildcards can be used to represent repeated parts. For example, if the API names all contain the `Resource` field in the middle, it can be expressed as:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "vod:*Resource*"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
|`${ProductName}ProductFullAccess` |Allows access to a specific space only:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "vod:*"```<br>```      ],```<br>```      "Resource": [```<br>```           "trn:vod::21000xxxxx:space/1633341028192xxxxxx"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
