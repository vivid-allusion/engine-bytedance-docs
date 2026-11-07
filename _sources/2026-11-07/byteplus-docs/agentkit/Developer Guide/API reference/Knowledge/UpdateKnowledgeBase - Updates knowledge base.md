---
title: "UpdateKnowledgeBase - Updates knowledge base"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateKnowledgeBase_-_Updates_knowledge_base"
---

You can call this operation to update knowledge bases.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|i6Wfh4">必选</span> `Sample value: UpdateKnowledgeBase`

The action that you want to perform. Value: UpdateKnowledgeBase.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|NIoHmw">必选</span>  `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Description**<span data-label="purple"> string </span>`Optional Sample value: sample description.`

Description of the knowledge base.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* If left blank, the parameter defaults to an empty value.

* Separate multiple field names with ampersands (&).



**KnowledgeId ** <span data-label="purple">string </span><span data-api-tag="require|D8qleu">必选</span> `Sample value: kb-123`

Knowledge base ID.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* Separate multiple field names with ampersands (&).


Value:


* For a Viking knowledge base, use ResourceId.



**VpcConfig.SubnetIds.N ** <span data-label="purple">string[] </span>`Optional Sample value: ["subnet-1", "subnet-2"]`

List of subnet IDs.


* Each subnet occupies one IP for creating a network interface card.

* Pass in multiple subnets to achieve high availability of VPC connections.

* Only one subnet can be passed in for each availability zone.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

Knowledge base ID.



**ProviderKnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

ID of the imported knowledge base.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_KNOWLEDGE`

Type of the knowledge base platform. Value:


* VIKINGDB_KNOWLEDGE: Viking knowledge base.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=UpdateKnowledgeBase&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "KnowledgeBases":[
      {
        "ProviderType": "VIKINGDB_KNOWLEDGE",
        "VpcConfig.VpcId": "vpc-257gqcdfvx6n****"
      }
    ],
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateKnowledgeBase",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "KnowledgeId": "kb-4yds45***",
    "ProviderKnowledgeId": "kb-ye7s2g****",
    "ProviderType": "VIKINGDB_KNOWLEDGE"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |LimitExceeded.MinimumSubnetIds |The number of specified SubnetIds exceeds the minimum limit. |The specified SubnetIds exceeds the lower limit. |
|400 |MissingParameter.KnowledgeId |The required parameter KnowledgeId is not supplied. |The parameter KnowledgeId cannot be empty. |
|400 |MissingParameter.VpcId |The required parameter VpcId is not supplied. |The parameter VpcId cannot be empty. |
