---
title: "Exporting an instance list"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_an_instance_list"
---

You can view the instance resources on the cloud offline. This topic describes how to export the instance list.

<span id="prerequisites"></span>
## Prerequisites

The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. Click **Instance list** in the left\-side navigation bar.

4. On the **Instance list** page, click the **Export instance list** icon in the top\-right corner of the page.

5. In the pop\-up **Export instance list** dialog box, select the information to be exported. Information supporting export is shown in the table below:

   
   |**Information** |**Required** |
   |---|---|
   |Instance name/ID |Required |
   |Running status |Optional |
   |Availability zone |Optional |
   |Private address/port |Optional |
   |Public address/port |Optional |
   |VPC |Optional |
   |Instance type |Optional |
   |Tag |Optional |
   |Primary node specification |Optional |
   |Number of nodes |Optional |
   |Database version |Optional |
   |Billing method |Optional |
   |Creation time |Optional |
   |Project |Optional |
   

6. Click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">After export, the instance information is output as a CSV file that you can download locally to view with a text editing tool.</div>
