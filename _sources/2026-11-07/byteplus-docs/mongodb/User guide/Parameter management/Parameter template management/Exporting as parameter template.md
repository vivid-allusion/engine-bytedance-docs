---
title: "Exporting as parameter template"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/export-parameter-template"
---

The Document Database for MongoDB provides a parameter template export function. You can export the configuration of all parameters in the current instance as a parameter template, so that the parameter configuration of this instance can be quickly applied to other instances of the same database version through the exported parameter template.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance type must be a **Replica set** instance. For more information about replica set instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **NoSQL Database \> MongoDB \> Replica set instances**.

4. On the **Replica set instances** page, click the name of the target instance.

5. On the instance details page, click **Parameters** tab.

6. On the **Current parameter** sub\-tab, click **Export as template**.

7. In the pop\-up dialog box, configure the following parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   

8. click **OK**.
