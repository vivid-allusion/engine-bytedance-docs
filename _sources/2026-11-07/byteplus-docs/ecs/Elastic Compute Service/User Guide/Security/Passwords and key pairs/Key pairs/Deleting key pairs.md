---
title: "Deleting key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleting-key-pairs"
---

This topic describes how to delete one or more key pairs in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You cannot delete key pairs associated with instances. If you want to delete a key pair associated with instances, [disassociate the key pair from the instances](https://docs.byteplus.com/en/docs/ecs/Unbinding-key-pairs-from-instances) before you delete the key pair.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the key pair is located. 

3. On the key pair list page, use one of the following methods to go to the "Delete key pair" page.

   * Delete a single key pair: Click the "Delete" button in the "Actions" column of the target key pair.

   * Delete multiple key pairs at the same time: Select one or more key pairs that you want to delete and click the "Delete" button at the bottom of the list.

4. In the dialog box that appears, confirm the key pair name.

5. After you confirm that the key pair name is correct, click the "Delete" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DeleteKeyPairs](https://docs.byteplus.com/en/docs/ecs/DeleteKeyPairs): Deletes key pairs

* [DetachKeyPair](https://docs.byteplus.com/en/docs/ecs/DetachKeyPair): Disassociates key pairs
