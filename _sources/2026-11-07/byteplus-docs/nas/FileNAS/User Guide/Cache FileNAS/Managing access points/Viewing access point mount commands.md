---
title: "Viewing access point mount commands"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Viewing_access_point_mount_commands"
---

After creating an access point, you can view and copy its mount command for later use. This guide shows you how to do that.

<span id="12661e16"></span>
## Prerequisites

The access point has been created. For detailed steps, see [Creating access points](https://docs.byteplus.com/en/docs/nas/Managing_access_points#a4a6cb20).

<span id="19a4f2a2"></span>
## Steps


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Integrated point** tab, then click the target access point.

6. In the access point details panel, locate the **Mount command** and click the copy icon at the end of the command to copy it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The mount command format is <code>mount -t fsx /nas/<access point ID>.<access point domain name>:/ <local mount directory></code>.   </div>
