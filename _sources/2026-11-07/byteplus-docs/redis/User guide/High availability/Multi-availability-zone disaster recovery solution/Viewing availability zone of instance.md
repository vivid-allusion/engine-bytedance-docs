---
title: "Viewing availability zone of instance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-az"
---

Cache for Redis supports single availability zone deployment and multi\-availability zone deployment. After the instance is created, you can view the availability zone information of the instance on the Redis console.

## Prerequisite

A multi\-availability zone deployment solution has been set for the target instance. For specific procedures, refer to [Deploying in multiple availability zones](https://docs.byteplus.com/en/docs/redis/deploy-multi-az).

## Procedure

You can use either of the methods below to view the availability zone information of the instance.

### Method 1: View on the Instances page

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the **Availability zone** column of the **Instances** page, you can view information of the availability zone in which the target instance is located.

   The information of availability zones displayed may vary according to the deployment solution, where:

   * Multi\-availability zone deployment

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a9877ab2e9d2dc9e7b920116a97766d.png)

   * Single availability zone deployment

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_695d721bfe630d48c08e12e13032296d.png)

### Method 2: View on the instance's Summary page

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Basic information** pane of the **Summary** page, you can view information of the availability zone in which the target instance is located.

   > **tip**

   > You can also view the role and the availability zone information of the server node in each shard's **Topology** area of the **Summary** page. For more details, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

   The information of availability zones displayed may vary according to the deployment solution, where:

   * Multi\-availability zone deployment

      ![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6555d285fc86cd217adcc6b337099668.png)

   * Single availability zone deployment

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0152824b7d88e23d1a14a65b08dbb341.png)
