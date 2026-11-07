---
title: "ListLines"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listlines"
---

Gets the list of ISP lines, geolocation lines, and cloud vendor lines provided by BytePlus DNS.

## Usage

* Rate limit: Maximum 50 calls per second.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListLines&Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListLines` |The name of the API. The value of this parameter is `ListLines`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|PageSize |Integer |No |`2000` |The number of lines per page. The system will display the retrieved lines in pages. The number of pages is determined by the total number of retrieved lines and `PageSize`. The value range for this parameter is 1 ~ 2000. The default value of this parameter is `2000`. |
|PageNumber |Integer |No |`1` |The page number. The API returns the lines included in this page number. The default value of this parameter is `1`. |
|Hierarchy |String |No |`true` |Whether to return lines by hierarchy. This parameter has the following values:<br><br><br>* `true`: Return lines by hierarchy. The results will show parent lines and child lines.<br><br>* `false` (default): Do not return lines by hierarchy. Parent lines and child lines are returned at the same level. |
|ZID |Integer |No |`1234` |Represents the ID of a domain name. Based on the edition of the instance where your domain name is located, BytePlus DNS returns the lines available for that edition. If you do not set this parameter, BytePlus DNS returns all lines by default. |

## Response body

### ResponseMetadata object

|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result Object

|Name |Type |Description |
|---|---|---|
|TotalCount |Integer |The total number of returned lines. This parameter value is not affected by the `PageNumber` parameter. Suppose the `PageNumber` you specified does not contain any lines. In this case, the `Lines` parameter will not display any lines. However, `TotalCount` will still show the total number of lines actually obtained by this API. |
|PageSize |Integer |The number of lines contained in each page. |
|PageNumber |Integer |The page number where the `Lines` are displayed. |
|Lines |Object Array |List of lines. |
|ID |String |The ID of the line. |
|Name |String |The name of the line. |
|Value |String |The code of the line. If you need to specify the `Line` parameter in a called API, you need to use the value of the `Value` parameter to represent the corresponding line. |
|FatherValue |String |The code of the parent line. This parameter only appears when the request parameter `Hierarchy` is `false`. |
|Type |Integer |Line type.<br><br><br>* 1: Default line<br><br>* 2: ISP line<br><br>* 3: Geolocation line<br><br>* 4: Cloud vendor line |
|PartName |String |Line hierarchy name. |
|Level |Integer |This parameter has no practical significance. You can ignore this parameter. |
|Children |Object Array |The sub\-lines contained in this line. This parameter only appears when the request parameter `Hierarchy` is `true`. |
|ID |String |The ID of the sub\-line. |
|Name |String |The name of the sub\-line. |
|Value |String |The code of the sub\-line. |
|FatherValue |String |The code of the parent line. |
|Type |Integer |Line type.<br><br><br>* 1: Default line<br><br>* 2: ISP line<br><br>* 3: Geolocation line<br><br>* 4: Cloud vendor line |
|PartName |String |Line hierarchy name. |
|Level |Integer |This parameter has no practical significance. You can ignore this parameter. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListLines&PageNumber=7&PageSize=1&Hierarchy=true
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230413201148F0DE3A41DD2EE858F888",
        "Action": "ListLines",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalCount": 564,
        "PageNumber": 1,
        "PageSize": 10,
        "Lines": [
            {
                "ID": "2432",
                "Name": "Asia_South Korea",
                "Value": "oversea",
                "Type": 3,
                "PartName": "South Korea",
                "Level": 1
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
