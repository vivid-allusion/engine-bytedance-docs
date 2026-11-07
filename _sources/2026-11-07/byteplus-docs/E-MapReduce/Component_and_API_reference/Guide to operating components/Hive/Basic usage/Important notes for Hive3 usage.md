---
title: "Important notes for Hive3 usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Important_notes_for_Hive3_usage"
---

<span id="_1-开启-ranger-不支持-dfs-命令"></span>
## 1. DFS commands are not supported when Ranger is enabled

If Ranger is enabled in Hive, the !dfs command cannot be used. [Refer to the official documentation link](https://issues.apache.org/jira/browse/RANGER-1866).

<span id="_2-casting-timestamps"></span>
## 2. Casting timestamps

Hive3 has made significant changes to time types, and the behavior of the cast function differs from Hive2. For example, 1706859973123 corresponds to Beijing time 2024\-02\-02 15:46:13. In Hive3, the behavior is as follows:

```sql
hive> select cast(1706859973123 as timestamp);
OK
2024-02-02 07:46:13.123
```


In Hive3, it is recommended to use `from_utc_timestamp` and `to_utc_timestamp`

Refer to the official documentation: [Different TIMESTAMP types](https://cwiki.apache.org/confluence/display/Hive/Different+TIMESTAMP+types) and [Hive UDFs](https://cwiki.apache.org/confluence/display/Hive/Hive+UDFs)
