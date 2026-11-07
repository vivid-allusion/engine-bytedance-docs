---
title: "Logging on to the data interaction platform (Cache for Redis)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis"
---

This topic describes how to log on to the data interaction platform to connect to a Cache for Redis instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an instance and account. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [Setting a password](https://docs.byteplus.com/en/docs/redis/create-manage-account).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After enabling password\-free access, community version instances of Cache for Redis can use the default account `default` to access the Cache for Redis instance without a password on the DBW console. For detailed steps, refer to [Enabling password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).

* Instances with security control enabled support password\-free login on the data interaction platform. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=en).

* When you select **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, the IP address of the DBW backend service host will be added to the allowlist of the database instance. The name of the allowlist is in the `DBW_Sole_***_***_***_Redis` format.

* Log out and log in again to restore all pages to their state before logging out.

* After 5 consecutive failed login attempts due to an incorrect username or password, DBW will lock the login for one minute. Try again after one minute.

* Do not modify or delete the allowlist during the login process, as this will prevent opening new command windows to execute commands, although the current window can continue to execute commands.

* Logging onto the DBW database interaction platform is temporarily not supported for instances with SSL encryption enabled.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instances without SSL encryption enabled can successfully log on to the DBW data interaction platform.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an instance that has successfully logged on to the DBW data interaction platform enables the SSL encryption service, the original connection will not be disconnected and other commands can still be executed, but new windows can no longer be opened.   </div>
   

* The current Console only supports the Resp2 protocol, with Resp3 protocol not yet available.


<span id=".6YCa6L-HLWRidy3mjqfliLblj7DnmbvlvZUtc3FsLeeql-WPow=="></span>
## Procedure


<Tabs>
<Tab zoneid="dLMRcEXg7H" title="DBW console entry">
<TabTitle>DBW console entry</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **SQL window**.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **Cache for Redis**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Connection Mode**<br><br> |Select a connection mode as needed. Options include **Proxy mode** and **Direct connection mode**. For more information about connection modes for Cache for Redis instances, see [View connection address](https://docs.byteplus.com/en/docs/redis/view-address?lang=en). |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
<Tab zoneid="z3p5n998hy" title="Cache for Redis console entry">
<TabTitle>Cache for Redis console entry</TabTitle>

1. Log on to the [Cache for Redis console](https://console.byteplus.com/db/region:db+cn-beijing/redis).

2. In the upper\-left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance list** page, click **Login** in the **Actions** column of the target instance.

4. In the **Database Workshop** dialog box, set the relevant parameters as shown in the table below.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance type** |From the drop\-down list, select **Cache for Redis**. |
   |**Instance name** |From the drop\-down list, select a target instance from **Recently logged in** or **All**. Fuzzy search is supported. |
   |**Connection Mode**<br><br> |Select a connection mode as needed. Options include **Proxy mode** and **Direct connection mode**. For more information about connection modes for Cache for Redis instances, see [View connection address](https://docs.byteplus.com/en/docs/redis/view-address?lang=en). |
   |**Database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   

5. Check **Remember password**, **Authorize Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

   After remembering the password, you won’t need to enter it for subsequent logins, helping to improve work efficiency. When you need to clear a remembered password, you can click **Clear record** for the target account in the **Database account** drop\-down list, which will forget the account password.


</Tab>
</Tabs>


<span id="RBZVHzxp"></span>
## Next steps

After logging in, you can perform the following operations in the command window:


* Visually create key values and others.

* Execute statement commands. For more information, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/executing-commands-for-redis).

* Click **Observation and diagnosis** to perform operation and maintenance management on the instance. For more information, refer to [Observation and diagnosis](https://docs.byteplus.com/en/docs/DBW/automatic-bandwidth-scaling-management-for-redis).

* Click **Instance details** to view the details of the instance. For more information, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

* Click **Log out** to exit the instance workbench.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |
