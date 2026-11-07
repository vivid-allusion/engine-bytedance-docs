---
title: "Deleting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Deleting_file_systems"
---

You can delete a FileNAS file system if you no longer need it.

<span id="19dc8dda"></span>
## Notes

All data will be permanently deleted if you remove the file system.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you delete a file system with a running DataFlow policy, the system will not automatically synchronize or export any newly added or modified files in the relevant paths to the associated object bucket. To do so, create a new eviction task and complete it before deleting the file system.</div>


<span id="aa063785"></span>
## Steps


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File** **System** \> **File** **System** **list**.

4. On the **File System list** page, click **Delete** in the **Actions** column of the target file system.

5. In the dialog box, click **Delete** to remove the file system.
