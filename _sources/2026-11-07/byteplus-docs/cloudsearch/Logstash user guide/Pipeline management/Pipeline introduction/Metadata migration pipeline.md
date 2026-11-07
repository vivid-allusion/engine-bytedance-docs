---
title: "Metadata migration pipeline"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Metadata_migration_pipelines"
---

Migrating data between Elasticsearch/OpenSearch instances requires migrating all index metadata, including indexes and index templates. The metadata migration pipeline in Cloud Search Logstash migrates metadata. This article introduces the metadata migration pipeline.

<span id="9wPFk16j"></span>
## Applicable scenarios

Supports migrating metadata from Elasticsearch/OpenSearch instances to other Elasticsearch/OpenSearch instances. The migration includes the configuration for indexes (`index`) and index templates (`_index_template` and `_template`), excluding`.`system indexes that start with a period.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Index templates with a lifecycle policy configuration cannot be migrated and cannot be included in <code>include_template_list</code>.</div>


<span id="ybGSfMLf"></span>
## Metadata migration pipeline template

When creating a metadata migration pipeline, you can reference the MetaMigrate\-meta_migrate template. For detailed instructions, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline). The fields in the MetaMigrate\-meta_migrate template are described as follows.

```Python
{
  "input": {   # Source instance information.
    "hosts": "http://**a**.ivolces.com:9200",   # Address, required. The port in the address is required. If no port is specified, enter 9200.
    "user": "elastic",   # Authentication username, required.
    "password": "*****"   # Authentication password. Required.
  },
  "output": {  # Target instance information.
    "hosts": "http://**b**.ivolces.com:9200",  # Address. Required.
    "user": "admin",  # Authentication username. Required.
    "password": "*****"   # Authentication password. Required.
  },
  "index": {  # Index configuration.
    "include_list": [  # The list of indexes to migrate. Use "*" to migrate all.
      "*"
    ],
    "exclude_list": [],  # The list of indexes to exclude. It has a higher priority than include_list.
    "settings": null  # Adds configuration to each index during migration. Supports all native Elasticsearch/OpenSearch configurations in JSON format.
  },
  "index_type": {  # For versions earlier than ES 6 where each index has multiple types.
    "include_list": [  # A list of index types to migrate. "*" indicates all types.
      "*"
    ],
    "auto_split": false,  # Specifies whether to automatically split different types into separate destination indexes when the source index has multiple types to migrate.
    "split_index_name_pattern": "%s-index_type-%s",  # The destination index name pattern when a source index with multiple types is split into different destination indexes.
    "rename": "_doc"  # Forcibly specifies the index type when the destination cluster is ES 6, which defaults to _doc. Set to null if you do not need to rename the index type.
  },
  "include_template_list": [  # A list of index templates to migrate. "*" indicates all. Set to [] if you do not need to migrate templates.
    "*"
  ]
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After saving and deploying the metadata migration pipeline, you can view the metadata migration status in the Logs when the Logstash instance status changes to <strong>Running</strong>. If the Logs contain <code>[root]USD数据迁移完成(metadata migrate finished)</code> and no logs at the ERROR level, the metadata migration is complete. For detailed instructions, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/Query_logs">Query Logs</a>.</div>


<span id="ybGSfMLf"></span>
## Migrate metadata and configure Logstash


<Tabs>
<Tab zoneid="UYSUMZcTHE" title="ES 6 -> ES 6&7 ， ES 7 -> ES 7">
<TabTitle>ES 6 -> ES 6&7 ， ES 7 -> ES 7</TabTitle>

In ES 6, a single index mapping has only one `_type`. In ES 7 and later versions, mappings do not support setting `_type`. Therefore, indices can be migrated one\-to\-one. No other fields need to be modified except `input` and `output`.


</Tab>
<Tab zoneid="qzf1DqAOGw" title="ES 2&5 -> ES 6&7">
<TabTitle>ES 2&5 -> ES 6&7</TabTitle>

In ES 2 and ES 5 versions, a single index can have multiple `_type`s, and there are three migration methods:


* Migrate data of a specified `_type` from the source index.

   * Migrate a source index with only one `_type` to the same destination index.

   * The source index has multiple `_type`s; only documents of the specified `_type` are migrated to the same target index, and the rest are discarded.

* Migrate all `_type` data from the source index to the same target index.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When migrating multiple or all <code>_type</code>s from the source index to the same target index, inconsistent mappings or data meanings for different <code>_type</code>s will lead to dirty data.   </div>
   

* Migrate all `_type` data from the source index to different target indexes, where the target index names follow a conventional style.


<span id="pdlEf384"></span>
### Migrate the source index to the same target index.

If the index has only a single `_type`, migrate it directly. If an index has multiple `_type`s, to migrate only the metadata where the `_type` is `t_1` and rename the `_type` in all target indexes to `_doc`, modify the following field in the template to `t_1` and fill in other fields as needed.

```Python
{
  "index_type": {
    "include_list": [
      "t_1"
    ],
  },
}
```


When migrating data with a standard Logstash pipeline, add the following configuration to discard data from other `_type`s.

```Python
filter {
  if [@metadata][_type] != "t_1" {
    drop {}
  }
}
```


<span id="adueNAYu"></span>
### Migrate different `_type`s from the source index to different target indexes.

If the index has only a single `_type `, migrate it directly without changing the target index name. If an index has multiple index `_type`s, the destination index name is partitioned based on `{source index name}-index_type-{source index type}`, and all destination index `_type`s are renamed to `_doc`.

```Python
{
  "index_type": {
    "auto_split": true,
    "split_index_name_pattern": "%s-index_type-%s",
    "rename": "_doc"
  }
}
```


When migrating data with a standard Logstash pipeline, the `index` configuration in the `output` plugin is as follows.

```Python
output {
  elasticsearch {
    index => "%{[@metadata][_index]}-index_type-%{[@metadata][_type]}"
  }
}
```



</Tab>
<Tab zoneid="TNvn6AWtHJ" title="ES 7&8 -> OpenSearch">
<TabTitle>ES 7&8 -> OpenSearch</TabTitle>

ES 7 and ES 8 do not support setting `_type`, so indices can be migrated one\-to\-one. No other fields need to be modified except `input` and `output`.


</Tab>
<Tab zoneid="z5DipXIGBh" title="OpenSearch -> OpenSearch">
<TabTitle>OpenSearch -> OpenSearch</TabTitle>

OpenSearch does not support `_type` settings, so indices are migrated on a one\-to\-one basis. Except for `input` and `output`, no other fields need to be modified.


</Tab>
</Tabs>


&nbsp;

&nbsp;

&nbsp;
