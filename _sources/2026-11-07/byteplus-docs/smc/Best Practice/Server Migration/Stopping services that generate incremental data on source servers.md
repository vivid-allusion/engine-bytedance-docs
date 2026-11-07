---
title: "Stopping services that generate incremental data on source servers"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Stop-generating-incremental-data-in-the-source-server"
---

Servers used in scenarios such as gaming, social media, and e\-commerce typically have requirements for data consistency. Therefore, before performing the final incremental migration, you need to stop the workloads on the source server that continuously generate data. This prevents data loss or other issues in the migrated business system.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the source server from which incremental migration is in progress.

2. Execute the following command to check whether any non\-system applications are running.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this topic, CentOS 7.9 is used as the operating system of the source server.   </div>
   

   ```Plain Text
   ps -ef
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5e5c99f27f79e3c0e2252c61c51920e2.png) </span>

3. Execute the following command to stop the application that affects data consistency.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this topic, MySQL is to be stopped. Replace <code>mysqld</code> with the actual application you need to stop.   </div>
   

   ```Plain Text
   systemctl stop mysqld
   ```
   

4. Execute the following command to check whether the target application has been stopped.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this topic, MySQL is to be stopped. Replace <code>mysqld</code> with the actual application.   </div>
   

   ```Plain Text
   systemctl status mysqld
   ```
   

   If the following output is displayed, the target application has stopped running.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28537cdb9345f6b7af2e06aaefb740f5.png) </span>
