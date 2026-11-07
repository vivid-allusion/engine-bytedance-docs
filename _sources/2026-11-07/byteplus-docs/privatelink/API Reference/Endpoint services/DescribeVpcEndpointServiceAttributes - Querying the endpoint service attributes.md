---
title: "DescribeVpcEndpointServiceAttributes - Querying the endpoint service attributes"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes"
---

Call the DescribeVpcEndpointServiceAttributes API to query detailed information of the endpoint service.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointServiceAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|VGAElX">必选</span> `Example: DescribeVpcEndpointServiceAttributes`

Action to execute. Set the value to **DescribeVpcEndpointServiceAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ohn7go">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple">String </span><span data-api-tag="require|0y0Mep">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**ServiceId** <span data-label="purple">String</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.



**ServiceName ** <span data-label="purple">String </span>`Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name.



**ServiceNameManaged ** <span data-label="purple">String </span>`Example: false`

Whether the endpoint service is managed.


* false: Non\-managed endpoint service.

* true: Managed endpoint service.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned when the account to which the endpoint service belongs has not enabled the managed endpoint service feature.</div>




**ServiceDomain ** <span data-label="purple">String </span>`Example: epsvc-2fe630gurkl37k5gfuy33****.cn-guangzhou.privatelink.volces.com`

Service domain name of the endpoint service.



**AutoAcceptEnabled** <span data-label="purple">Boolean</span> `Example: false`

Auto\-accept endpoint connection.


* true: The endpoint service automatically accepts endpoint connection requests.

* False: The endpoint service does not automatically accept endpoint connections; you need to manually accept them by calling the [EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) API.



**ServiceType ** <span data-label="purple">String </span>`Example: Interface`

Endpoint service type.


* Interface: Interface endpoint service.



**Payer ** <span data-label="purple">String </span>`Example: Endpoint`

The account that pays for PrivateLink.


* Endpoint: Endpoint account.

* EndpointService: Endpoint service account.



**BillingType ** <span data-label="purple">Integer </span>`Example: 0`

Billing method of endpoint service.


* 0: No charge.

* 3: Pay\-as\-you\-go.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

Whether the endpoint service is locked.


* Normal

* FinancialLocked: Being locked.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When this parameter returns empty, it indicates that the endpoint service is not locked.</div>




**IpAddressVersions** <span data-label="purple">String[]</span> `Example: ipv4`

IP protocol type of the endpoint service.


* If the return value contains only **ipv4**, it indicates that the endpoint service is of IPv4 type, supporting only IPv4 services.

* If the return value contains both **ipv4** and **ipv6**, it indicates that the endpoint service is of dual\-stack type, supporting both IPv4 and IPv6 services simultaneously.



**ServiceResourceType ** <span data-label="purple">String </span>`Example: CLB`

Service resource type.


* CLB: Classic Load Balancer.

* ALB: Application Load Balancer.

* RDSMySQL: Cloud Database MySQL Edition.



**ZoneIds ** <span data-label="purple">String[] </span>`Example: cn-guangzhou-a`

The availability zones in which the endpoint service provides its service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter returns a null value when the <code>ServiceResourceType</code> parameter returns <strong>RDSMySQL</strong>.</div>




**Description ** <span data-label="purple">String </span>`Example: endpoint service`

Description of the endpoint service.



**PrivateDNSEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Indicates whether the private DNS name is enabled for the endpoint service.


* false: Disabled.

* true: Enabled.



**PrivateDNSName ** <span data-label="purple">String </span>`Example: www.example.com`

Private DNS name of the endpoint service.

This parameter returns empty when the `PrivateDNSEnabled` parameter returns **false**.



**PrivateDNSType ** <span data-label="purple">String </span>`Example: public`

Domain type of private DNS name.


* Public: Internet.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned when the custom private domain name feature is not enabled.</div>




**PrivateDNSNameConfiguration ** <span data-label="purple">Object </span>`Example: --`

The configuration information of the private DNS name for the endpoint service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned when <code>PrivateDNSType</code> is <strong>private</strong>.</div>



**Name ** <span data-label="purple">String </span>`Example: _2fe6iz2tou9s059gp68um****`

Domain verification name.



**Status ** <span data-label="purple">String </span>`Example: PendingVerification`

Domain verification status.


* Pending verification

* Verifying

* Verified

* Failed: Verification failed



**Type ** <span data-label="purple">String </span>`Example: TXT`

Domain validation type.


* TXT: TXT record.



**Value ** <span data-label="purple">String </span>`Example: epsvc:2fe6iz4spybr459gp67fb****`

Domain validation value.




**CreationTime** <span data-label="purple">String</span> `Example: 2021-07-20T03:32:32+08:00`

Creation time of the endpoint service.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-09-20T03:32:32+08:00`

The deletion time of the endpoint service.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-07-20T03:32:32+08:00`

Last operation time of the endpoint service.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the endpoint service.


* Creating

* Pending: Modifying configuration.

* Available

* Deleting



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the endpoint belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the endpoint service.


**Key ** <span data-label="purple">String </span>`Example: k1`

Tag key of the endpoint service tag.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value of the endpoint service tag.




**SupportedRegions ** <span data-label="purple">String[] </span>`Example: cn-beijing`

The region where the endpoint service is published. Endpoints in that region can establish connections with this endpoint service.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpcEndpointServiceAttributes&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcEndpointServiceAttributes",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AutoAcceptEnabled": true,
        "BillingType": 0,
        "BusinessStatus": "Normal",
        "CreationTime": "2021-07-20T03:32:32+08:00",
        "DeletedTime": "2021-09-20T03:32:32+08:00",
        "Description": "endpoint service",
        "IpAddressVersions": [
            "ipv4",
            "IPv6"
        ],
        "Payer": "Endpoint",
        "PrivateDNSEnabled": true,
        "PrivateDNSName": "www.example.com",
        "PrivateDNSNameConfiguration": {
            "Name": "_2fe6iz2tou9s059gp68um****",
            "Type": "TXT",
            "Value": "epsvc:2fe6iz4spybr459gp67fb****",
            "Status": "PendingVerification"
        },
        "PrivateDNSType": "public",
        "ProjectName": "default",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "ServiceDomain": "epsvc-2fe630gurkl37k5gfuy33****.cn-guangzhou.privatelink.volces.com",
        "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
        "ServiceName": "com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****",
        "ServiceNameManaged": "false",
        "ServiceResourceType": "CLB",
        "ServiceType": "Interface",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-07-20T03:32:32+08:00",
        "ZoneIds": [
            "cn-guangzhou-a",
            "cn-guangzhou-b"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Here, XXX represents the name of the missing parameter.</div><br> |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
