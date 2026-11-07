---
title: "How to handle exceptions during \"File replication\" migrations?"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/How-to-handle-exceptions-when-migrating-using-File-Duplication"
---

<span id=".5pWF6Zqc546w6LGh"></span>
## Symptom

During full or incremental migration of data based on the "File replication" method, an exception occurred, or the migration failed.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Cause

For data migration based on the "File replication" method, the rsync tool installed on the source server is used to transfer data. Issues related to rsync may cause migration errors.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Log in to the source server where the exception occurred.

2. Execute the following command to enter the directory where the Agent is located.

   ```Plain Text
   cd /root/download/
   ```
   

3. Execute the following command to view the most recent content in the rsync.log file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This log file is generated only for migrations performed based on the "File replication" method.   </div>
   

   ```Plain Text
   tail -f rsync.log
   ```
   

   **Sample output**

   As shown in the figure below, you can determine the cause of the exception based on the `ERROR` message. In this example, the exception occurred because the file name exceeded the maximum path length.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5199ad90b7c0b77750fefd32d74fd2d6.png) </span>
