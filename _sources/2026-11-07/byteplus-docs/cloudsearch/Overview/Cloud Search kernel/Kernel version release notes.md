---
title: "Kernel version release notes"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Kernel_version_release_notes"
---

Cloud search service delivers full\-featured compatibility with both Elasticsearch and OpenSearch kernels, making the kernel more stable, secure, cost\-effective, and easier to monitor based on proven customer best practices. This topic describes the features and version updates of the cloud search service across different kernel versions.

<span id="93ba9c6d"></span>
## OpenSearch


<Tabs>
<Tab zoneid="TFbsj8hh2V" title="Version 3.3.0">
<TabTitle>Version 3.3.0</TabTitle>


|**version number** |**Release date** |**Type** |**Description** |
|---|---|---|---|
|3.3.0\-26.8.1 |2026\-08\-04 |New features |The Security plugin supports dynamic configuration of `bcrypt.rounds`. |
|||Feature optimization |None |
|||Bug fixes |None. |
|3.3.0\-26.8.0 |2026\-07\-29 |New features |Added support for DiskANN and RaBitQ capabilities. |
|||Feature optimization |None. |
|||Bug fixes |None. |
|3.3.0\-26.3.2 |2026\-03\-27 |New features |Add built\-in plugins related to OpenSearch version 3.3. |
|||Function optimization |None. |
|||Bug fixes |None. |
|3.3.0\-25.12.2 |2026\-01\-06 |New features |* Support ISM snapshots can be searched.<br><br>* Support jieba tokenization plugin.<br><br>* Update other plugins in the plugin list. |
|||function optimization |None. |
|||Bug fixes |None. |
|3.3.0\-25.12.1 |2025\-12\-23 |New features |Add OpenSearch version 3.3.0. |
|||Function optimization |None. |
|||Bug fixes |None. |



</Tab>
<Tab zoneid="zrryKfFX0T" title="Version 2.9.0">
<TabTitle>Version 2.9.0</TabTitle>


