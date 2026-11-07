---
title: "Delete a Line Group"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/5fdIEK"
---

This document introduces how to delete a line group.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Before deleting a line group, you need to consider carefully. If you delete a line group, it cannot be restored. You cannot roll back this operation.</div>


<span id="steps"></span>
## Steps

Follow the steps below to delete a line group.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Line management** page, find the line group you need to update, and click **Delete** in the **Actions** column.

   * If the line group is not used by any DNS record, the console will pop up a window asking if you are sure to delete the line group. Click **Confirm** and the line group will be deleted.

   * If the line group is used by any DNS record, the line group cannot be deleted. The console will pop up a **Failed to delete the line group** window. The window will display all the record sets that use the line group. You can click **Check** to view the corresponding record sets.
