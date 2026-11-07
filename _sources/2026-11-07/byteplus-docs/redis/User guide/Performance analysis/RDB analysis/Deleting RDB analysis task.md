---
title: "Deleting RDB analysis task"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/delete-rdb-analysis-task"
---

You can delete RDB analysis tasks no longer needed in a timely manner. This topic describes how to delete RDB analysis tasks on the Redis console.

## Prerequisites

* A RDB analysis task is created. For specific procedures, refer to [Creating RDB analysis task](https://docs.byteplus.com/en/docs/redis/create-rdb-analysis-task).

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Delete individual analysis task

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **RDB analysis** sub\-tab.

6. In the upper\-right corner of the **RDB analysis** sub\-tab, set the query start and end time to filter analysis tasks.

7. Find the target analysis task in the analysis task list, and click **Delete** in the **Actions** column on the right.

   > **tip**

   > The delete operation only applies to the selected analysis tasks. The backup files used by the analysis tasks will not be deleted.

8. In the pop\-up dialog box, confirm information of the analysis tasks to be deleted, and click **Delete** on the lower\-right corner.

## Deleting analysis tasks in batch

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **RDB analysis** sub\-tab.

6. In the upper\-right corner of the **RDB analysis** sub\-tab, set the query start and end time to filter analysis tasks.

7. Select the analysis tasks to be deleted from the analysis task list, and click **Batch delete** above the list.

   > **tip**

   > The delete operation only applies to the selected analysis tasks. The backup files used by the analysis tasks will not be deleted.

8. In the pop\-up dialog box, confirm information of the analysis tasks to be deleted, and click **Delete** on the lower\-right corner.
