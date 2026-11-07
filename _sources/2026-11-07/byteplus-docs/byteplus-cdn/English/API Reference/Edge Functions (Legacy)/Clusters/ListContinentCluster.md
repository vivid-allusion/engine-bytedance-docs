---
title: "ListContinentCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListContinentCluster"
---

This API is used to get the list of clusters where the function is deployed.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListContinentCluster&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListContinentCluster<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The function ID<br><br>  |  <br><br>23455331245<br><br>  |
|  <br><br>Continents<br><br>  |  <br><br>[]Continent<br><br>  |  <br><br>No<br><br>  |  <br><br>Specify the continent. Multiple continents can be specified, separated by commas.<br><br>  |  <br><br>["Asia"]<br><br>  |
|  <br><br>Countries<br><br>  |  <br><br>[]Country<br><br>  |  <br><br>No<br><br>  |  <br><br>Specify the country. Multiple countries can be specified, separated by commas.<br><br>  |  <br><br>["Singapore"]<br><br>  |
|  <br><br>ClusterType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The type of cluster.<br><br>  <br><br> <br> <br><br>* 100: canary cluster<br><br><br> <br> <br><br>* 200: production cluster<br><br><br>  <br><br>  |  <br><br>100<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The number of entries per page<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Data order.<br><br>  <br><br> <br> <br><br>* 1 for descending<br><br><br> <br> <br><br>* 2 for ascending<br><br><br>  <br><br>  <br><br>Default is arranged in ascending order according to id.<br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>ContinentCluster<br><br>  |  <br><br>[]ContinentCluster<br><br>  |  <br><br>List of continent cluster.<br><br>  |  <br><br>See the explanation below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>The total number of clusters matching the filter criteria.<br><br>  |  <br><br>1<br><br>  |

#### ContinentCluster

|  <br><br>Name<br><br>  |  <br><br>Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example Value<br><br>  |
|---|---|---|---|
|  <br><br>Country<br><br>  |  <br><br>String<br><br>  |  <br><br>The country where the cluster is located.<br><br>  |  <br><br>Singapore<br><br>  |
|  <br><br>Continent<br><br>  |  <br><br>String<br><br>  |  <br><br>The continent where the cluster is located.<br><br>  |  <br><br>Asia<br><br>  |
|  <br><br>ClusterType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>The type of cluster.<br><br>  <br><br> <br> <br><br>* 100: canary cluster<br><br><br> <br> <br><br>* 200: production cluster<br><br><br>  <br><br>  |  <br><br>100<br><br>  |
|Traffics |String |The versions of the function deployed on this cluster. |[{"version_tag":"1.0.1"}] |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListContinentCluster&Version=2021-03-01
&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240423082346DA1BD20A355B07D425CA",
        "Action": "ListContinentCluster",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ContinentCluster": [
            {
                "Continent": "Europe",
                "Country": "France",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Turkey",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Philippines",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Japan",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Malaysia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Saudi Arabia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "South America",
                "Country": "Brazil",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "South Korea",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Europe",
                "Country": "Russia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Thailand",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Indonesia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "North America",
                "Country": "United States",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Singapore",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Vietnam",
                "ClusterType": 100,
                "Traffics": "[{\"version_tag\":\"1.0.1\"}]"
            },
            {
                "Continent": "Europe",
                "Country": "Germany",
                "ClusterType": 100,
                "Traffics": ""
            }
        ],
        "TotalCount": 15
    }
}
```
