---
title: "Manage time-series data using Data Streams and ISM"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Manage_time-series_data_using_Data_Streams_and_ISM"
---

This topic uses log data as an example to show how to easily manage time\-series data with OpenSearch's Data Streams and ISM features.

<span id="684b1efc"></span>
## Background

In time\-series data scenarios (e.g., log data), to prevent unlimited growth in a single index’s size, a common method is to store data daily, switch to a new write index every day using Rollover, and ensure old indexes are searchable through aliases. This data management process involves many steps, including creating index aliases, creating Rollover data management policies, creating initial indexes, and setting write indexes, making the operation process complex.

Data Streams is a feature designed for time\-series data management scenarios that greatly simplifies the configuration steps for data management. This article uses Nginx log data simulated by the [nginx-log-generator](https://github.com/kscarlett/nginx-log-generator) tool to illustrate how to simplify data management by combining OpenSearch’s Data Streams and ISM features.

<span id="5bef3e49"></span>
## Precautions


* The time\-series data management method introduced here currently applies only to OpenSearch and Elasticsearch 7.10.2 instances. This topic uses an OpenSearch instance as an example.

* Index templates and ISM policies only automatically associate and take effect for data streams that have not yet been created. Converting an existing index into a Data Stream is also not supported. Therefore, please create index templates and ISM policies before starting log data writing.


<span id="b182eaf3"></span>
## Step one: create an index template


1. Access Dashboards through the public network. For specific steps, see [Public access to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool#3cbdb7b4).

2. In the left menu, select **Management \> Dev Tools** to open the developer tools page.

3. Create an index template.

   Create an index template named `nginx-logs-template`. If the index name written by the user starts with `nginx-logs-`, the system will automatically create it as a data stream and create the corresponding backing index.

   ```HTTP
   PUT _index_template/nginx-logs-template
   {
       "index_patterns": [
            "nginx-logs-*"
       ],
       "data_stream": {},
       "priority": 100
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The data stream requires the indexed documents to have the <code>@timestamp</code> field by default. To use a different field name, explicitly specify it when creating the index template.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```HTTP
   PUT /_index_template/nginx-logs-template
   {
       "index_patterns": [
           "nginx-logs-*"
       ],
       "data_stream": {
           "timestamp_field": {"name": "request_time"}
        },
       "priority": 100
   }
   ```
      </div>
   

<span id="a6889d8c"></span>
## Step two: create an ISM policy


1. On the instance Dashboards page, go to **Management \> Dev Tools** in the developer tools page.

2. Create an automatic rollover strategy and link it to the index template.

   Create an ISM policy with the id `rollover_nginx_logs` that automatically rolls over indexes created one day ago and creates a new backing index.

   
   <Tabs>
   <Tab zoneid="lBhN7qJTNv" title="OpenSearch instance">
   <TabTitle>OpenSearch instance</TabTitle>
   
   ```HTTP
   PUT _plugins/_ism/policies/rollover_nginx_logs
   {
       "policy": {
           "description": "Rollover policy for nginx logs data stream",
           "default_state": "rollover",
           "states": [
               {
                   "name": "rollover",
                   "actions": [
                       {
                           "rollover": {
                                "min_index_age": "1d"
                           }
                       }
                   ],
                   "transitions": []
               }
           ],
           "ism_template": {
               "index_patterns": [
                     "nginx-logs-*"
               ],
               "priority": 100
           }
       }
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="irORtwJTYL" title="Elasticsearch 7.10.2 instance">
   <TabTitle>Elasticsearch 7.10.2 instance</TabTitle>
   
   ```HTTP
   PUT _opendistro/_ism/policies/rollover_nginx_logs
   {
       "policy": {
           "description": "Rollover policy for nginx logs data stream",
           "default_state": "rollover",
           "states": [
               {
                   "name": "rollover",
                   "actions": [
                       {
                           "rollover": {
                                "min_index_age": "1d"
                           }
                       }
                   ],
                   "transitions": []
               }
           ],
           "ism_template": {
               "index_patterns": [
                     "nginx-logs-*"
               ],
               "priority": 100
           }
       }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   


<span id="0c1c9337"></span>
## Step three: write data

You need to **complete creating the index template and ISM policy** before you can start writing data. If the written index name matches the `nginx-logs-*` pattern, the system automatically creates the corresponding data stream and write index.

This article chooses to write Nginx logs to the OpenSearch instance via Logstash's [OpenSearch output plugin](https://opensearch.org/docs/latest/tools/logstash/index/). The Logstash collection pipeline configuration is as follows:

```HTTP
input {
    file {
        path => "/tmp/nginx.log"
        type => "nginx"
        start_position => "beginning"
    }
}

filter {
    grok {
        match => { "message" => ['%{IPORHOST:remote_addr} - - \[%{HTTPDATE:timestamp}\] \"(?:%{WORD:verb} %{NOTSPACE:request}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:rawrequest})\" %{NUMBER:response} (?:%{NUMBER:bytes}|-) \"%{DATA:referrer}\" \"%{DATA:agent}\"'] }
  }
}

output {
    opensearch {
        # 目标OpenSearch实例的访问地址。
        hosts => ["https://localhost:9200"]
        # 索引名称。
        index => "nginx-logs-devbox"
        action => "create"
        # 目标OpenSearch实例的鉴权信息。
        user => "XXXX"
        password => "XXXXX"
        # 是否仅用hosts配置项数组中的https地址进行请求。
        ssl => true
        # 当使用https连接实例时，是否验证实例的服务端证书。
        ssl_certificate_verification => false
    }
}
```


<span id="b92b5dbc"></span>
## View ISM policy execution records

ISM saves execution records in the index `.opendistro-ism-managed-index-history*`. You can query the ISM policy execution history in Dashboards like querying regular index data visualizations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f729137fdfe44589a9b35bae656a3d5~tplv-goo7wpa0wc-image.image) </span>

<span id="e215f71f"></span>
## FAQs

If you encounter exceptions or have questions while using the ISM strategy, refer to the open source documentation [ISM error prevention resolutions](https://opensearch.org/docs/latest/im-plugin/ism/error-prevention/resolutions/).

If your issue remains unresolved, you can also [submit a ticket](https://console.byteplus.com/workorder/create/?step=1) for assistance.
