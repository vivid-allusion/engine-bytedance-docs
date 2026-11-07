---
title: "ListContinentCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinentCluster-en"
---

Gets the list of edge nodes for the canary environment or the full release environment.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListContinentCluster`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|Continents |String |No |Specify continents. Multiple continents can be specified, separated by commas. |
|Countries |String |No |Specify countries. Multiple countries can be specified, separated by commas. |
|ClusterType |Integer |No |Release environment type.<br><br><br>* 100: Canary environment.<br><br>* 200: Full release environment. |
|Page |Integer |No |Page number of the edge node list.<br><br>&nbsp;<br><br>If both Page and Limit parameters are not specified, all data will be returned; if only Limit is specified without Page, the first page of data will be returned; if only Page is specified without Limit, all data will be returned; if both Page and Limit are specified, data meeting the conditions will be returned. |
|Limit |Integer |No |Number of records per page. Currently, a maximum of 50 records can be retrieved per page.<br><br>&nbsp;<br><br>If both Page and Limit parameters are not specified, all data will be returned; if only Limit is specified without Page, the first page of data will be returned; if only Page is specified without Limit, all data will be returned; if both Page and Limit are specified, data meeting the conditions will be returned. |
|OrderBy |Integer |No |Sorting method for edge nodes.<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|ContinentCluster |Object[] |List of edge nodes. | |
|Country |String |Country or region where the edge node is located. |`Singapore` |
|Continent |String |Continent where the edge node is located. |`Asia` |
|ClusterType |Integer |Edge node type.<br><br><br>* 100: Canary release edge node<br><br>* 200: Full release edge node |`100` |
|Traffic |String |Version number of the function deployed on this edge node. |`[{"version_tag":"1.0.1"}]` |
|TotalCount |Long |Total number of edge nodes matching the query conditions. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
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
