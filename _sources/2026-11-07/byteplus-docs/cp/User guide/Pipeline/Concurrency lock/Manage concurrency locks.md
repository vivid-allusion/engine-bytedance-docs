---
title: "Manage concurrency locks"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_concurrency_locks"
---

This article introduces operations for managing concurrency locks, such as viewing, editing, deleting, and releasing them.

<span id=".5p-l55yL5bm25Y-R6ZSB"></span>
## View concurrency locks

Obtain information about the maximum concurrency, current concurrency, and other details of each concurrency lock.


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> concurrency lock**.

3. In the concurrency lock list, view all concurrency locks that have been created.

4. Click the target Concurrency Lock Name to view details of that concurrency lock.


<span id=".57yW6L6R5bm25Y-R6ZSB"></span>
## Edit the concurrency lock

Support modifying the name, description, sharing scope, and maximum concurrency of the concurrency lock.


1. In the concurrency lock list, click **edit** in the **actions** column.

2. In the pop\-up Edit Concurrency Lock dialog box, modify the parameters as needed.

3. After making changes, click **Confirm.** 


<span id=".6YeK5pS-5bm25Y-R6ZSB"></span>
## Release the concurrency lock

Manually release pipelines that are currently using the lock's concurrency slots. After the lock is released, if there are pipelines waiting in the queue, they will be granted concurrent access to the lock in a first\-in, first\-out order.

For example, assume that the maximum concurrency is N. After release, the N pipelines currently occupying concurrency will continue running normally, and the N pipelines that were previously queued will no longer need to wait and will start running immediately.


1. In the concurrency lock list, click **Release Lock** in the **actions** column.

2. In the pop\-up confirmation dialog, click **Confirm**.


<span id=".5Yig6Zmk5bm25Y-R6ZSB"></span>
## Delete a concurrency lock

After the concurrency lock is deleted, the execution of pipelines associated with the lock will no longer be constrained by it.


1. In the concurrency lock list, click the  **`···`**  in the **actions** column.  **\> delete**.

2. In the pop\-up secondary confirmation dialog, confirm the concurrency lock information. After confirming that everything is correct, click **OK**.
