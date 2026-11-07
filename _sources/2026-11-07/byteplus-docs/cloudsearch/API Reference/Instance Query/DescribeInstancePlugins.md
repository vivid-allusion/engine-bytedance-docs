---
title: "DescribeInstancePlugins"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstancePlugins"
---

Call DescribeInstancePlugins to query the plugins that are installed on a specified instance.

<span id="cb459146"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=DescribeInstancePlugins&Version=2023\-01\-01 HTTP/1.1


<span id="fe4bfe37"></span>
## Request parameters

<span id="83e0dfc3"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DescribeInstancePlugins` |The action that you want to perform. Value: `DescribeInstancePlugins`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="670ab184"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*718 |The ID of the instance for which you want to query the installed plugins. |


<span id="5280d2a7"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstancePlugins |Array of [ESPluginDTO](https://docs.byteplus.com/docs/cloudsearch/DescribeInstancePlugins#3b42cb7b) | |Details of the plugins installed on the instance. |


<span id="3b42cb7b"></span>
### ESPluginDTO


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|PluginName |String |analysis\-dynamic\-synonym |The plugin name. |
|Version |String |7.10.2.1 |The plugin version. |
|Description |String |Analysis\-plugin for synonym. |The description of the plugin. |
|Status |String |PreInstalled |The status of the plugin.<br><br>Valid values: PreInstalled, Installed, Uninstalled, Installing, Uninstalling |


<span id="c75d929e"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=DescribeInstancePlugins&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***718"
}
```


<span id="af39e16c"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202310231700***7AFA8399E80",
        "Action": "DescribeInstancePlugins",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstancePlugins": [
            {
                "PluginName": "analysis-dynamic-synonym",
                "Version": "7.10.2.1",
                "Description": "Analysis-plugin for synonym",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-icu",
                "Version": "7.10.2",
                "Description": "The ICU Analysis plugin integrates the Lucene ICU module into Elasticsearch, adding ICU-related analysis components.",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-ik",
                "Version": "7.10.2.1",
                "Description": "IK Analyzer for Elasticsearch",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-kuromoji",
                "Version": "7.10.2",
                "Description": "The Japanese (kuromoji) Analysis plugin integrates Lucene kuromoji analysis module into elasticsearch.",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-phonetic",
                "Version": "7.10.2",
                "Description": "The Phonetic Analysis plugin integrates phonetic token filter analysis with elasticsearch.",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-pinyin",
                "Version": "7.10.2",
                "Description": "Pinyin Analysis for Elasticsearch",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-smartcn",
                "Version": "7.10.2",
                "Description": "Smart Chinese Analysis plugin integrates Lucene Smart Chinese analysis module into elasticsearch.",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "analysis-stconvert",
                "Version": "7.10.2",
                "Description": "STConvert is a analysis plugin that convert Chinese characters between traditional and simplified.",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "byte-codec",
                "Version": "1.0.0",
                "Description": "The plugin supporting additional codec for Elasticsearch",
                "Status": "Uninstalled"
            },
            {
                "PluginName": "byte-throttler",
                "Version": "1.0.0",
                "Description": "The index-level rate limiter to throttle qps and throughput of search/bulk actions.",
                "Status": "Uninstalled"
            },
            {
                "PluginName": "opendistro-alerting",
                "Version": "1.13.1.0",
                "Description": "Amazon OpenDistro alerting plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-anomaly-detection",
                "Version": "1.13.0.0",
                "Description": "Amazon opendistro elasticsearch anomaly detector plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-asynchronous-search",
                "Version": "1.13.0.1",
                "Description": "Provides support for asynchronous search",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-index-management",
                "Version": "1.13.2.0",
                "Description": "Open Distro Index Management Plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-job-scheduler",
                "Version": "1.13.0.0",
                "Description": "Open Distro for Elasticsearch job schduler plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-knn",
                "Version": "1.13.0.0",
                "Description": "Open Distro for Elasticsearch KNN",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-performance-analyzer",
                "Version": "1.13.0.0",
                "Description": "Performance Analyzer Plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-reports-scheduler",
                "Version": "1.13.0.0",
                "Description": "Scheduler for ODFE Kibana Reports Plugin",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro-sql",
                "Version": "1.13.2.0",
                "Description": "Open Distro for Elasticsearch SQL",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "opendistro_security",
                "Version": "1.13.1.0",
                "Description": "Provide access control related features for Elasticsearch 7",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "prometheus-exporter",
                "Version": "7.10.2.0",
                "Description": "Export Elasticsearch metrics to Prometheus",
                "Status": "PreInstalled"
            },
            {
                "PluginName": "repository-s3",
                "Version": "7.10.2",
                "Description": "The S3 repository plugin adds S3 repositories",
                "Status": "PreInstalled"
            }
        ]
    }
}
```
