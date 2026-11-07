---
title: "Bucket inventory"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-inventory2"
---

This article introduces common issues encountered during the use of bucket inventory for your reference.

<span id="2ca51210"></span>
### Why hasn't the inventory file been generated for a long time?

You can troubleshoot the reason why the inventory file was not generated based on the following causes.


|Possible causes |Solution |
|---|---|
|The target bucket or path for viewing the list file is incorrect |Check the inventory file according to the configured target bucket and path |
|The source bucket has no objects, or the configured inventory rules do not match any eligible objects |Please select appropriate objects to create the bucket inventory. |
|The number of objects matched by the inventory rule is too large, causing the inventory file generation to fail. |Set the export cycle reasonably based on the number of objects<br><br><br>* Number of objects < 10 billion: daily or weekly export is acceptable<br><br>* Number of objects between 10 billion and 50 billion: weekly export is recommended<br><br>* Number of objects \> 50 billion: specify prefixes and export in batches |
|Insufficient permissions |TOS supports bucket inventory via the `TosArchiveTOSInventory` role If you set bucket policies or IAM policies for business needs, or if the bucket has SSE\-KMS default encryption enabled, it may cause inventory file generation to fail. For details, see [permission description](https://docs.byteplus.com/docs/tos/Bucket-inventory#permission-description) |


<span id="8fbc3ce4"></span>
### What factors affect the speed of inventory export?

The export speed depends on the number of items exported. It is recommended to set the export cycle reasonably according to the number of objects.

If you need to export more than 10 billion objects, it is recommended to export the inventory file weekly; otherwise, the generation of the inventory file may fail.
