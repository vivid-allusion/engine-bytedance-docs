---
title: "Configure the concurrency lock"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configure_the_concurrency_lock"
---

A concurrency lock is used to provide fine\-grained control over the maximum concurrency of a group of pipelines. Create and associate a concurrency lock

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

A concurrency lock defines the maximum concurrency level for a group of pipeline runs. A single run of the pipeline is considered as one unit of concurrency. When a group of pipelines is bound to the same concurrency lock, the maximum concurrency for that group will be limited by the concurrency lock. Pipelines that exceed the maximum concurrency will be queued in a first\-in, first\-out order.

For example, suppose five pipelines are bound to the same concurrency lock, which allows a maximum concurrency of three. A maximum of three pipelines can be in the **running** state at the same time. Any additional pipelines triggered will be in the **waiting for a lock** state and will queue in a first\-in, first\-out order.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The account has been configured with CPAdminAccess permission.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

A pipeline can only be associated with one concurrency lock.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65bm25Y-R6ZSB"></span>
### Step 1: Create a concurrency lock


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> concurrency lock**.

3. On the concurrency lock page, click **Create concurrency lock**.

4. On the Create Concurrency Lock page, enter the required parameters.



|Configuration Item |Descriptions |
|---|---|
|Concurrency Lock Name |The custom concurrency lock name must be globally unique. |
|Description |Enter remarks for the concurrency lock. This field can be left blank. |
|Sharing scope |Select the shared workspace range for the current concurrency lock Only pipelines under the selected workspace can be associated with this concurrency lock. |
|Maximum concurrency |Set the lock's maximum concurrency. The selectable range is 1 to 100. |



5. Click **OK** to complete the creation of the concurrency lock.


<span id=".5q2l6aqk5LqM77ya57uR5a6a5bm25Y-R6ZSB"></span>
### Step 2: Associate a concurrency lock

Bind all pipelines subject to concurrency constraints to the same concurrency lock. Pipelines support working across workspaces.


1. In the left navigation bar, select **workspace**. On the workspace page, click the name of the desired workspace to enter it.

2. Click **pipeline** to go to the pipeline list.

3. In the pipeline list, select the pipeline that needs to be associated with a concurrency lock, then click the  **`···`**  in the actions column.  **\> edit**.

4. On the pipeline edit page, switch to the basic information tab and select a concurrency lock for the current pipeline.

5. Click **Save** to save the pipeline configuration.

6. Optionally, repeat steps 1 through 5 to associate concurrency locks with other pipelines.
