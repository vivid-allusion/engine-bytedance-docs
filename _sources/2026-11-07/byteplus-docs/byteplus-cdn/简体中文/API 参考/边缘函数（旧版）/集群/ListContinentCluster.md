---
title: "ListContinentCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListContinentCluster"
---

该接口用于获取函数所部署的集群列表。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListContinentCluster`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数id |
|Continents |String |否 |指定大洲。可以指定多个大洲，用逗号分隔。 |
|Countries |String |否 |指定国家。可以指定多个国家，用逗号分隔。 |
|ClusterType |Integer |否 |集群类型。<br><br><br>* 100：灰度发布集群<br><br>* 200：全量发布集群 |
|Page |Integer |否 |集群列表的页码。<br><br>&nbsp;<br><br>如果 Page 和 Limit 参数都不指定，将返回全量数据；如果仅指定 Limit，不指定 Page ，将返回第 1 页数据；如果仅指定 Page，不指定 Limit，将返回全量数据；如果 Page 和 Limit 都指定，将返回符合条件的数据。 |
|Limit |Integer |否 |每页记录数。目前，每页最多可获取50条记录。<br><br>&nbsp;<br><br>如果 Page 和 Limit 参数都不指定，将返回全量数据；如果仅指定 Limit，不指定 Page ，将返回第 1 页数据；如果仅指定 Page，不指定 Limit，将返回全量数据；如果 Page 和 Limit 都指定，将返回符合条件的数据。 |
|OrderBy |Integer |否 |查询出来的集群的排序方式。<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ContinentCluster |Object[] |集群列表 |`See the explanation below` |
|Country |String |集群所在的国家。 |`Singapore` |
|Continent |String |集群所在的大洲。 |`Asia` |
|ClusterType |Integer |集群类型。<br><br><br>* 100：灰度发布集群<br><br>* 200：全量发布集群 |`100` |
|Traffic |String |部署在该集群上函数的版本号。 |`[{"version_tag":"1.0.1"}]` |
|TotalCount |Long |符合查询条件的集群总数。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
```


<span id="返回示例"></span>
### 返回示例

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


&nbsp;
