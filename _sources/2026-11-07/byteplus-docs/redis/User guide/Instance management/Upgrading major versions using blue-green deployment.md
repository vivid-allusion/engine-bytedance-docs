---
title: "Upgrading major versions using blue-green deployment"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment"
---

Cache for Redis provides blue\-green deployment capabilities, allowing you to achieve zero\-downtime, low\-risk, and fully verifiable major database version upgrades. This topic describes the procedures for upgrading major versions using blue\-green deployment.

## **Prerequisites**

* Instances needed to upgrade major versions using blue\-green deployment must meet the following requirements:

   * The instance's database version is **not** Redis 7.0.

   * The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

   * The instance does not use additional bandwidth. If additional bandwidth is in use, cancel it first. For specific procedures, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).

   * The instance with sharding cluster enabled has not applied for direct connection address. If a direct connection address has been applied for, release it first. For specific procedures, refer to [Releasing direct connection addresses](https://docs.byteplus.com/en/docs/redis/release-direct-connection-address).

* Currently, only support creating **Pay\-as\-you\-go** green instances. Therefore, before creating green instance, ensure that the total value of your account balance (that is, cash balance) and vouchers must be at least USD 0. For more information, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go).

## **Precautions**

* A single instance can have at most one ongoing blue\-green deployment process each time.

* During the process of upgrading an instance's major version using the blue\-green deployment feature, both blue and green instances are **only allowed to perform information viewing operations**, for example, [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance), [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

## **Upgrade process**

When Cache for Redis upgrades major version using blue\-green deployment feature, it mainly involves 3 main processes: creating green instance, testing and verification, and blue\-green switch. The following table summarizes the detailed descriptions of each process for your reference.

|Upgrade process |Process description |
|---|---|
|1. Create green instance |To perform a major version upgrade using blue\-green deployment, you must first create a green instance. This method enables database updates to be applied with brief, predictable downtime. The blue\-green deployment model not only reduces risks during database updates (such as major or minor engine version upgrades) but also further shortens the associated service interruption. |
|2. Test verification |To ensure stable operation after upgrade, go to green instance's details page, obtain connection address,  [connect to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance) and conduct thorough testing. You can refer to the following suggestions for testing:<br><br><br>* Test scope recommendation: Prioritize validating core business scenarios (for example, data read/write, transaction execution, key expiration policies). Focus on high\-concurrency, high\-traffic operations consistent with production environment to confirm green instance functionality and performance meet expectations.<br><br>* Data consistency verification: Compare key data (for example, quantity and value integrity of core business keys) between blue (original instance) and green (new instance) to ensure complete and accurate data synchronization.: Compare key data between the blue (original instance) and green (new instance) ends (e.g., the number of core business keys, value integrity) to ensure that data synchronization is complete and accurate, with no omissions or discrepancies.<br><br>* Issue reporting: If you encounter functional anomalies, performance degradation, or data inconsistencies during testing, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support. We will assist in identification and resolution to prevent impact on upgrade schedule.<br><br>* Monitor memory usage: During testing, closely monitor the memory usage of the blue and green instances to prevent data synchronization anomalies caused by excessive test data in the green instance. For more details on memory usage, refer to [Monitoring and alerts](https://docs.byteplus.com/en/docs/redis/monitoring-metric). |
|3. Blue\-green switch |After thoroughly testing and verifying the green instance has no issues, you can choose appropriate time to perform the blue\-green switch operation based on your business needs:<br><br><br>1. After blue\-green switch completes, only business data and Redis major version are swapped between blue and green instances, ensuring seamless business access. Blue instance (original instance) configurations including metadata, connection method, allowlist, and account information remain unchanged.<br><br>2. During switching, the database may experience brief disconnections (1~3 times) or enter read\-only status for seconds. Operate with caution. It is recommended to perform the switch operation during off\-peak business hours and ensure the application has an automatic reconnection mechanism to minimize the impact of the operation on your business.<br><br>3. If write operations were performed on the green instance, restart the blue\-green deployment process to ensure data integrity and avoid inconsistency risks. If business assessment determines new data in green instance has no impact and is acceptable, redeployment is unnecessary and blue\-green switch can proceed directly. |