|**version number** |**Release date** |**Type** |**Description** |
|---|---|---|---|
|2.9.0\-26.7.1 |2026\-07\-07 |New features |* KNN supports radial search.<br><br>* KNN supports using RaBitQ to build indices.<br><br>* Limits the size of `BitSetFilterCache` to 5% of the JVM heap by default. |
|||Feature optimization |None. |
|||Bug fixes |None. |
|2.9.0\-26.5.0 |2026\-05\-14 |New features |None. |
|||Function optimization |Optimize some query indicators |
|||Bug fixes |None. |
|2.9.0\-26.4.0 |2026\-05\-14 |New features |None. |
|||Function optimization |Optimize some query indicators. |
|||Bug fixes |None. |
|2.9.0\-26.3.1 |2026\-03\-18 |New features |* Support LDAP configuration.<br><br>* ISM plugin supports lifecycle management of vector data. |
|||Function optimization |None. |
|||Bug fixes |None. |
|2.9.0\-25.10.0 |2026\-01\-06 |New features |* Added some kernel capabilities, such as **long_term** and **fsync io** metric collection and retrieval.<br><br>* k\-NN plugin restricts engine select type. |
|||Function optimization |None. |
|||Bug fixes |None. |
|2.9.0\-25.9.3 |2025\-11\-17 |New features |None. |
|||Function optimization |None. |
|||Bug fixes |Fix issues related to Synonym Hot Module Replacement and signatures. |
|2.9.0\-25.8.4<br><br>&nbsp;<br><br> |2025\-09\-18<br><br> |New features |Supports dynamic modification of Leader Check and Follower Check heartbeat parameters. |
|||Function optimization |None. |
|||Bug fixes |Fixed error issues in the Embedding Pipeline under certain scenarios. |
|2.9.0\-25.8.3<br><br>&nbsp;<br><br> |2025\-08\-20<br><br> |New features |* Added support for using BloomFilter on the `_id` field.<br><br>* Added support to modify store or restore speed during snapshot recovery.<br><br>* Added support for using the Notification plugin in Dashboards. |
|||Feature Optimization |Optimize KNN plugin performance |
|||Bug fixes |Fix some issues and defects. |
|2.9.0\-25.8.2 |2025\-07\-16 |New features |The DiskANN + RaBitQ feature is officially released. For more details, see [DiskANN + RaBitQ engine usage](https://docs.byteplus.com/en/docs/6465/1553583#0a201eda). |
|||Feature Optimization |Optimized the merge rate of KNN Binary DocValues. |
|||Bug fixes |* Fix snapshot vulnerabilities<br><br>* Fix issues in the jieba participle plugin |
|2.9.0\-25.8.1 |2025\-05\-19 |New features |None. |
|||Function optimization |Optimize the real\-time update mechanism of the synonym plugin. |
|||Bug fixes |None. |
|2.9.0\-25.8.0 |2025\-04\-16 |New features |* Add drived source.<br><br>* Add support for time\-based field query index pruning.<br><br>* Add support for paginated retrieval of snapshot shard information.<br><br>* Add support for dynamically configuring index.check_pending_flush.enabled.<br><br>* Add support for the jieba tokenization plugin. |
|||Function optimization |* Optimize lucene\-level memory locks to enhance write performance.<br><br>* Optimize certain security plugin functions. |
|||Bug fixes |None. |



</Tab>
</Tabs>


<span id="tmtC5tog"></span>
## Elasticsearch


<Tabs>
<Tab zoneid="bDowiPRdwU" title="Version 7.10.2">
<TabTitle>Version 7.10.2</TabTitle>


|**Version number** |**Release date** |**Type** |**Description** |
|---|---|---|---|
|7.10.2\-26.7.1 |2026\-07\-07 |New features |* Supports concurrent Translog recovery to improve recovery efficiency.<br><br>* Limits the size of BitSetFilterCache to 5% of the JVM heap by default.<br><br>* Supports using the preference parameter to route queries to the primary or replica shards. |
|||Feature optimization |None. |
|||Bug fixes |None. |
|7.10.2\-26.4.1 |2026\-05\-11 |New features |Add ingest\-attachment plugin. |
|||Function optimization |None. |
|||Bug fixes |None. |
|7.10.2\-26.3.1 |2026\-03\-18 |New features |None. |
|||Function optimization |None. |
|||Bug fixes |Fixed some vulnerabilities. |
|7.10.2\-25.12.1 |2026\-01\-06 |New features |* Support parameter configuration for some kernels.<br><br>* Support bloom_filter. |
|||Function optimization |None. |
|||Bug fixes |None. |
|7.10.2\-25.8.5 |2025\-11\-17 |New features |None. |
|||Function optimization |None. |
|||Bug fixes |Fix issues related to Synonym Hot Module Replacement and signatures. |
|7.10.2\-25.8.4<br><br> |2025\-09\-18<br><br> |New features |* Support sorting of Long type data optimized through Lucene.<br><br>* Support dynamic adjustment of Leader Check and Follower Check heartbeat parameters. |
|||Function optimization |None. |
|||Bug fixes |None. |
|7.10.2\-25.8.3 |2025\-08\-20<br><br> |New features |Added support to modify store or restore speed during snapshot recovery. |
|||Feature Optimization |None. |
|||Bug fixes |None. |
|7.10.2\-25.8.2 |2025\-07\-16 |New features |None. |
|||Function optimization |None. |
|||Bug fixes |Fix snapshot vulnerabilities |
|7.10.2\-25.8.1 |2025\-05\-19 |New features |None. |
|||Function optimization |Optimize the real\-time update mechanism of the synonym plugin. |
|||Bug fixes |None. |
|7.10.2\-25.8.0 |2025\-04\-16 |New features |* Add drived source.<br><br>* Add support for time\-based field query index pruning.<br><br>* Add support for paginated retrieval of snapshot shard information.<br><br>* Add support for configuring the attribute "ignore region during query".<br><br>* Add support for dynamically configuring index.check_pending_flush.enabled.<br><br>* Add the querycache caching strategy and remove the restriction that segments with less than 3% proportion are excluded from caching.<br><br>* Add the lz4nodict compression algorithm (in the byte\-codec plugin) to solve the issue of excessive IO.<br><br>* Add support for the jieba tokenization plugin. |
|||Function optimization |* Optimize lucene\-level memory locks to enhance write performance.<br><br>* Optimize certain security plugin functions.<br><br>* Optimize the real\-time update mechanism of the synonym plugin. |
|||Bug fixes |None. |



</Tab>
<Tab zoneid="GqmscTGCxV" title="Version 6.8.23">
<TabTitle>Version 6.8.23</TabTitle>


|**Version number** |**Release date** |**Type** |**Description** |
|---|---|---|---|
|6.8.23\-25.2.0 |2025\-04\-15 |New features |None. |
|||Function optimization |Optimize certain security plugin functions. |
|||Bug fixes |None. |



</Tab>
</Tabs>
