---
title: "Viewing access point mount commands"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Viewing_access_point_mount_commands"
---

After creating an access point, you can view and copy its mount command for later use. This guide shows you how to do that.

<span id="nhCdiyQf"></span>
## Prerequisites

You have created an access point. For instructions, see [Creating an access point](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW).

<span id="2etvM0v6"></span>
## Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access** **Point**.

6. On the **Access** **Point** page, click the access point you want to manage.

7. In the access point details panel, locate the **Mount command**. Click the copy icon at the end of the command to copy it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The mount command format is <code>mount -t fsx /efs/<access point ID>.<access point domain name>:/ <local mount directory></code>.   </div>
