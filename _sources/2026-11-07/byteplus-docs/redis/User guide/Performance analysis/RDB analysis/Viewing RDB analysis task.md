---
title: "Viewing RDB analysis task"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-rdb-analysis-task"
---

After the RDB analysis task is completed, you can view the basic information of the task, information of related shards, and details about big keys on the console. This topic describes how to view information about RDB analysis tasks.

## Prerequisites

* A RDB analysis task is created. For specific procedures, refer to [Creating RDB analysis task](https://docs.byteplus.com/en/docs/redis/create-rdb-analysis-task).

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## ßPrecautions

Currently, only RDB analysis tasks within the last 30 days can be viewed.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.ßßßß

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **RDB Analysis** sub\-tab.

6. In the upper\-right corner of the **RDB analysis** sub\-tab, set the query start and end time to filter analysis tasks.

   > **tip**

   > By default, analysis tasks from the last 1 day are displayed. You can view RDB analysis tasks from up to the last 30 days.

7. Find the target analysis task in the analysis task list, and click **View** in the **Actions** column on the right.

   > **tip**

   > The basic information of the RDB analysis task, information of related shards, and details about big keys will be displayed in the analysis results. For more information about analysis results, refer to [Analysis results](https://docs.byteplus.com/en/docs/redis/rdb-overview#.5YiG5p6Q57uT5p6c).
