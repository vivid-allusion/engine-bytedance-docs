---
title: "Compaction strategy guide"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Compaction_strategy_guide"
---

This article mainly introduces the advantages and disadvantages of the hot and cold tier compaction strategy and explains its usage.

<span id="xBPxTn51"></span>
## Background

By default, after setting the hot/cold separation time boundary, you need to wait until the system completes the next compaction (a random number between 3.5 and 10.5 days) or manually execute the major_compact command before data can be migrated according to the hot/cold separation boundary. In this case, each compaction will interact with the cold storage files, which will slow down the compaction process and affect system stability.

To solve this problem, HBase adds a hot\-cold tiered compaction strategy to speed up the compaction process. The advantages and disadvantages of this function are as follows. Please make a reasonable choice based on your actual business situation.


* **Advantages**: Reduces compaction pressure and avoids selecting cold storage files every time a major compaction occurs. Only when the cold storage file threshold is exceeded will all cold storage files be compacted at once.

* **Disadvantages**: Delaying the compaction of cold storage files will cause read amplification when reading cold storage, and the cold storage capacity will also increase.


<span id=".5L2_55So5pa55byP"></span>
## How to use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function is only effective for tables that have hot and cold data separation enabled.</div>



1. Execute the following command in HBase Shell to enable the hot\-cold tier compaction strategy.

   ```sql
   alter 'table', CONFIGURATION => {'hbase.hstore.defaultengine.compactionpolicy.class' => 'org.apache.hadoop.hbase.regionserver.compactions.TieredCompactionPolicy'}
   ```
   

2. After it is enabled, the number of redundant files in major compaction is adjusted based on resource usage.

   ```sql
   alter 'table', CONFIGURATION => {'hbase.regionservers.compactions.tiered.file.max.num' => 2}
   ```
   

   Note: Setting the threshold to 2 means that cold storage is allowed to store two cold files generated after major compaction. That is, the cold files will be read during the third major compaction.
