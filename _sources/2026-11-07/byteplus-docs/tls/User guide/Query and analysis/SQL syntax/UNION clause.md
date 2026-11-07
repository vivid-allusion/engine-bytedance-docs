---
title: "UNION clause"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/UNION-clause-2"
---

The UNION clause combines the analysis results of multiple SELECT statements.

<span id="b4d7b837"></span>
## **Syntax description**

The syntax format of the UNION clause is as follows:

```SQL
SELECT Key1 FROM Topic1 
UNION [ALL]
SELECT Key1 FROM Topic2
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The UNION clause can combine results across multiple topics. When you use the UNION clause to combine the results of multiple SELECT statements, each SELECT statement can involve different topics or projects.</div>


* <div data-tips="true" data-tips-type="tip">The analysis results of each SELECT statement in the UNION clause must have the same number and type of fields.</div>



Parameter description


|Parameter |Description |
|---|---|
|ALL |If the results of the SELECT statement contain duplicate rows, the UNION clause removes duplicate rows and reserves only one row by default. To reserve all duplicate rows, use `UNION ALL`. |
|Key |The name of a field or a column, where:<br><br><br>* The results of each SELECT statement must have the same number of fields.<br><br>* The data type of key1 and key2 must be the same, but the field names can be different. |
|Topic |The topic name. This parameter is required. To combine results across projects, specify the project names, such as `Project1.Topic1`. |


<span id="60b3bfaf"></span>
## **Examples**

<span id="a1158f96"></span>
### Example 1: Remove duplicate data when combining results

Count the status values of two services. Query the status field of the open_api and web_api topics and combine the results into one column. If the status field has duplicate values, only one value is returned.


* SQL statement:

   ```SQL
   * | 
   SELECT status FROM open_api GROUP BY status 
   UNION 
   SELECT status FROM web_api GROUP BY status
   ```
   

* Return result:

   
   |status |
   |---|
   |200 |
   |400 |
   |403 |
   |500 |
   


<span id="9835c347"></span>
### Example 2: Reserve duplicate data when combining results

Count the list of members of two groups. Query the staffname field of the groupA and groupB topics and combine the results into one column. All values of the staffname field are returned, even if duplicate values exist.


* SQL statement:

   ```SQL
   * | 
   SELECT staffname FROM groupA GROUP BY staffname 
   UNION ALL
   SELECT staffname FROM groupB GROUP BY staffname
   ```
   

* Return result:

   
   |staffname |
   |---|
   |Zack |
   |Lily |
   |Zack |
   |Mark |
