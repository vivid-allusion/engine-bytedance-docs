---
title: "ListSlowQueryAdviceApi"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ListSlowQueryAdviceApi"
---

Call the ListSlowQueryAdviceApi API to get detailed slow log diagnosis information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSlowQueryAdviceApi |The purpose of this request. The value is `ListSlowQueryAdviceApi`. |
|Version |String |Yes |2018\-01\-01 |API version number. The value is `2018-01-01`. |
|InstanceType |String |Yes |MySQL |Database type. Valid values are as follows:<br><br><br>* `MySQL`: instance for RDS for MySQL.<br><br>* `VeDBMySQL`: instance for veDB MySQL. |
|InstanceId |String |Yes |mysql\-0648c527\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br> |
|AdviceType |String |Yes |no_advice |Advice type. Valid values are as follows:<br><br><br>* `no_advice`: no advice.<br><br>* `index_advice`: index advice.<br><br>* `rewrite_sql_advice`: Rewrite SQL advice. |
|SummaryId |String |Yes |eb053670\-7d4b\-4654\-8676\-73da31a5\*\*\*\* |The unique identifier of each slow log diagnosis. |
|GroupBy |String |Yes |Module |Aggregation type. Valid values are as follows:<br><br><br>* `Advice`: Aggregate by advice.<br><br>* `Module`: Aggregate by module. |
|OrderBy |String |Yes |QueryTimeRatioNow |Sort type. The values are as follows:<br><br><br>* `QueryTimeRatioNow`: Sorts by the current query time ratio.<br><br>* `Benefit`: Sorts by revenue. |
|PageNumber |Integer |Yes |1 |Page number. The value range is between 1 and 200. |
|PageSize |Integer |Yes |10 |The number of records per page. The value range is between 1 and 100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |27 |Total number of slow log diagnosis suggestions. |
|AdvicesByGroup |Array of Object |[Array of AdvicesByGroup Object](https://docs.byteplus.com/en/docs/DBW/data-structure#array-of-advicesbygroup-object) |Diagnostic suggestions aggregated according to recommendations. If the value of `GroupBy` in the request parameters is `Advice`, the response parameter is `AdvicesByGroup`. |
|Advices |Array of Object |[Array of Advices Object](https://docs.byteplus.com/en/docs/DBW/data-structure#array-of-advices-object) |Diagnostic advice aggregated by module. If the aggregation type in the request parameter is `Module`, the response parameter is `Advices`. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=ListSlowQueryAdviceApi&Version=2018-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20250626T033530Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250626/cn-beijing/dbw/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceType":"MySQL",
    "RegionId":"cn-beijing",
    "InstanceId":"mysql-0648c527****",
    "AdviceType":"no_advice",
    "SummaryId":"eb053670-7d4b-4654-8676-73da31a5****",
    "GroupBy":"Module",
    "OrderBy":"QueryTimeRatioNow",
    "PageNumber":1,
    "PageSize":10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata":{
        "RequestId":"202507041645271E4CE53687E8F6836B25-342542",
        "Action":"ListSlowQueryAdvice",
        "Version":"2018-01-01",
        "Service":"dbw",
        "Region":"cn-beijing"
    },
    "Result":{
        "Advices":[
            {
                "Advice":"",
                "AdviceIndexSize":0,
                "AdviceLevel":"Low",
                "Benefit":0,
                "DB":"tpch",
                "QueryTimeAvgAfter":33.352660417661085,
                "Risk":"",
                "SQLModule":"SELECT `nation`,`o_year`,SUM(`amount`) AS `sum_profit` FROM (SELECT `n_name` AS `nation`,EXTRACT(YEAR FROM `o_orderdate`) AS `o_year`,`l_extendedprice`*(?-`l_discount`)-`ps_supplycost`*`l_quantity` AS `amount` FROM ((((((`part`) JOIN `supplier`) JOIN `lineitem`) JOIN `partsupp`) JOIN `orders`) JOIN `nation`) WHERE `s_suppkey`=`l_suppkey` AND `ps_suppkey`=`l_suppkey` AND `ps_partkey`=`l_partkey` AND `p_partkey`=`l_partkey` AND `o_orderkey`=`l_orderkey` AND `s_nationkey`=`n_nationkey` AND `p_name` LIKE ?) AS `profit` GROUP BY `nation`,`o_year` ORDER BY `nation`,`o_year` DESC",
                "SourceIPs":[
                    "100.65.**.**"
                ],
                "SpeedUp":1,
                "TableName":"lineitem,nation,orders,part,partsupp,supplier",
                "User":[
                    "sqlbrain"
                ],
                "agg":{
                    "DB":"tpch",
                    "ExecuteCount":419,
                    "ExecuteCountRatio":0.03,
                    "FirstAppearTime":1750809748,
                    "LastAppearTime":1750982260,
                    "LockTimeRatio":0.12,
                    "LockTimeStats":{
                        "Average":0.000004264916467780429,
                        "Max":0.000013,
                        "Min":0.000002,
                        "Total":0.0017869999999999997
                    },
                    "PSM":"-",
                    "PTAnalysisResult":" # Attribute pct total min max avg # ============= === ======= ======= ======= ======= # Count 0 419 # Exec time 15 13974.76s 30.15s 37.44s 33.35s # Lock time 0 1.8ms 2.0us 13.0us 4.3us # Rows sent 0 73.33k 175 175 175.00 # Rows examined 2 412.05M 965.28k 1.00M 983.41k # String: # Databases tpch # # EXPLAIN /*!50100 PARTITIONS*/ SELECT `nation`,`o_year`,SUM(`amount`) AS `sum_profit` FROM (SELECT `n_name` AS `nation`,EXTRACT(YEAR FROM `o_orderdate`) AS `o_year`,`l_extendedprice`*(?-`l_discount`)-`ps_supplycost`*`l_quantity` AS `amount` FROM ((((((`part`) JOIN `supplier`) JOIN `lineitem`) JOIN `partsupp`) JOIN `orders`) JOIN `nation`) WHERE `s_suppkey`=`l_suppkey` AND `ps_suppkey`=`l_suppkey` AND `ps_partkey`=`l_partkey` AND `p_partkey`=`l_partkey` AND `o_orderkey`=`l_orderkey` AND `s_nationkey`=`n_nationkey` AND `p_name` LIKE ?) AS `profit` GROUP BY `nation`,`o_year` ORDER BY `nation`,`o_year` DESC\G ",
                    "QueryTimeRatio":15.12,
                    "QueryTimeStats":{
                        "Average":33.352660417661085,
                        "Max":37.44366,
                        "Min":30.146108,
                        "Total":13974.764714999996
                    },
                    "RowsExaminedRatio":1.77,
                    "RowsExaminedStats":{
                        "Average":983414.2935560859,
                        "Max":1003217,
                        "Min":965281,
                        "Total":412050589
                    },
                    "RowsSentRatio":0.04,
                    "RowsSentStats":{
                        "Average":175,
                        "Max":175,
                        "Min":175,
                        "Total":73325
                    },
                    "SQLTemplate":"SELECT `nation`,`o_year`,SUM(`amount`) AS `sum_profit` FROM (SELECT `n_name` AS `nation`,EXTRACT(YEAR FROM `o_orderdate`) AS `o_year`,`l_extendedprice`*(?-`l_discount`)-`ps_supplycost`*`l_quantity` AS `amount` FROM ((((((`part`) JOIN `supplier`) JOIN `lineitem`) JOIN `partsupp`) JOIN `orders`) JOIN `nation`) WHERE `s_suppkey`=`l_suppkey` AND `ps_suppkey`=`l_suppkey` AND `ps_partkey`=`l_partkey` AND `p_partkey`=`l_partkey` AND `o_orderkey`=`l_orderkey` AND `s_nationkey`=`n_nationkey` AND `p_name` LIKE ?) AS `profit` GROUP BY `nation`,`o_year` ORDER BY `nation`,`o_year` DESC",
                    "SQLTemplateID":"55c9cb442b6418e35b79ac8797ecde33b664768318f2ed997c13bfe8c5e****",
                    "SourceIP":"100.65.**.**",
                    "SqlFingerprint":"",
                    "SqlMethod":"SELECT",
                    "Table":"lineitem,nation,orders,part,partsupp,supplier",
                    "User":"sqlbrain"
                }
            }
        ],
        "Total":27
    }
}

}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
