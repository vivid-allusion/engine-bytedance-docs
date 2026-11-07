---
title: "Pre-processing Query"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/pre-processing-query"
---

This article will demonstrate, through an example, how to use a pre\-processed query in the console. For specifics on syntax and a detailed introduction, please see [Preprocessing query PREPARED STATEMENT](https://docs.byteplus.com/docs/bytehouse/preprocessing-query-prepared-statement).

<span id="da82029b"></span>
## Prerequisites

Before usage, please confirm that the cluster engine version has been upgraded to 2.5 or above.

<span id="03ba0b9e"></span>
## Usage example

We will use the system table `system.numbers` as an example to demonstrate how to create a pre\-processed query, quickly execute some query commands, and delete the pre\-processed query.

<span id="391181bd"></span>
### Create pre\-processing query


1. Visit the **ByteHouse Console \- Data Query** window, input the command to create a pre\-processing query.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c3882ca912a430fbf50731599306e78~tplv-goo7wpa0wc-image.image) </span>

2.  **[Important] Change “Automatic Allocation of Nodes” to “All Nodes”.** 

3. Select "all queries" and click Run.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55bdf0e389b24fa4aa9c1213c658f739~tplv-goo7wpa0wc-image.image) </span>

4. If the system returns "Run Successful," it means the pre\-processing query has been successfully created. Refresh the "Data Objects" list on the left to see that the creation has been completed in the "Pre\-processing Query."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f253ff8a169437d9acfce27daa12b15~tplv-goo7wpa0wc-image.image) </span>

5. Hovering the mouse cursor over the pre\-processing query will allow you to preview its SQL statement content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4327f92c4644813a79d1c9fde249c3c~tplv-goo7wpa0wc-image.image) </span>


<span id="20c1d63f"></span>
### Run a pre\-processing query.


1. In **the data query**, create a new window and enter the command to run the pre\-processing query. For example, we use "`EXECUTE PREPARED STATEMENT prep USING i = 5;`" and enter it in the query box.

2. **After selecting "All Nodes" and "All Queries",**  click run.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96511aa9b7e54b8995e4623235b4ff5d~tplv-goo7wpa0wc-image.image) </span>

3. The system has completed the query operation. This action is equivalent to the system executing the following statement.

   ```SQL
   SELECT count()
   FROM (SELECT number FROM system.numbers LIMIT 10)
   WHERE number < 5;
   ```
   


<span id="d1bdd06b"></span>
### Manage pre\-processing queries.


1. Visit the ByteHouse console "Data Manage" page to view all the preprocessed query lists in the left column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e95d5ccb723474c99b8aa0b146ee8b9~tplv-goo7wpa0wc-image.image) </span>

2. Click on a preprocessed query to view the corresponding SQL statement on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2101295f98a24db98939bb0e3b16d044~tplv-goo7wpa0wc-image.image) </span>

3. Click "Query" to immediately jump to the query window page, and the query statement is automatically filled in. Complete the part after `USING` to quickly use the preprocessed query function. Note, **when querying, you still need to check "All nodes".** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f97989738eed4a3dbab29cf693f2653c~tplv-goo7wpa0wc-image.image) </span>

4. In the data manage preprocessed query manage page, you can also click the fold button to "Delete" and "Clone".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d216cfa3f8204a0cbc500c242c254337~tplv-goo7wpa0wc-image.image) </span>


<span id="48dc0d0b"></span>
### Delete preprocessed query

We can delete a preprocessed query via a SQL statement or on the console manage page.

<span id="985faab1"></span>
#### Delete console


1. Visit the ByteHouse console "Data Manage" page, click on a preprocessed query in the left column to enter the details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2101295f98a24db98939bb0e3b16d044~tplv-goo7wpa0wc-image.image) </span>

2. Click the fold button and select "Delete".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d216cfa3f8204a0cbc500c242c254337~tplv-goo7wpa0wc-image.image) </span>

3. The system will perform a second confirmation. If you confirm the deletion action, click "Confirm".

4. The system will return a successfully deleted prompt, indicating the action was successful.


<span id="013d0ea3"></span>
#### Delete SQL statement


1. In **data query** create a new window and input the command to delete the prepared query. Like "`DROP PREPARED STATEMENT prep`".

2. Select "All nodes" and "All queries", then click Run.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd30582c0eca4eab95eba052209b24f8~tplv-goo7wpa0wc-image.image) </span>

3. If the system returns "Operation successful," it means the action is complete.
