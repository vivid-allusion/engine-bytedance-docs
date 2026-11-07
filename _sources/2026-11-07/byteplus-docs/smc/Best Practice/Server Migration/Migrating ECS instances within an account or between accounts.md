---
title: "Migrating ECS instances within an account or between accounts"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Same-Account-or-Cross-Account-migration-of-ECS"
---

SMC supports migrating servers from your local infrastructure or other cloud platforms to the BytePlus platform. It also enables you to migrate ECS instances within the BytePlus platform, under the same account or to a different account.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your BytePlus platform account and migration source must meet the requirements in the [Limits](https://docs.byteplus.com/en/docs/smc/Limits).

* You have [completed preparations](https://docs.byteplus.com/en/docs/smc/Preparations).

* If you need to migrate data from a custom BytePlus image, you first need to create an instance using that image before initiating the migration. For instructions, see [Purchasing an instance based on an image​](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images).


<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When the cross\-region image copy or image sharing features cannot meet your needs for ECS instance migration, follow the following guide to enable ECS instance migration within the same account or across different accounts.


* **Migration within the same account**

   Migrate an ECS instance from an account on the BytePlus platform within the same region or to another region under the same account.

* **Migration across accounts**

   Migrate an ECS instance from an account on the BytePlus platform to a different account on the BytePlus platform, within the same region or to a different region.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a-85YWl6L-B56e75rqQ"></span>
### Step 1: Import the migration source


<Tabs>
<Tab zoneid="DR3wWyL7eL" title="Migration within the same account">
<TabTitle>Migration within the same account</TabTitle>

1. [Log in to the instance to be migrated](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. [Import the migration source](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources).


</Tab>
<Tab zoneid="xh6GpbAOoP" title="Migration across accounts">
<TabTitle>Migration across accounts</TabTitle>

1. Use the account to which the migration source instance belongs to [log in to the instance to be migrated](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. [Import the migration source](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources).


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqM77ya6L-B56e75LqR5pyN5Yqh5Zmo"></span>
### Step 2: Migrate ECS instance


1. Use the account to which the destination instance belongs to log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region where the target instance is located, and in the left directory tree, select "Server Migration Center \> Migration Source".

3. Click the "Create migration task" button in the "Actions" column of the target migration source.

4. Configure the same\-region/cross\-region migration task by referring to [Creating and starting migration tasks](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task).


<span id=".5q2l6aqk5LiJ77ya5p-l55yL6L-B56e75Lu75Yqh"></span>
### Step 3: View migration task


1. After migration starts, you can log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region where the target instance is located, and in the left directory tree, select "Server Migration Center \> Migration Job".

3. View task progress and result.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_208062d697ea10baf18f10e00296a1dc.png) </span>


After migration, you can log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance) and use the login password/key pair of the source ECS instance to log in to the destination ECS instance.
