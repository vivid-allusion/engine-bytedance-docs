---
title: "UpdateVpcEndpoint"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/updatevpcendpoint"
---

Update the VPC access endpoint.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request address: https://cr.cn\-beijing.byteplusapi.com.cn?Action=UpdateVpcEndpoint&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateVpcEndpoint |The API name. The current API name is `UpdateVpcEndpoint`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |test\-cr |The name of the Container Registry instance. |
|Vpcs |Array of [VpcMeta](https://docs.byteplus.com/en/docs/65/26087#vpcmeta) |no |[{"VpcId": "vpc\-3rfawyc34g0sg5zsk2idd\*\*\*\*"}] |Specifies which VPCs can access this Standard Edition Container Registry instance. For specific fields, you may refer to the definition of [VpcMeta](https://docs.byteplus.com/en/docs/cr/data-structures-of-requests#vpcmeta) in the general data structure. Each time UpdateVpcEndpoint is called, this field should contain all the VPCs for which you want to enable access endpoints. |


<span id="vpcmeta"></span>
### VpcMeta


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|VpcId |String |Yes |vpc\-3rfawyc34g0sg5zsk2idd\*\*\*\* |The VPC ID. The Container Registry instance will configure the access endpoint within this VPC. |
|SubnetId |String |no |subnet\-jhhsrhjjdfssi\*\*\*\* |The subnet ID under the VPC. If not specified, the subnet with the most remaining IP addresses in the VPC will be automatically selected, and it cannot be changed afterwards. |
|AccountId |Long |no |1400000001 |The ID of the root user to which the VPC belongs. This ID needs to be specified when exposing a Standard Edition instance to a VPC under another root user. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=UpdateVpcEndpoint&Version=2022-05-12
{
    "Registry": "test-cr",
    "Vpcs": [
        {
            "VpcId": "vpc-2331",
            "SubnetId": "subnet-09665"
        },
        {
            "VpcId": "vpc-2334",
            "SubnetId": "subnet-8764",
            "AccountId": 1400000037
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "UpdateVpcEndpoint",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
|400 |OperationDenied.Status |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current access endpoint status. Please wait for the status transition to complete and try again. |
