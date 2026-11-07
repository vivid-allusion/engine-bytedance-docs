---
title: "Filtering instances by tags"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/filtering-instances-by-tags"
---

After successfully binding a label to an instance, you can filter by the label when retrieving the instance to filter out the list of instances that contain the specified label. This document describes the steps to filter resources based on tags.

<span id="background-information"></span>
## **Background information**

When you look up an instance in the RDS for SQL Server Console, if the SQL Server instance has a label set, you can filter and filter by specifying the label key and the label value to filter out all instances bound to the specified label. The supported filtering methods are as follows:


|filter method |explain |example |
|---|---|---|
|Filter by label key |Filter according to the label key, that is, only the label key is set when filtering, which means to view all instances where the label key is the specified string and the label value is any value. You can also specify multiple label keys to filter at the same time, indicating that you are viewing instances that match any of the filter criteria.<br><br>It only limits the label key and does not limit the label value during retrieval, which is suitable for the scene of fuzzy search. |Scenario 1: The label key is module, and the label value is empty, which means to view all instances in the label where the label key is module. Scenario 2: The label keys are module and owner, and the label values are both empty, indicating that all instances in the label where the label key is module or owner are viewed. |
|Filter by tag key + tag value |Filter according to label key + label value, that is, when filtering, specify both label key and label value, indicating that all instances bound to the specified label are viewed. You can also specify multiple tags to filter at the same time, indicating that you are viewing instances that meet any of the filter criteria.<br><br>Both label keys and label values are specified for precise search scenarios. |Scenario 1: The label key is module and the label value is http, indicating that all instances labeled module: http are viewed. Scenario 2: Filter condition 1 is module: http, and condition 2 is module: tcp, indicating that all instances with a label key of module and a label value of http or tcp are viewed. |


<span id="precautions"></span>
## **Precautions**


* When filtering, the label key is required and the label value is optional. A null label value indicates filtering for instances where the label value is not set.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the filter icon to the right of the **label** column.

4. In the text box that pops up, set the label keys and label values that need to be filtered.

5. You can click **Add Field** to enter multiple label keys to filter with multiple filter criteria of **or** relationship.

6. Click **OK**. The instance list displays all instance information that meets the filter criteria. To reset the filter criteria, you can click **Reset** to clear all filters and then re\-set conditions to filter according to step 4.
