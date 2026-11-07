---
title: "UpdateMemory - Modifies memory information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateMemory_-_Modifies_memory_information"
---

You can call this API to modify the memory description and strategy information.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|9nMu1s">必选</span> `Sample value: UpdateMemoryCollection`

The action that you want to perform. Value: UpdateMemoryCollection.



**Version**<span data-label="purple"> string</span>  <span data-api-tag="require|YzTcEw">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Description ** <span data-label="purple">string </span>`Optional Sample value: memory-test`

Description of the memory. Maximum length: 200 characters.



**LongTermConfiguration.Strategies.N.Name ** <span data-label="purple">string[] </span><span data-api-tag="require|aMe6hC">必选</span> `Sample value: s_1`

Name of the LTM extraction strategy.


* Parameter \- N: Indicates the serial number of the strategy. Value range: 1–5.

* Separate multiple field names with ampersands (&).


Naming rules:


* Can only contain English characters [A\-Za\-z], numbers, and underscores (_).

* It must be 1 to 48 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Strategy names must be unique within the same memory.</div>




**LongTermConfiguration.Strategies.N.Type ** <span data-label="purple">string[] </span><span data-api-tag="require|TVeNQL">必选</span> `Sample value: Summary`

Type of the LTM extraction strategy.


* Parameter \- N: Indicates the serial number of the strategy. Value range: 1–5.

* Separate multiple field names with ampersands (&).

* Value:

   * Summary: Session summary (session level).

   * Semantic: Semantic memory (user level).

   * UserPreference: User preference (user level).



**LongTermConfiguration.Strategies.N.CustomExtractionInstructions ** <span data-label="purple">string[] </span>`Optional Sample value: Summarize facts.`

The system prompt for a custom strategy.


* Parameter \- N: Indicates the serial number of the strategy. Value range: 1–5.

* Maximum length: 8,000 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A strategy without a system prompt is a built\-in strategy. Each strategy type can have at most one built\-in strategy.</div>




**MemoryId ** <span data-label="purple">string </span><span data-api-tag="require|7FU3G0">必选</span> `Sample value: mem-17616225****`

Memory ID.



**VpcConfig.VpcId ** <span data-label="purple">string </span><span data-api-tag="require|6IaKVC">必选</span> `Sample value: vpc-257gqcdfvx6n****`

VPC ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once set, this parameter cannot be changed.</div>




**VpcConfig.SubnetIds.N ** <span data-label="purple">string[]</span>` Optional Sample value: ["subnet-1", "subnet-2"]`

List of subnet IDs.


* Each subnet uses one IP address to create a network interface.

* Specify multiple subnets to achieve high availability of the VPC connection.

* You can specify at most one subnet per availability zone. For the MEM0 type, only one subnet is allowed in total.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LongTermConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Updated LTM information.


**Strategies ** <span data-label="purple">object[] </span>`Sample value: --`

Information about the LTM extraction strategies.


**CustomExtractionInstructions ** <span data-label="purple">string </span>`Sample value: --`

List of LTM extraction strategies.



**Name ** <span data-label="purple">string </span>`Sample value: my_collection`

Memory name.



**Type ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Memory type. Value:


* VIKINGDB_MEMORY: Viking LTM.





**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-17616225****`

Memory ID.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: mem-294775****`

ID of the imported memory.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Memory type. Value:


* VIKINGDB_MEMORY: Viking LTM.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=UpdateMemoryCollection&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "MemoryId": "mem-17611386****",
    "Description": "new Description",
    "LongTermConfiguration":{
      "Strategies":[
        {
          "Type": "Summary",
          "CustomExtractionInstructions": "Extract key information from conversation",
          "Name": "agentkit_semantic_v1"
        }
      ]
    }
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateMemoryCollection",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MemoryId": "mem-17611386****",
    "ProviderCollectionId": "mem-294775****",
    "ProviderType": "VIKINGDB_MEMORY",
    "LongTermConfiguration": {
      "Strategies": [
        {
          "Type": "Summary",
          "CustomExtractionInstructions": "Extract key information from conversation",
          "Name": "agentkit_semantic_v1"
        }
      ]
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |LimitExceeded.MinimumSubnetIds |The number of specified SubnetIds exceeds the minimum limit. |The number of specified SubnetIds exceeds the lower limit. |
|400 |MissingParameter.MemoryId |The required parameter MemoryId is not supplied. |The parameter MemoryId cannot be empty. |
|400 |MissingParameter.VpcId |The required parameter VpcId is not supplied. |The parameter VpcId cannot be empty. |
|400 |InvalidParameter.InvalidSubnets |The specified subnet(s) is invalid. |The specified subnet is invalid. Please verify the subnet. |
|400 |InvalidParameter.Mem0VpcConfig |The specified Mem0 VPC configuration is invalid. Only one subnet is allowed. Mem0 VPC does not allow update. |The specified Mem0 VPC configuration is invalid. Only one subnet is allowed. |
|400 |InvalidParameter.UpdateVpcNotAllowed |Ajust memory or knowledge VPC ID is not allowed. |The VPC ID of the knowledge base or memory cannot be modified. |
|400 |OperationDenied.TooManyVpcUpdates |Too many VPC updates. Please try later. |VPC updates are too frequent. Please try again later. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |
