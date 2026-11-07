---
title: "Use Logstash to migrate data across clusters"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/migrating-data-across-Logstash"
---

Logstash is an open\-source data collection engine with real\-time pipeline processing capabilities. It can simultaneously collect data from multiple sources, transform it, and then send it to Elasticsearch. This article explains how to migrate data across clusters using Logstash.

## Prerequisites

A Logstash instance has been created and is in the **Running** state. For the procedure, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

## Notice

Before data migration, ensure network connectivity between the source cluster, the Logstash service, and the destination cluster. For the procedure, refer to [Use SNAT to configure public network access](https://docs.byteplus.com/en/docs/cloudsearch/Use_DNAT_to_configure_Logstash_access_from_the_public_network).

## Operation steps

1. Create and deploy a metadata migration pipeline. For specific operations and parameter configuration, refer to [Metadata migration pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Metadata_migration_pipelines).

2. Create and deploy a regular pipeline. For specific steps, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline). The following is a sample pipeline configuration.

   ```Bash
   input {
     opensearch {
      # Source cluster endpoint
       hosts => "源集群链接"
       # Source cluster basicAuth authentication information (if any)
       user => "源集群用户名"
       password => "源集群密码"
       # Wildcards are supported. "*" indicates all indexes. If there are many indexes with a large volume of data, you can configure them separately.
       # "*,-.*" indicates all indexes not starting with ".". Indexes starting with "." are typically system indexes and do not need to be synchronized.
       index => "源索引名"
       query => '{ "sort": [ "_doc" ] }'
       size => 1000
       # Scroll session retention time
       scroll => "5m"
       docinfo => true
       # Assign docinfo to @metadata
       docinfo_target => "@metadata"
       # Whether to use only the HTTP links in the hosts configuration array for requests
       # If an HTTP cluster does not have a certificate, skip certificate verification by configuring ssl=>true without configuring ca_file.
       ssl => false
       # Supported since ES6. To accelerate scroll, the value should not exceed the number of source index shards.
       slices => 1
     }
   }
   
   # Optional: Delete fields automatically added by Logstash.
   #filter {
   #    mutate {
   #       remove_field => ["@version", "@timestamp"]
   #   }
   #}
   
   output {
     opensearch {
      # Target cluster endpoint
       hosts => "目标集群链接"
       # BasicAuth authentication information for the target cluster (if any)
       user => "目标集群用户名"
       password => "目标集群密码"
       # Keep this consistent with the source index name
       index => "%{[@metadata][_index]}"
       document_id => "%{[@metadata][_id]}"
       # Whether to use only the HTTP links in the hosts configuration array for requests
       ssl => false
       # Whether to verify the ES server certificate when using an HTTP link
       ssl_certificate_verification => false
       # When ssl_certificate_verification is true, this is the path to the server CA certificate (.cer or .pem format) for verification
       # cacert => "CA certificate path"
     }
   }
   ```

   > **tip**

   * > For specific configuration, refer to the official Elasticsearch documentation. [Input plugins](https://www.elastic.co/guide/en/logstash/7.10/input-plugins.html) and [Output plugins](https://www.elastic.co/guide/en/logstash/7.10/output-plugins.html).

   * > If data in the source cluster includes a `routing` parameter, also configure the `routing` field in the output plugin.

   * > For the differences in the output plugin between Elasticsearch and OpenSearch, refer to [Differences in the output plugin between Elasticsearch and OpenSearch](https://docs.byteplus.com/en/docs/cloudsearch/Differences_Between_Plugins_in_Elasticsearch_and_OpenSearch).

3. View the pipeline health. For the procedure, refer to [Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs) and [Use the debugging feature](https://docs.byteplus.com/en/docs/cloudsearch/Use_the_debugging_feature).

4. View the migration progress.

   Execute the following command to query information about all indices in the cluster, including their health, state, name, UUID, shards, replicas, and number of documents.

   ```Shell
   GET /_cat/indices?v
   ```

   Determine the migration progress by comparing the number of indices and documents in the source and destination clusters. Data migration is complete when the clusters have the same number of indices and a nearly identical number of documents.

   > **tip**

   * > The migration task does not migrate subsequent incremental data; the number of documents in existing indices will be nearly the same.

   * > Since ES 2 and ES 5 support multiple `_type`s in a single index, you need to view the migration progress by `_type` if the migration specified a `_type` for the source index or split different `_type`s into different destination indices. In the source cluster, use `/{index_name}/{_type}/_count` to view the number of documents for a specific index and `_type`.

5. (Optional) Migrate incremental data.

   > **tip**

   > If the source index requires incremental updates, note the following precautions:

   * > The documentation includes a time field that marks the last update time.

   * > Before migration, record the start time, which will be used as the start time for incremental migration.

   * > The incremental data migration must start after the full data migration is complete.

   Create and deploy a general pipeline. For the procedure, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline). The following is an example of the pipeline input plugin configuration.

   ```Bash
   input {
     elasticsearch {
       # Source ES cluster endpoint
       hosts => "源集群链接"
       # BasicAuth authentication information for the source cluster (if any)
       user => "源集群用户名"
       password => "源集群密码"
       # Wildcards are supported. "*" represents all indexes. If there are many indexes or a large amount of data, you can configure them separately.
       # "*,-.*" represents all indexes that do not start with ".". Indexes that start with "." are usually system indexes and do not need to be synchronized.
       index => "源索引名"
       # Query incremental data by time range. The following configuration queries data from the last 10 minutes.
       # The following @timestamp is the field for distinguishing new from old data. It can be flexibly adjusted according to the actual index fields during migration. The same applies to the query statement.
       query => '{"query":{"range":{"@timestamp":{"gte":"now-10m","lte":"now/m"}}}}'
       size => 1000
       # Specifies whether to use slice scroll to accelerate migration. The value cannot exceed the number of shards for a single index. This configuration is only supported in ES Version 6 and later.
       # slices => 4
       # Scroll session keep-alive time
       scroll => "5m"
       docinfo => true
       ssl => false
     }
   }
   ```
