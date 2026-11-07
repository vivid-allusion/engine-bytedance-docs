---
title: "ListGtms"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/CrGpNh"
---

Gets a list of GTM instances.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=ListGtms&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListGtms` |The name of the API. The value of this parameter is `ListGtms`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|Domain |String |No |`www.example.com` |The domain name of the GTM instance, for example, `www.example.com`.<br><br>Default is empty, meaning this parameter is not used as a query condition. |
|Cname |String |No |`www.example.com.bpgslb001.com` |The routing domain name of the GTM instance.<br><br>Default is empty, meaning this parameter is not used as a query condition. |
|Remark |String |No |`Remark` |The remark of the GTM instance.<br><br>Default is empty, meaning this parameter is not used as a query condition. |
|SearchMode |String |No |`like` |The query mode. Includes the following modes:<br><br><br>* **like**: (Default) Fuzzy query.<br><br>* **exact**: Exact query. |
|PageNumber |Integer |No |`1` |The page number. Default is 1. The number of pages is determined by the total number of GTM instances retrieved and the `PageSize`. |
|PageSize |Integer |No |`50` |The number of GTM instances per page. Default is 50.<br><br>BytePlus GTM will display the retrieved GTM instances in pages. The number of pages is determined by the total number of GTM instances retrieved and the `PageSize`. |
|SortOrder |String |No |`asc` |The sorting order of the GTM instance list.<br><br><br>* **asc**: Ascending order.<br><br>* **desc**: (Default) Descending order. |
|SortBy |String |No |`Domain` |The value used for sorting.<br><br><br>* **Domain**: The domain name of the GTM instance.<br><br>* **Cname**: The routing domain name of the GTM instance.<br><br>* **State**: The status of the GTM instance.<br><br>* **Remark**: The remark of the GTM instance.<br><br>* **UpdateTime**: (Default) The update time of the GTM instance.<br><br>* **CreateTime**: The creation time of the GTM instance. |

## Response body

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID of this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|TotalCount |Integer |Total number of GTM instances. |
|PageNumber |Integer |Page number for pagination. |
|PageSize |Integer |Number of GTM instances per page. |
|Data |Array of Objects |List of GTM instances. |
|GtmId |String |UUID of the GTM instance. |
|Domain |String |Domain name of the GTM instance. |
|Cname |String |Routing domain of the GTM instance. |
|PolicyType |String |Type of policy. The available values are:<br><br><br>* geo: Basic policy.<br><br>* perf: Intelligent policy. |
|Ttl |Integer |The expiration time of the DNS record. The unit is seconds. |
|Remark |String |Remarks for the GTM instance. |
|AlarmId |String |ID of the alert rule bound to this GTM instance. |
|AccessMode |String |Connection mode of the GTM instance.<br><br><br>* cname: BytePlus GTM automatically generates a routing domain based on your domain name. According to your configuration in BytePlus GTM, the routing domain is resolved to the address’s IP or domain name. You need to create a CNAME record with your DNS service provider and point your domain name to this routing domain.<br><br>* domain: Resolve your domain name to the target address’s IP or domain name. This connection mode can only be used if your domain name’s DNS service provider is BytePlus DNS. |
|CreateTime |String |Creation time of the GTM instance, accurate to milliseconds. The format complies with the ISO 8601 standard. |
|UpdateTime |String |Most recent modification time of the GTM instance, accurate to milliseconds. The format complies with the ISO 8601 standard. |
|State |String |This parameter is invalid. Please ignore this parameter. |
|Owner |String |BytePlus account of the user who created this GTM instance. |
|LastOperator |String |BytePlus account of the last user who operated this GTM instance. |
|SpecName |String |Edition of the GTM instance. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=ListGtms&Version=2023-01-01&PageNumber=1&PageSize=1
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20240722065033A59118D3AD7C1B0B6628",
        "Action": "ListGtms",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 50,
        "Data": [
            {
                "GtmId": "fd5277c1-74ea-4ff8-aa44-0020bc612e1c",
                "Domain": "example.com",
                "Cname": "",
                "PolicyType": "geo",
                "Ttl": 600,
                "Remark": "",
                "AlarmId": "",
                "AccessMode": "domain",
                "CreateTime": "2024-07-22T06:46:14.499Z",
                "UpdateTime": "2024-07-22T06:46:14.499Z",
                "State": "init",
                "Owner": "30*****2",
                "LastOperator": "30*****2",
                "SpecName": "ultimate"
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
