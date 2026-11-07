---
title: "Column-Level Access Control"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-column-level-access-control"
---

This section illustrates how Column\-Level Access Control is enforced in ByteHouse and configured by users. Column\-Level Access Control allows users to configure permissions on columns, allowing access only to the appropriate users. This is especially useful for limiting access to sensitive columns such as Personally Identifiable Information (PII).

<span id="configuring-column-level-access-control"></span>
## Configuring Column\-Level Access Control

To provide column\-level permissions, the user needs first to be provided with the associated table\-level permissions as follows:


|**Column Actions** |**Table Actions Needed** |
|---|---|
|SELECT |SELECT |
|INSERT |INSERT |
|ALTER |ALTER |
|DROP |ALTER |


<span id="granting-permissions-on-specific-columns"></span>
### Granting permissions on specific columns

You can specify columns that should be accessible to specific roles. In this case, " **demo_role** " is granted permission to `SELECT` `demo_col_one` .

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/6778b59-image-8-1627496763805.png) </span>

Once permission is granted permission to " **demo_role** ", " **demo_role** " would be able to select from `demo_col_one` only.

```sql
SELECT demo_col_one FROM demo_db.demo_table -- okay!

SELECT demo_col_one, demo_col_two FROM demo_db.demo_table -- access denied!
```


To grant users additional permissions on more columns, select click on the check box on the grid:

<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/e1e4c11-image-9-1627496764409.png" width="400px" /></div>


For example, by adding `SELECT` permission on `demo_col_two` , " **demo_role** " will now be able to perform select from `demo_col_two` as well:

```sql
SELECT demo_col_one FROM demo_db.demo_table -- okay!

SELECT demo_col_one, demo_col_two FROM demo_db.demo_table -- okay!
```


<span id="granting-permissions-on-future-columns"></span>
### Granting permissions on future columns

For specific users that can be granted permissions to all and future columns, simply click and enable the corresponding permission pill.

<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/89593fc-image-10-1627496765216.png" width="400px" /></div>


This should be applied to roles that can access all columns, including sensitive columns that could be added in the future. For `SELECT` permissions, " **demo_role** " will now be able to use `SELECT *` to view data of all columns.

```sql
SELECT demo_col_one from demo_db.demo_table -- okay!

SELECT demo_col_one, demo_col_two from demo_db.demo_table -- okay!

SELECT * from demo_db.demo_table -- okay!
```
