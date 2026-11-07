---
title: "Differences Between Plugins in Elasticsearch and OpenSearch"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Differences_Between_Plugins_in_Elasticsearch_and_OpenSearch"
---

This article introduces the differences between output plugins in Elasticsearch and OpenSearch.

<span id="tSLT8cZh"></span>
## Plugin Source and Installation Methods


|Plugin |Provider |Installation method |See documentation |
|---|---|---|---|
|Elasticsearch plugin |Maintained and supported by Elasticsearch official. |Provided with Elasticsearch Logstash, no manual installation required. |[Logstash Plugins](https://www.elastic.co/docs/reference/logstash/plugins) |
|OpenSearch plugin |Maintained and supported officially by OpenSearch. |Pre\-installed by default in Logstash 8.17.0 versions of Cloud Search service without additional configuration. |* [Logstash Input OpenSearch](https://github.com/opensearch-project/logstash-input-opensearch)<br><br>* [Logstash Output OpenSearch](https://github.com/opensearch-project/logstash-output-opensearch) |


<span id="th4QQEQ3"></span>
## Compatibility

  The compatibility matrix for Logstash plugins of Elasticsearch and OpenSearch is shown in the following table. For more actions, see [OpenSearch official documentation](https://docs.opensearch.org/latest/tools/#compatibility-matrix-for-logstash).


|Instance type |Plugin type |Elasticsearch 5.6 |Elasticsearch 6.8~7.17 |Elasticsearch 8.17 |OpenSearch 2.9~3.3 |
|---|---|---|---|---|---|
|Elasticsearch |Input |<div style="text-align: center"><br>Compatible</div><br> ||||
||Output |<div style="text-align: center"><br>compatible</div><br> ||||
|OpenSearch |Input |incompatible |Compatible |Incompatible |compatible |
||Output |<div style="text-align: center"><br>compatible</div><br> ||||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">OpenSearch input plugin reports error <code>OpenSearch::UnsupportedProductError</code> when incompatible.</div>


<span id="UigYySGB"></span>
## Support for ECS specification

Logstash 8.x introduces the ECS (Elastic Common Schema) specification.


* **Main purpose**: unify naming rules for output fields across plugins to avoid difficulties in data analytics and visualization caused by inconsistent naming.

* **Specification content**: standardizes commonly used fields; [see ECS field reference](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for details.


Upgrading to Logstash 8.x may cause incompatibility with some existing configurations or plugins due to ECS. To maintain consistency with earlier configurations, add the following parameters in plugin settings. For specific steps, see [ECS in Logstash](https://www.elastic.co/docs/reference/logstash/ecs-ls).

```JSON
ecs_compatibility => disabled
```


This configuration disables the ECS specification to ensure compatibility with earlier versions. The Elasticsearch plugin supports the ECS specification, while the OpenSearch plugin currently does not.

&nbsp;

&nbsp;
