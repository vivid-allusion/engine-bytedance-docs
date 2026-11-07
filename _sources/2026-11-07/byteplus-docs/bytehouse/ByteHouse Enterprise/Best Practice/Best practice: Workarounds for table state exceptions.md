---
title: "Best practice: Workarounds for table state exceptions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-workarounds-for-table-state-exceptions"
---

ByteHouse is a distributed database with MPP architecture. In order to achieve balanced storage of data and balanced distribution of queries, the definition of each table must exist and be consistent on every node.

This article will detail the steps to resolve "defects" and "conflicts" in the table state in ByteHouse.

<span id="6353acbe"></span>
## Table state definition

Table status reflects the distribution of tables in the cluster, as follows:


1. **Normal**: The distribution of tables in the cluster is normal.

2. **defect**: Some nodes of the table in the cluster are missing, which may cause some queries to fail because the table definition cannot be found, and the data between nodes is not balanced.

3. **conflict**: Inconsistent table definitions among some nodes in the cluster, or inconsistent definitions of distributed tables and local tables, may result in inconsistent returns from multiple queries.


You can view the status of the database & table on the "Data Management" page of the ByteHouse console.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acc4d5c38067438a9ffd5c8160948dba~tplv-goo7wpa0wc-image.image) </span>

<span id="23e63153"></span>
## Solution to table defect status

<span id="31a8d8a1"></span>
### Common error causes

The reason for the defective state of the table is that the "on cluster" syntax is not used when the table is built, resulting in some nodesShangweiSynchronize.

<span id="fa4be246"></span>
### Basic solution steps


1. To find the missing node of the table, refer to the following statement.


```SQL
SELECT table_name, create_table_query, host_address
from system.clusters as clusters 
left join (
    SELECT
        name as table_name,
        create_table_query,
        host() AS node
    FROM cluster(<cluster_name>,system,tables)
    where database = ''
 and (name = '' or name = '')
)  as systable
on clusters.host_address = systable.node;
```



2. Executing a table\-building statement with the "on cluster" syntax on a node of the missing table completes the table definition on each node.


<span id="dd26032b"></span>
### Use example

For example, in the defalut library, there is a test table for defect status.


1. Query table for missing nodes. After the SQL statement above is executed, you can see that the console returns the result that the test table is missing at a node (192.18.0.232).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb09a5390e774bde855c760388d12966~tplv-goo7wpa0wc-image.image) </span>


<span id="8cf82406"></span>
## Solution to table conflict status


1. Is the schema of each node consistent:

   ```SQL
   SELECT
       other_nodes.name as table_name,
       if(other_node_sql=first_node_sql,'same','diff') AS status,
       other_nodes.create_table_query AS other_node_sql,
       first_node.create_table_query AS first_node_sql,
       other_nodes.node
   FROM 
   ( 
       SELECT
           name,
           create_table_query,
           host() AS node
       FROM cluster('bytehouse_cluster_test', 'system', 'tables')
       WHERE database = '' AND (name = '' or name = '')
   ) AS other_nodes
   LEFT JOIN 
   (
       SELECT
           name,
           create_table_query
       FROM system.tables
       WHERE database = ''  (name = '' or name = '')
   ) AS first_node
   ON other_nodes.name = first_node.name
   ORDER BY name;
   ```
   

   If there is any inconsistency, then:

   * Find points of inconsistency (column names, column types, etc.)Solve this problem by rebuilding the correspondence table of the corresponding node (if the table has no data, or is a distributed table), or by Alter correspondence table.

2. Compare the columns of the local table and the distributed table:

   ```SQL
   SELECT
       name AS column_name,
       type AS column_type,
       host() AS node_name
   FROM cluster('bytehouse_cluster_test','system','columns')
   WHERE database = '' AND  (table = '' or table = '')
   ORDER BY column_name, node_name;
   ```
   

   If there is any inconsistency, then:

   * Find points of inconsistency (column names, column types, etc.)The problem is solved by reconstructing the distributed table corresponding to the node, or the distributed table corresponding to Alter.


<span id="1afc0cbf"></span>
## Summary

Through the above steps, we can solve the problem of abnormal table state in ByteHouse, ensure the normal distribution of tables in the cluster, and improve the performance and stability of the database.
