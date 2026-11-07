---
title: "DescribeVpcEndpointServices - Querying the endpoint service list"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices"
---

Call the DescribeVpcEndpointServices API to query the list of endpoint services that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointServices&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ZIyuvJ">必选</span> `Example: DescribeVpcEndpointServices`

Action to execute. Set the value to **DescribeVpcEndpointServices**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Fn7N9F">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries. Maximum: 100. Default: 10.



**ServiceName ** <span data-label="purple">String </span>`optional` `Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name. Format: com.volces.privatelink. *<regionID\>* . *<endpointserviceID\>* .



**ServiceType ** <span data-label="purple">String </span>`optional` `Example: Interface`

Endpoint service type.


* Interface: Interface endpoint service.



**ServiceIds.N ** <span data-label="purple">String </span>`optional` `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.


* Parameter \-N: Indicates the serial number of the endpoint service ID, ranging from 1 to 100.

* Separate multiple endpoint service IDs with ampersands (&).



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which the endpoint service belongs.



**ServiceResourceType ** <span data-label="purple">String </span>`optional` `Example: CLB`

The type of service resource associated with the endpoint service. Valid values:


* CLB: Classic Load Balancer.

* ALB: Application Load Balancer.

* RDSMySQL: Cloud Database MySQL Edition.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature of PrivateLink supporting ALB and RDS type service resources is currently in beta stage. If you need to use it, please contact your account manager.</div>




**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns endpoint services tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns endpoint services that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


<div data-tips="true" data-tips-type="tip">When an empty string is passed, it indicates querying ALB instances with empty tag values.</div>




**ServiceRegions.N ** <span data-label="purple">String </span>`optional` `Example: cn-beijing`

The region where the endpoint service is published. Endpoints in that region can establish connections with this endpoint service. For the region ID, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of rows on the current page.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of endpoint services matching the specified conditions.



**VpcEndpointServices ** <span data-label="purple">Object[] </span>`Example: --`

Details of endpoint service.


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

The configuration information of the private DNS name for the endpoint service. For detail, see the table **PrivateDNSNameConfiguration**.

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

* Available: Available for use.

* Deleting: In the deleting process.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the endpoint belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the endpoint service.


**Key ** <span data-label="purple">String </span>`Example: k1`

Tag key of the endpoint service tag.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value of the endpoint service tag.




**SupportedRegions ** <span data-label="purple">String[] </span>`Example: ["cn-beijing","cn-shanghai"]`

The region where the endpoint service is published.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpcEndpointServices&Version=2020-04-01&ProjectName=default HTTP/1.1
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
        "Action": "DescribeVpcEndpointServices",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "TotalCount": 2,
        "VpcEndpointServices": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Payer": "Endpoint",
                "Status": "Available",
                "ZoneIds": [
                    ""
                ],
                "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
                "UpdateTime": "2021-07-20T03:32:32+08:00",
                "BillingType": 0,
                "DeletedTime": "2021-09-20T03:32:32+08:00",
                "Description": "endpoint service",
                "ProjectName": "default",
                "ServiceName": "com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****",
                "ServiceType": "Interface",
                "CreationTime": "2021-07-20T03:32:32+08:00",
                "ServiceDomain": "epsvc-2fe630gurkl37k5gfuy33****.cn-guangzhou.privatelink.volces.com",
                "BusinessStatus": "Normal",
                "PrivateDNSName": "www.example.com",
                "PrivateDNSType": "public",
                "SupportedRegions": [
                    "cn-beijing",
                    "cn-shanghai"
                ],
                "AutoAcceptEnabled": false,
                "IpAddressVersions": [
                    ""
                ],
                "PrivateDNSEnabled": false,
                "ServiceNameManaged": "false",
                "ServiceResourceType": "CLB",
                "PrivateDNSNameConfiguration": {
                    "Name": "_2fe6iz2tou9s059gp68um****",
                    "Type": "TXT",
                    "Value": "epsvc:2fe6iz4spybr459gp67fb****",
                    "Status": "PendingVerification"
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.EndpointServices |You've reached the limit on the number of EndpointServices that you can operate. |The quota for the number of endpoint services that can be operated on in a single request has been reached. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
