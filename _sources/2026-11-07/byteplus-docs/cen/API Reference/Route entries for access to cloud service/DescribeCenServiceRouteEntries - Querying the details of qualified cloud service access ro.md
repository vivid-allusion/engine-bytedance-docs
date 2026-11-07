---
title: "DescribeCenServiceRouteEntries - Querying the details of qualified cloud service access routes"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenServiceRouteEntries"
---

Call the DescribeCenServiceRouteEntries API to query details of cloud service access routes that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenServiceRouteEntries&groupName=%E4%BA%91%E6%9C%8D%E5%8A%A1%E8%AE%BF%E9%97%AE&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|y3a4Tt">必选</span> `Example: DescribeCenServiceRouteEntries`

Action to execute. Set the value to DescribeCenServiceRouteEntries.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Max9sB">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span>`optional` `Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to get the CEN instance ID.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 10`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**DestinationCidrBlock ** <span data-label="purple">string </span>`optional` `Example: 100.XX.XX.0/24`

The address of the cloud service. It must belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR block.



**ServiceRegionId ** <span data-label="purple">string </span>`optional` `Example: cn-beijing`

The region of cloud service.



**ServiceVpcId ** <span data-label="purple">string </span>`optional` `Example: vpc-3rlkeggyn6tc010exd32q****`

VPC instance ID used to access the cloud service.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC instance ID.



**CenRouteEntryIds.N ** <span data-label="purple">string[] </span>`optional` `Example: rte-7qthudw0ll6jmc****`

The route ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 1`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of qualified route entries.



**ServiceRouteEntries ** <span data-label="purple">object[] </span>`Example: --`

Details of cloud service route entry.


**DestinationCidrBlock ** <span data-label="purple">string </span>`Example: 100.XX.XX.0/24`

The address where the cloud service is deployed. It must belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR block.



**CenId ** <span data-label="purple">string </span>`Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.



**ServiceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region of cloud service.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the cloud service route entry.


* Available

* Pending: ​​Configuration in progress.

* Creating

* Deleting



**PublishMode ** <span data-label="purple">string </span>`Example: Custom`

Publish scope of cloud service route entry.


* LocalDCGW: Indicates that the cloud service route entry is automatically published to all Direct Connect Gateways in the region where the cloud service is deployed that are attached to the CEN instance.

* Custom: Indicates that you manually specify the network instances to which the cloud service route entry needs to be published.



**CreationTime ** <span data-label="purple">string </span>`Example: 2022-04-28T22:57:03+08:00`

Creation time of the cloud service route entry.



**Description ** <span data-label="purple">string </span>`Example: test-service-route`

Description of the cloud service route entry.



**PublishToInstances ** <span data-label="purple">object[] </span>`Example: --`

Publish information of cloud service route entry.


**InstanceId ** <span data-label="purple">string </span>`Example: vpc-uf6o8d1dj8sjwxi6o****`

Network instance ID to which the cloud service route entry is published.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

Region to which the cloud service route entry is published.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

Network instance type to which the cloud service route entry is published.


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.




**ServiceVpcId ** <span data-label="purple">string </span>`Example: vpc-uf6o8d1dj8sjwxi6o****`

VPC ID used to access the cloud service.




&nbsp;



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 1`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of qualified route entries.



**ServiceRouteEntries ** <span data-label="purple">object[] </span>`Example: --`

Details of cloud service route entry.


**DestinationCidrBlock ** <span data-label="purple">string </span>`Example: 100.XX.XX.0/24`

The address where the cloud service is deployed. It must belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR block.



**CenId ** <span data-label="purple">string </span>`Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.



**ServiceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region of cloud service.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the cloud service route entry.


* Available

* Pending: ​​Configuration in progress.

* Creating

* Deleting



**PublishMode ** <span data-label="purple">string </span>`Example: Custom`

Publish scope of cloud service route entry.


* LocalDCGW: Indicates that the cloud service route entry is automatically published to all Direct Connect Gateways in the region where the cloud service is deployed that are attached to the CEN instance.

* Custom: Indicates that you manually specify the network instances to which the cloud service route entry needs to be published.



**CreationTime ** <span data-label="purple">string </span>`Example: 2022-04-28T22:57:03+08:00`

Creation time of the cloud service route entry.



**Description ** <span data-label="purple">string </span>`Example: test-service-route`

Description of the cloud service route entry.



**PublishToInstances ** <span data-label="purple">object[] </span>`Example: --`

Publish information of cloud service route entry.


**InstanceId ** <span data-label="purple">string </span>`Example: vpc-uf6o8d1dj8sjwxi6o****`

Network instance ID to which the cloud service route entry is published.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

Region to which the cloud service route entry is published.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

Network instance type to which the cloud service route entry is published.


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.




**ServiceVpcId ** <span data-label="purple">string </span>`Example: vpc-uf6o8d1dj8sjwxi6o****`

VPC ID used to access the cloud service.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCenServiceRouteEntries&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082608Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151637480191550171457F2BB8",
    "Action": "DescribeCenServiceRouteEntries",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 1,
    "TotalCount": 1,
    "ServiceRouteEntries": [
      {
        "DestinationCidrBlock": "100.XX.XX.0/24",
        "CenId": "cen-2nim00ybaylts7trquyzt****",
        "ServiceRegionId": "cn-beijing",
        "Status": "Available",
        "PublishMode": "Custom",
        "CreationTime": "2022-04-28T22:57:03+08:00",
        "Description": "test-service-route",
        "PublishToInstances": [
          {
            "InstanceId": "vpc-uf6o8d1dj8sjwxi6o****",
            "InstanceRegionId": "cn-beijing",
            "InstanceType": "VPC"
          }
        ],
        "ServiceVpcId": "vpc-uf6o8d1dj8sjwxi6o****"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
