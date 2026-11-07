---
title: "UpdateCountryCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateCountryCluster"
---

This interface is used to modify the type of cluster for canary release or full release.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=UpdateCountryCluster&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>UpdateCountryCluster<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function for which you want to update the cluster type. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>ClusterType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The type of cluster.<br><br>  <br><br> <br> <br><br>* 100: canary cluster<br><br><br> <br> <br><br>* 200: production cluster<br><br><br>  <br><br>  |  <br><br>100<br><br>  |
|  <br><br>Countries<br><br>  |  <br><br>[]Country<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The array of countries where the cluster is located.<br><br>  |  <br><br>["Singapore"]<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=UpdateCountryCluster&Version=2021-03-01
{
    "ClusterType": 200,
    "Countries": [
        "Singapore"
    ],
    "FunctionId": "3gyz993****",
}
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "UpdateCountryCluster",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
