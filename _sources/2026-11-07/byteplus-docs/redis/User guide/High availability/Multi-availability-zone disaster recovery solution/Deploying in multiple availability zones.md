---
title: "Deploying in multiple availability zones"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deploy-multi-az"
---

Cache for Redis supports single availability zone deployment and multi\-availability zone deployment. Compared to single availability zone deployment, multi availability zone deployment has higher disaster recovery capability and can withstand server room level failures. This topic contains instructions on how to deploy Redis instances in multiple availability zones.

## Limits

Only **primary\-secondary** instances support multi\-availability zone deployment, while single\-node instances only support single availability zone deployment. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Precautions

Deployment across availability zones can improve availability, but there may be a network latency of 2 ms to 3 ms.

## Billing instructions

When creating an instance, selecting the multi\-availability zone deployment option will only incur the fees for creating the instance, and the multi\-availability zone functionality can be used free of charge.

## Procedure

> **tip**

> You can set the multi\-availability zone deployment solution to:

* > Creating an instance

* > Restore to new instance by backup file

* > Restore to new instance by point in time

* > Restoring deleted instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region for the instance.

3. According to your use case, enter the **Create instance** or **Recovery instance** page by referring to instructions on [Creatin instance](https://docs.byteplus.com/en/docs/redis/create-instance), [Restore to new instance by backup file](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ), [Restore to new instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ) or [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance), and set the parameters for the **Deployment plan** following the steps below:

   1. Select the **Deployment plan** as **Multiple availability zone deployment**.

   2. From the **Availability zone** drop\-down list, set the required availability zones for the primary node and each secondary node respectively.

      > **tip**

      * > If you select multiple identical availability zones, indicating that both the primary and secondary nodes are in the same availability zone, then during the instance creation, the system will automatically switch the deployment scheme to the **Single availability zone deployment** plan.

      * > Deployment across availability zones can improve availability, but there may be a network latency of 2 ms to 3 ms.

      After setting the **Deployment plan** parameters, proceed to set other parameters for the instance and buy the instance by reference to the Creating an Instance or Restoring an instance operation guidance.
