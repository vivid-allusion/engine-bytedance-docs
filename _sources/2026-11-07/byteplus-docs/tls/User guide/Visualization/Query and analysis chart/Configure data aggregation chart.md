---
title: "Configure data aggregation chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Statistical-chart-related-operations"
---

This section explains how to configure data aggregation chart operations in an existing dashboard.

<span id="98ce12ce"></span>
## Prerequisites

When configuring data aggregation charts, ensure the related conditions in [Notes](https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5) are met.

<span id="26fb77c6"></span>
## Steps to configure data aggregation chart


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **dashboard**.

4. Select the dashboard to add charts to, click **Add Chart,**  then click **Create Chart**.

5. Select the search time range.

6. On the **query and analysis** tab, add data sources as needed, select the target log topic, and enter the query and analysis statement.

7. On the **Data Transformation** tab, click **Add Transformation**, then click **Data Aggregation**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data transformation can also be enabled below the chart analysis on the query and analysis page, using data classification and data aggregation functions.   </div>
   

8. Select the connection method; refer to [Data Aggregation Connection Methods](https://docs.byteplus.com/docs/tls/Statistical-chart-related-operations#eb5f23fd), then click **Start Analysis**.

9. After the chart settings are complete, click **Save Dashboard**. Or click **Apply to Dashboard**, preview the effect, then click **Save** again.


<span id="eb5f23fd"></span>
## Data aggregation connection methods

The log service supports aggregating multiple query and analysis results into one by concatenation, appending, Cartesian product, inner join, left join, and right join, and displays them in statistical charts.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab1f804d351297062c8d151419f3e4d4.png) </span>


|Connection method |Description |
|---|---|
|Concatenate |After concatenating two data sources, columns from both data sources merge into one table. If columns share the same name, the merged column name becomes `DataSourceName.OriginalColumnName`. For example:<br><br><br>* Data source A contains key1, data source B contains key2; after concatenation, the table header is `key1`, `key2`.<br><br>* Data source A contains key1, data source B also contains key1; after concatenation, the table header is `A.key1`, `B.key1`. |
|append |After appending data source B to data source A, the values of A and B will merge by column name, and a new `__tls_dashboard_datasource__` column will indicate the data source of each row. |
|Cartesian product |The Cartesian product of data sources A and B pairs each row from A with each row from B, resulting in a dataset with rows equal to A multiplied by B. |
|Inline |When inner joining data sources A and B, matching is done using specified columns (e.g., ID), retaining only intersecting rows. |
|left join |When performing a left join on data sources A and B, data can be matched by specifying a column (such as ID). If a row in A has no matching row in B, the B part of that row in the result set will show null. |
|right join |When performing a right join on data sources A and B, you can match the data by specifying a column (such as ID). If B has no matching row in A, the A part of that row will show null in the result set. |
|full join |When performing a full join on data sources A and B, data can be matched by specifying a column (such as ID), and all rows are retained in the result set. |


<span id="7b3755f0"></span>
### Concatenation/appending example

After concatenating query and analysis results A and B, display them in one chart.


|Configuration |Example |
|---|---|
|Query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d75dd5784ecb221a59910d7ecbd65b7.png) </span> |
|Query and analysis results (A) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cba8fe8aced54d988da9787617152914~tplv-goo7wpa0wc-image.image) </span> |
|Query and analysis results (B) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cba8fe8aced54d988da9787617152914~tplv-goo7wpa0wc-image.image) </span> |
|Aggregation results |* Concatenation aggregation results<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9048a3a0dd7f2978054afa46db8d9ac3.png) </span><br><br>* Additional aggregation results<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4071ccb0bf31f2975c6cabb5d306120.png) </span> |


<span id="8153409e"></span>
### Cartesian product example

After aggregating query and analysis results A and B by Cartesian product, display them in one chart.


|configuration |Example |
|---|---|
|Query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eae15bbcce53ba543b87a0b0c27c1d71.png) </span> |
|Query and analysis results (A) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb356a3e7f23425aaa7cbd79e45e5277~tplv-goo7wpa0wc-image.image) </span> |
|query and analysis results (B) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d1307f1d5fd4cd4b05d15a52881978e~tplv-goo7wpa0wc-image.image) </span> |
|Aggregation result |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0283b49983594970af0258bad70e409d~tplv-goo7wpa0wc-image.image) </span> |


