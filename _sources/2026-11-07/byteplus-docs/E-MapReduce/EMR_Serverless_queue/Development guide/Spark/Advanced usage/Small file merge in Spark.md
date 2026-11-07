---
title: "Small file merge in Spark"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Small_file_merge_in_Spark"
---

Serverless Spark provides automated small file merging for Hive tables, supporting the following two merge strategy configurations:


* Merge by file count

* Merge by file size


<span id="5c1caea5"></span>
## Merge by file count

Control the number of output files by adjusting the number of shuffle partitions.

```SQL
-- Required parameter
set spark.merge.files.enabled=true;

-- Optional parameter
set spark.merge.files.number=1;
```


<span id="5c572c57"></span>
## Merge by file size

Control the amount of data read from shuffle partitions using Spark AQE rules. Since file size also depends on the compression format and its compression ratio, the final generated file size may fluctuate to some extent compared to the preset parameter value.

```SQL
-- Required parameter
set spark.merge.files.enabled=true;
set spark.merge.files.byBytes.enabled=true;

-- Optional parameter
set spark.merge.files.byBytes.fileBytes=536870912;
set spark.merge.files.byBytes.compressionRatio=1;
-- fileBytes * compressionRatio is the estimated file size
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Dynamic partition insert is supported, but sort by, distribute by, and cluster by are not compatible, and the original sorting logic in SQL will not be inherited.</div>


* <div data-tips="true" data-tips-type="warning">Currently, operations on lake format tables are not supported. To merge small files in lake format tables, refer to the compact functionality provided by the corresponding format.</div>
