---
title: "Diagnostic Analysis: Application Practice of Visual SQL Profiler"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/diagnostic-analysis-application-practice-of-visual-sql-profiler"
---

ByteHouse CDW supports visual query diagnostic capabilities; in scenarios such as slow SQL diagnostic analysis, you can add diagnostic parameters (**log_segment_profiles**) to the SQL commands as needed, and then conduct visual diagnostic analysis on the log page. This text introduces how to add diagnostic parameters and proceed on the visual SQL Profiler page for diagnostic analysis, covering the main procedure and key actions.

<span id="fbd2d7bc"></span>
# Caution


* Current visual diagnostic analysis only supports SELECT type statements.

* In ByteHouse CDW, diagnostic analysis is not activated by default for SELECT statements; you need to add the parameter (log_segment_profiles) to the specified SELECT statements to activate row diagnostic analysis for that SQL.

* The diagnostic parameter (log_segment_profiles) added in SQL is only valid for the current SQL execution.


<span id="6122e5d7"></span>
# Steps

Below, by using a simple example of a SQL worksheet query analysis, we introduce the complete process of the operations.

<span id="d1c610c1"></span>
## Step 1: Add diagnostic parameters in SQL

Log in and enter a specific SQL worksheet, then add diagnostic parameters to the query SQL statement. Example code is below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de5b0c6df85f4540a934a76528ccbe21~tplv-goo7wpa0wc-image.image) </span>

```SQL
select xxx  from xxx settings log_segment_profiles = 1;
```



* You can add diagnostic parameters to the SQL commands requiring diagnosis analysis using the settings command: log_segment_profiles.

* `log_segment_profiles = 1` indicates the activation of diagnostic analysis.


<span id="f3740a50"></span>
## Step2: Enter the **log page**


1. At the bottom of the page, click to get the Query ID for this query task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c07fd287cca4bc78fb01528e912a387~tplv-goo7wpa0wc-image.image) </span>

2. Click on the **Audit Logs** tab at the top, and in the **Query history**, find the local task log via the Query ID.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/418d6f41f97747638a1d402c7fe285cf~tplv-goo7wpa0wc-image.image) </span>

3. Click the Query ID to enter the detailed log page, where you can view the task's SEGMENT level and operator level diagnostic information.


<span id="9b549d7e"></span>
## Step3: Diagnostic Analysis


* View the overall details of the task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4276ae16deed4d1793cef553e0cc594b~tplv-goo7wpa0wc-image.image) </span>

   * You can view the visualized segment sequence of the current task in the middle of the page.

   * The left side of the page can be expanded to view details such as the total time consumed by the current query and SQL statement details.

   * The right side of the page allows you to view details of input/output and partition pruning.

* Clicking on a segment within the page allows you to further view the operational details of that segment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a10a72a926e4464bbdf9bf779d394b31~tplv-goo7wpa0wc-image.image) </span>