## Blue\-green deployment status

The following table summarizes the possible statuses in the blue\-green deployment process, along with relevant explanations and impacts for your reference.

|Blue\-green deployment status |Status code |Triggering operation |Description or impact |
|---|---|---|---|
|Initializaing |INIT |After creating the blue\-green deployment task, the system starts verifying source instance (that is, blue instance) related information and enters the **Initializaing** status. |At this time, both blue and green instances are **Blue\-green deployment in progress**, and both blue and green instances **are only allowed to perform information viewing operations**, such as [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) and [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).<br><br> |
|Creating green instance |PROVISIONING |After the blue\-green deployment task is successfully created, the creation of the target instance (that is, the green instance) begins. ||
|Green instance running |AVAILABLE |The green instance has been created and is in the running status, ready to enter the data synchronization phase. ||
|Data synchronizing |DATA_SYNCHRONIZING |After the green instance is in the running status, the system automatically triggers a data synchronization task, and the status will switch to **Data synchronizing**. ||
|Switchable |SWITCHOVER_AVAILABLE |After data synchronization is complete, blue\-green deployment enters the **Switchable** status. At this point, you can initiate the blue\-green switch operation after thorough testing and verification. ||
|Switching |SWITCHOVER_IN_PROGRESS |After initiating the immediate blue\-green deployment switch task, the status will change to **Switching**. ||
|Waiting for switch<br><br> |SWITCHOVER_PENDING<br><br> |When you choose to execute during the **maintenance period**, the blue\-green deployment will enter the **Waiting for switch** status, which will persist until the task is complete. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period). ||
|Switch failed |SWITCHOVER_FAILED |When an exception occurs (such ashealth check failure, write failure, or internal error) during the switchover leading to an incomplete switchover, the status changes to **Switch failed**. ||
|Deleting |DELETING |After canceling the blue\-green deployment task, the status will change to **Deleting**. ||
|Switch completed |SWITCHOVER_COMPLETED |After the blue and green instances are switched, the blue\-green deployment task will enter the **Switch completed** status. |The status of both blue and green instances is **Running**. You can perform view, change, and modify actions on the blue and green instances. |
|Deletion completed |DELETE_COMPLETED |Blue\-green deployment has been canceled, the corresponding blue\-green deployment task will end, and the status will change to **Deletion completed**. ||

## Billing instructions

