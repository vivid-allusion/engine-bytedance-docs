---
title: "ListVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListVersions"
---

This interface is used to retrieve all code versions that have been published for a function based on the function id.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListVersions&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListVersions<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to view the list of all code versions. You can get the FunctionId by calling the interface[ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow)<br><br> .<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number.<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Revisions<br><br>  |  <br><br>[]Revision<br><br>  |  <br><br>List of code versions<br><br>  |  <br><br>See below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of code versions<br><br>  |  <br><br>1<br><br>  |

### Revision Object

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Id<br><br>  |  <br><br>Int64<br><br>  |  <br><br>ID<br><br>  |  <br><br>1<br><br>  |
|  <br><br>VersionTag<br><br>  |  <br><br>String<br><br>  |  <br><br>The version number of this version.<br><br>  |  <br><br>1.0.1<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>The description of this version.<br><br>  |  <br><br>this is a sparrow<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>String<br><br>  |  <br><br>Creator<br><br>  |  <br><br>zhangsan<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListVersions&Version=2021-03-01
&FunctionId=3gyz993****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022011310282201022524312506*******",
        "Action": "ListVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Revisions": [
            {
                "Id": 133,
                "VersionTag": "1.0.1",
                "Description": "test publish",
                "Creator": "*****"
            }
        ],
        "TotalCount": 1
    }
}
```
