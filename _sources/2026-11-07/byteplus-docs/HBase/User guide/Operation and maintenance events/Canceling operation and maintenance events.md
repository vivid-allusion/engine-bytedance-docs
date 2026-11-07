---
title: "Canceling operation and maintenance events"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Canceling_operation_and_maintenance_events"
---

Operations events scheduled to be executed within a maintainable time period can also be cancelled. This article describes how to cancel a planned event.

<span id="gEk98cXB"></span>
## Prerequisites

The operation and maintenance event is in **Waiting for execution** state.

<span id="LZBumisk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/region:db+cn-beijing/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left\-side navigation pane, select **Operation and maintenance event**.

4. In the list of scheduled events, click **Cancel** in the **Actions** column for the target event.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Once a planned event is canceled, it cannot be executed again and you need to re\-initiate the change task. Please operate with caution.   </div>
   

5. Click **OK** in the pop\-up dialog box.
