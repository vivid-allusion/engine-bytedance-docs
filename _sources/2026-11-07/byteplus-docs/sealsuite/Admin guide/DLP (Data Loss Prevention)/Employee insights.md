---
title: "Employee insights"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/employee-insight-usage-guide"
---

**Employee Insights** helps Administrators understand enterprise data outbound activity. It also lets them view outbound channels, file types, data sensitivity levels, and more by employee, so they can identify abnormal or high\-risk behavior in a timely manner.

After you purchase **Data Security Agent**, SealSuite also uses AI to summarize employee behavior across channels. It automatically identifies risk events and analyzes possible risks and causes. For details, see AI employee insight.

## Employee Insights Overview Dashboard

In the left navigation pane of the Admin Console, choose **DLP** \> **Employee Insights** to go to the employee insights overview dashboard. You can filter global data by department and time range using the filter box at the top of the page.

### Risk Metrics

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2effa2ccec0b4897aa5ef2bef031f9c5~tplv-goo7wpa0wc-topic.webp)

The metric cards at the top of the page show the core metrics within the current filter scope:

* **Number of employees in the department**: The total number of employees in the selected department and its sub\-departments.

* **Number of employees who have sent source files**: The total number of employees who transferred files outbound within the selected time range.

* **Number of employees with risk events**: The total number of employees who triggered DLP risk policies. If you have not purchased the "Data Security Agent" license, this value is displayed as 0.

### Employee Risk List

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dad8078481a4b0db60ec7013b929abf~tplv-goo7wpa0wc-topic.webp)

The list is organized by employee and summarizes each employee's outbound transfer and risk data.

* **List view and filters**:

   * **Quick tabs**: By default, the list displays employees with **All** outbound files.

   * **List sorting**: By default, the list is sorted by descending **number of outbound files**. You can customize the sort order in the drop\-down list in the upper\-right corner.

   * **Conditional filters**: The page provides multi\-dimensional filters, including employee status, user name, source channel, file type, file size range, and data classification level.

   * **Custom columns**: Click **Columns** on the right side of the list to adjust the displayed fields as needed. The **Number of risk events** and **Risk event name** fields depend on the "Data Security Agent" license. If you have not purchased this license, these two fields cannot be selected for display in custom columns.

* **Core field descriptions**:

   * **Data sensitive level**: Counts the number of outbound transfers for each data sensitivity level (L1 to L9) involved in the employee's outbound files.

   * **Top 3 outbound channels**: Displays the three data outbound channels most frequently used by the employee and the corresponding number of outbound transfers.

## Employee Behavior Profile

In the employee risk list, click **Details** on the right side of the target employee to go to the employee behavior profile page and view the employee's data operation details.

### Employee Information Overview

The top of the page displays the employee's basic information, including employee name, department, and current employment status (such as active, pending departure, or departed). This helps Administrators include employee status in behavioral analysis.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dfaab32d29b49deb0bd74dd3e4fe709~tplv-goo7wpa0wc-topic.webp)

### Outbound Transfer Details View

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/098db1b85e594fb38557a2d997353334~tplv-goo7wpa0wc-topic.webp)

This view displays statistics on an employee's outbound data transfers:

* **File Outbound Trend**: A bar chart visualizes the employee's daily outbound action frequency within the selected time range. It clearly distinguishes between the total number of outbound transfers and the number of violations that hit sensitive policies.

* **Employee/department comparison**: A radar chart displays behavior deviation characteristics by overlaying the employee's activity across channels (Web, desktop software, code repositories, and more) with the department average. Vertices where the curve expands outward represent outliers for the employee.

* **File classification flow chart**: A Sankey diagram displays data flow paths and visualizes the mapping between file sensitivity levels and outbound destinations. This helps Administrators quickly identify the final destinations of high\-value assets.

* **Log statistics**: Provides raw evidence for all preceding charts. Administrators can clearly view the number of files transferred outbound by the employee through specific applications and the detailed list. Click **Query logs** in the **Actions** column to go to the employee's original audit trail and complete the evidence collection loop.

> **tip**

* > Website statistics are grouped by destination domain and include only outbound file logs that contain a destination URL.

* > Outbound file logs from Linux devices do not include destination website URLs, so these records cannot be grouped by website in Employee Insights. To view these records, go to **DLP \> Investigation Audit \> Audit Log \> File Sharing Log**.

### Export an Assessment Report

You can click **Export report** in the upper\-right corner of the page to export the employee's data security risk assessment report.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac4e14b27ba946749b8d848948f95d52~tplv-goo7wpa0wc-topic.webp)
