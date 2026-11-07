---
title: "Hive data masking"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_data_masking"
---

Ranger supports Hive data masking (Data Masking), which allows masking the results returned by Select statements to conceal sensitive information.

<span id="dc9d77d2"></span>
## Context

This feature is only applicable to HiveServer2 scenarios (such as Select statements executed via Beeline, JDBC, and Hue).

<span id="26bc02cb"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Ranger screenshots in this document use version 2.3.0 as an example; for other versions, please refer to the actual interface.</div>


On the **Default\-hive** tab of the Ranger UI configuration page, you can perform data masking for Hive data:


* Multiple masking methods are supported. For example, displaying the first 4 characters, displaying the last 4 characters, applying hash processing, and so on.

* Wildcard characters are not supported when configuring mask policy. For example, you cannot configure an asterisk (\*) for Table or Column in the policy.

* Each policy can only configure a mask strategy for one column; if there are multiple columns, you need to configure a mask policy for each column.

1. For configuring Ranger for Hive components, see [Hive integration](https://docs.byteplus.com/docs/E-MapReduce/109418) for details.

2. On the Ranger page, click **Default_hive**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1909c4784eab4177babaea0604d5a42a~tplv-goo7wpa0wc-image.image" width="2934px" /></div>



3. Configure masking policy.

   1. Click the **Masking** tab at the top.

   2. Click **Add New Policy** in the upper right corner.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed01c37376748fd81d26b5417bd79cf~tplv-goo7wpa0wc-image.image" width="2934px" /></div>



3. On the **Create Policy** page, configure the relevant parameters.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae4222026044f23b0b193b3f8ecedc7~tplv-goo7wpa0wc-image.image" width="2928px" /></div>



|**Parameters** |**Description** |**Example** |
|---|---|---|
|**Policy Name** |Name of the policy. Can be customized. |test_mask |
|**Hive Database** |Add a database in Hive. |testdb |
|**Hive Table** |Add a table. |test_table |
|**Hive Column** |You can add column names. |id |
|**Select User** |Specify the user to add this policy for. |test |
|**Access Types** |Select the permissions to grant. |select |
|**Select Masking Option** |Select the masking method. |Partial mask: show first 4 |



4. Click **Add**.

5. **Optional:**  Test masked data.


For example: When the test user uses the `select id from testdb.test_table1;` statement to view the data in the id column of the `testdb.test_table1` table, only the first 4 characters are displayed normally, and the remaining characters are masked with `x`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8732fbdcc0384515b32449b56dc3d973~tplv-goo7wpa0wc-image.image) </span>
