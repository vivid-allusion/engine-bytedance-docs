---
title: "GetVpcEndpoint"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/getvpcendpoint"
---

Query the VPC access endpoint information.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=GetVpcEndpoint&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetVpcEndpoint |The API name. The current API's name is `GetVpcEndpoint`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |test\-cr |The name of the Container Registry instance. |
|Filter |Object of [VpcEndpointFilter](https://docs.byteplus.com/en/docs/65/26090#vpcendpointfilter) |no | |The filtering conditions for querying VPC access endpoints. |


<span id="vpcendpointfilter"></span>
### VpcEndpointFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Statuses |Array of String |no |["Enabling", "Enabled"] |An array of VPC access endpoint statuses, used to filter out VPC access entries that are in the specified statuses.<br><br><br>* **Enabling**: turning on<br><br>* **Enabled**: turned on<br><br>* **Disabling**: turning off<br><br>* **Failed**: failed |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=GetVpcEndpoint&Version=2022-05-12
{
    "Registry": "test-cr"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |test\-cr |The name of the Standard Edition instance. |
|Vpcs |Array of [VpcInfo](https://docs.byteplus.com/en/docs/65/26090#vpcinfo) |[{"VpcId":"vpc\-2331","SubnetId": "subnet\-09665","Status": "Enabling","Ip": "10.7.6.5"}] |The filtering conditions for querying VPC access endpoints. |


<span id="vpcinfo"></span>
### VpcInfo


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|VpcId |String |vpc\-luebclsohfwnljn\*\*\*\* |VPC ID. |
|SubnetId |String |subnet\-nlohebas\*\*\*\* |The ID of the subnet. |
|Region Code |String |cn\-beijing |The region where the VPC is located. |
|AccountId |Long |14000\*\*\*\*\* |The ID of the root user to which the VPC belongs. |
|Ip |String |192.168.12.33 |The IP address of the Container Registry within the VPC. |
|Status |String |Enabled |The status of the access endpoint:<br><br><br>* Enabling: turning on<br><br>* Enabled: turned on<br><br>* Disabling: turning off<br><br>* Failed: failed |
|CreateTime |String |2022\-05\-20T13:00:55Z |The creation time. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "GetVpcEndpoint",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "Registry": "test-cr",
        "Vpcs": [
            {
                "VpcId": "vpc-2331",
                "SubnetId": "subnet-09665",
                "Status": "Enabling",
                "Ip": "10.7.6.5"
            },
            {
                "VpcId": "vpc-2334",
                "SubnetId": "subnet-8764",
                "Region": "cn-nantong",
                "Status": "Running",
                "Ip": "100.64.11.12"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