Related costs are incurred when creating green instance. For instance billing details, refer to [Billing overview](https://docs.byteplus.com/en/docs/redis/billing-overview).

## **Procedure**

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. In the **Configuration** area of the **Summary** tab, click **Upgrade major version** after **Database version**.

5. In the pop\-up panel, follow the procedure to complete the following operations.

   **Step 1: Create green instance**

1. Click **Create green instance**.

   2. In the pop\-up panel, set the following parameters for the green instance based on your business requirements.

      |Parameters ||Description |
      |---|---|---|
      |Blue instance configuration ||Confirm the database version and instance specifications (including node specifications, quantity, and shard quantity) of the blue instance. |
      |Basic information |Green instance name |Set the name of the green instance. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters.<br><br><br>> **tip**<br><br><br><br>* > If the name of the green instance is not set, `<blue instance name>-green-<six-digit random code>` will be used as its default instance name.<br><br><br>   > For example, if the blue instance name is `redistest`, the default name of the green instance created for it might be `redistest-green-b4bf10`.<br>   <br><br>* > The instance name for Cache for Redis cannot exceed 128 characters, and `-green-<six-digit random code>` occupies a fixed 13 characters. Therefore, to fit the total length limit, the `<blue instance name>` part of the green instance name will only use the first 115 characters of the blue name.<br> |
      |Specification configuration |Database version |Set the database version for the green instance.<br><br>> **tip**<br><br><br>> The database version of the green instance must be greater than that of the blue instance. For example, if the database version of the blue instance is 5.0, then the database version of the green instance can be 6.0 or 7.0.<br> |
      ||Instance specification |No configuration required. The instance specifications of the green instance (including node specifications, quantity, and shard quantity) are consistent with those of the blue instance. |
      |Billing method ||Set the billing method for the green instance. Currently, only **Pay\-as\-you\-go** is supported. |

   3. In the lower\-right corner of the page, click **Confirm order**.

   4. On the **Confirm configuration** page, first confirm the configuration information of the green instance, read and check the service terms, then in the lower\-right corner of the page, click **Create green instance**.

      > **tip**

      > After clicking **Create green instance**, you will be automatically redirected to the **Summary** page of the blue instance, and the instance status will change to **Blue\-green deployment in progress**.

   **Step 2: Test verification**

1. Confirm that the green instance has been successfully created.

      On the Instances list page, view the status of the newly created green instance. When the status changes from **Creating** to **Blue\-green deployment**, it indicates that the green instance has been successfully created.

   2. Connect your services to the green instance and perform thorough testing.

      Refer to the suggestions in [Upgrade process](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#YLGXBKaL) for testing. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

   3. (Optional) If issues are found during test verification, refer to the following procedures to terminate the major version upgrade task by canceling blue\-green deployment:

      1. Go to the **Summary** page of the green instance.

      2. In the **Configuration area**, click **Cancel upgrade** next to **Database version**.

      3. In the pop\-up dialog box, click **OK**.

         > **tip**

         * > After clicking **OK**, the blue and green instances will no longer be synchronized or associated. They will each retain their existing configurations and convert to regular instances. We recommend that you promptly delete the green instance to avoid resource waste. For specific procedures, refer to [Deleting pay\-as\-you\-go instance](https://docs.byteplus.com/en/docs/redis/delete-instance).

         * > After issue is resolved, you can re\-initiate a major version upgrade task for instance.

   **Step 3: Blue-green switch**

1. On the **Summary** page of the blue instance, clicking **Upgrade details** next to **Database version** in the **Configuration** area to view and confirm the status of the newly created green instance and data synchronization progress in the pop\-up panel.

   2. When the green instance status changes to **Switchable**, click **Switch now**.

   3. In the **Blue\-green switch** dialog, select the execution time. You can choose to either **Execute now** or **Execution during maintenance period.**

      > **tip**

      * > If you select **Execution during maintenance period**, the status of the green instance will change to **Waiting for switch**, and this status will persist until the task is complete. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).

      * > The duration of blue\-green switch operations is affected by factors such as data write load and data synchronization links. If the switch operation takes too long to complete, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for assistance in troubleshooting.

## **Subsequent operations**

After completing the major version upgrade using blue\-green deployment and verifying that there are no issues with the upgraded instance, delete the green instance promptly to avoid resource waste. For specific procedures, refer to [Deleting pay-as-you-go instance](https://docs.byteplus.com/en/docs/redis/delete-instance).

## Relevant APIs

|**API** |**Description** |
|---|---|
|[CreateBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/createbluegreendeployment) |Call the CreateBlueGreenDeployment API to create blue\-green deployment task. |
|[DescribeBlueGreenDeployments](https://docs.byteplus.com/en/docs/redis/describebluegreendeployments) |Call the DescribeBlueGreenDeployments API to query blue\-green deployment task details for target Redis instance. |
|[SwitchoverBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/switchoverbluegreendeployment) |Call the SwitchoverBlueGreenDeployment API to perform blue\-green deployment switch for target Redis instance. |
|[DeleteBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/deletebluegreendeployment) |Call the DeleteBlueGreenDeployment API to cancel blue\-green deployment task for target Redis instance. |
