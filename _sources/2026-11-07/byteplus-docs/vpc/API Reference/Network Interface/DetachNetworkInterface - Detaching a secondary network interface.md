---
title: "DetachNetworkInterface - Detaching a secondary network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface"
---

Call the DetachNetworkInterface API to detach the secondary network interface from the specified Elastic Compute Service (ECS) instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The ECS instance must be in the **Running** or **Stopped** state to support detaching a network interface.

* The primary network interface and [BytePlus Official service network interface](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview#.572R5Y2h57G75Z6L) cannot be detached.

* DetachNetworkInterface is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) API to check the status of the network interface. `Detaching` means the network interface is being detached. `Available` means the network interface has been successfully detached.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DetachNetworkInterface&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|CjwY9h">必选</span> `Example value: DetachNetworkInterface`

The interface name. The current API name is `DetachNetworkInterface`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|LOT3zW">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**NetworkInterfaceId ** <span data-label="purple"> String </span><span data-api-tag="require|NIDXIb">必选</span>`Example value: eni-bp1fgnh68xyz9****`

Secondary network interface ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.



**InstanceId ** <span data-label="purple"> String  </span><span data-api-tag="require|8iSYq3">必选</span> `Example value: i-wijfn35c****`

ID of the ECS.

You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the ID of the ECS instance.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DetachNetworkInterface&Version=2020-04-01&NetworkInterfaceId=eni-bp1fgn8xyz9****&InstanceId=i-wijfn35c**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DetachNetworkInterface",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEni.InstanceMismatch |The specified elastic network interface is not attached to the specified instance. |The specified elastic network interface is not bound to the ECS instance. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface cannot process this request. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS instance is in a state that cannot process this request. |
|400 |InvalidTrafficMirrorSession.InvalidStatus |The specified traffic mirror session is not in the correct status for the request. |The specified traffic mirror session is in a state that cannot process this request. |
|400 |InvalidVpcEip.InUse |The specified vpc eip is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified elastic network interface does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified ECS instance does not exist. |