<span id="2afa890e"></span>
### Inner join example

After aggregating query and analysis results A and B by inner join, display them in one chart. The join field is `account_id`.


|Configuration |Example |
|---|---|
|query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97bb518db37bd3108ba06bc972a2d10a.png) </span> |
|Query and analysis results (A) |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e6d53f103ecf61d5c033542bc5b091c.png) </span> |
|query and analysis results (B) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd92b560a66d4552aa0486f7085d5f5b~tplv-goo7wpa0wc-image.image) </span> |
|Aggregation result |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e92c2f25175546eaa813ba67dcffc0ca~tplv-goo7wpa0wc-image.image) </span> |


<span id="f2100801"></span>
### Left join example

Aggregate the query and analysis results A and B using a left join, then display them in one chart. The joining field is `userId`.


|Configuration |Example |
|---|---|
|query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a1a8ab135ed4b8c6458751f10181528.png) </span> |
|Query and analysis results (A) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd83fe64fb5f4d0e986361a731ab231d~tplv-goo7wpa0wc-image.image) </span> |
|Query and analysis results (B) |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b5844e4553d85067dfe5e82ea3fbb2a.png) </span> |
|aggregated results |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc47c14fe76c9de94dda310fdd0f1121.png) </span> |


<span id="8c2f371b"></span>
### Right join example

Aggregate the query and analysis results A and B using a right join, then display them in one chart. The joining field is `userId`.


|configuration |Example |
|---|---|
|Query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d6a03a858377367b0d9e0f2263a213b.png) </span> |
|Query and analysis results (A) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9087ea58515d4c5db3d667fdd75ba475~tplv-goo7wpa0wc-image.image) </span> |
|query and analysis results (B) |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7b13243c1fedd9b641394f87e0bf1cd.png) </span> |
|Aggregation result |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c338d8a152617d60057c22a7babb84e8.png) </span> |


<span id="63356fcc"></span>
### Full join example

Aggregate the query and analysis results A and B using a full join, then display them in one chart. The joining field is `userId`.


|Configuration |Example |
|---|---|
|Query and analysis configuration |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66fdec9f3f8191b046b5ff06b5948e91.png) </span> |
|query and analysis results (A) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3603360d329c423e927d69ed32d08180~tplv-goo7wpa0wc-image.image) </span> |
|Query and analysis results (B) |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1337846f275aeb34cbe9a74cecb9d23.png) </span> |
|Aggregation result |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0464b6ad762ffd3f4f5dd0f65eff1b4.png) </span> |


<span id="47c367a7"></span>
## `$__timeGroup` macro

The log service supports adding the `$__timeGroup` macro configuration in the dashboard's query and analysis statements. The format of the `$__timeGroup` macro is `$__timeGroup(time column, time interval)`. Among them, the `time interval` can be a fixed interval (such as 5m) or the variable `${{__interval}}`.

<span id="5e04d954"></span>
### Fixed time interval method

`$__timeGroup` macro supports the following time intervals in the format `$__timeGroup(time column, fixed time interval)`, which allows grouping and aggregating time series data according to the specified time interval.


|Identifier |Description |
|---|---|
|`y` |year |
|`M` |month |
|`w` |week |
|`d` |day |
|`h` |hour |
|`m` |minute |
|`s` |second |
|`ms` |millisecond |



* Query and analysis statement

   ```SQL
   * | SELECT $__timeGroup(__time__, 5m) AS time, status, count(*) as cnt Group BY time, status ORDER BY time 
   ```
   

* Query and analysis results

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1f711dd9db4331133c48317a7e1414b.png) </span>


<span id="56d51133"></span>
### `${{__interval}}` variable method

The format is `$__timeGroup(time column, ${{__interval}})`, which supports automatically selecting a suitable time interval based on the current chart’s time range to group and aggregate time series data, ensuring reasonable aggregation granularity when performing query and analysis over different time ranges. Among them, `${{__interval}}` is a preset variable; please refer to [time granularity variable](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard#f69b568c) for detailed information. Usage examples:


* Query and analysis statement

   ```SQL
   * | SELECT $__timeGroup(__time__, ${{__interval}}) AS time, status, count(*) as cnt Group BY time, status ORDER BY time 
   ```
   

* Query and analysis results

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bee3bb00dcc1b9c2275f159e2629bdd3.png) </span>


&nbsp;
