---
title: "Expanding a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Expanding-a-file-system"
---

If the capacity of the current file system cannot meet your daily needs, you can expand the corresponding file system in the console. FileNAS supports manual expansion and automatic expansion.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* Only extreme file systems in the **running** state support expansion.

* The file system only supports expansion and does not support reduction.

* The expansion of the file system generally takes no more than 5 minutes, and it does not affect your file writing during the expansion.

* To avoid potential issues, expansion is not allowed when the file system capacity exceeds 99%. Please clean up some data before proceeding.


<span id=".5pON5L2c5q2l6aqk"></span>
## Manual expansion


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top navigation bar, select the region where the target file system is located.

3. In the left navigation bar, select **File System** \> **File System List**.

4. On the **File System Lis**t page, click **Expand** option in the **Actions** column corresponding to the target file system.

5. On the **Expand File System** page, set the new capacity for expansion.

6. Click **Confirm order** to complete the file system expansion.

   After the purchase is completed, you can click on Go to Console to view the recently expanded file system on the Instance List page.


<span id="49a7f50e"></span>
## Automatic expansion

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">After enabling the automatic scaling function, when the used storage space is greater than or equal to the set scaling threshold, the system will automatically scale up to ensure the stable operation of your business. If your preset quota is insufficient, the system will automatically increase it to meet the requirements of automatic scaling.</div>



1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top navigation bar, select the region where the target file system is located.

3. In the left navigation bar, select **File System** \> **File System List**.

4. On the **File System List** page, click the name of the target file system.

5. On the file system **Overview** tab, click **Edit** button in the **Auto\-expansion strategy** area.

6. In the pop\-up dialog box, set the following parameters.

   
   |Parameters |Description |
   |---|---|
   |Current state |Turn on the automatic scaling switch. |
   |Expansion threshold |Set the capacity threshold for triggering the expansion operation, with a supported range of 50% to 90%, with a default of 60%. Once set, when the used capacity of FileNAS exceeds the threshold, it will automatically expand according to the expansion step size. |
   |Expansion increment |Set the expansion increment for automatic scaling, with a supported range of 1GiB to 10GiB, and a default value of 1GiB. |
   |Auto\-expandsion Limit |Set the upper limit for automatic scaling, which is optional. The minimum value is the current storage space of the target instance, and the maximum is 64TiB. The default value is 64TiB. |
   

7. After completing the parameter settings, click **Modify**.


<span id="efec6438"></span>
### Other operations


* **View automatic scaling policy**: In the **Auto\-expansion strategy** area. on the file system **Overview** tab, view the details of the automatic scaling policy.

* **Modify automatic scaling policy**: On the file system **Overview** tab, click **Edit** button in the **Auto\-expansion strategy** area to modify the policy information.
