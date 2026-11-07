---
title: "Instance sessions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/instance-session"
---

Cache for Redis provides instance sessions feature, which support real\-time viewing of session details when each client accesses a Redis instance, including the node connected to the current session, client address and port information, commands executed and length of connection duration. You can terminate abnormal sessions according to service requirements or download session information locally for analysis and management.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Instance sessions** sub\-tab.

6. On the **Instance sessions** sub\-tab, you can perform the following actions.

   |Supported operations |Description |
   |---|---|
   |View session details |The session details list displays all the current session details for instance.<br><br><br>* In the **Node ID** drop\-down list, select the target node to quickly filter out sessions connected to the target node. By default, session information for all nodes in the instance is displayed.<br><br>* You can click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c0fb07367dc9d64ea42e9dd8ad49dd8.png)icon next to each field name to view the specific meaning of the field. For more information on the various fields in the session list, refer to [Client list command](https://redis.io/commands/client-list/).<br><br><br>> **tip**<br><br><br><br>* > There is a delay of approximately 3 minutes in Instance session information updates. For example, if the actual data update time is 2023\-07\-17 15:51:00, the time recorded in the session list is approximately 2023\-07\-17 15:48:00.<br><br><br>* > To manually refresh the session information, click![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9922286936256abfa0d80ced4257c0ee.png)icon in the upper\-right corner of the list. You can also enable **Auto refresh** and set the auto refresh frequency. By default, it will automatically refresh every 30 seconds. You may also set it to automatically refresh every 5, 10, or 15 seconds according to your service requirements.<br><br><br>* > You can enter the client address and port number, or the session ID in the search box in the upper\-right corner to filter the session information. Fuzzy search is supported.<br><br><br>* > To download the session list to a local device for analysis and management, please click![](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg)icon in the upper\-right corner, check the fields you want to view in the pop\-up dialog box, and click **OK**.<br> |
   |Terminate abnormal sessions |1. You can select a specific session according to your service requirements,<br><br>2. and click **Kill selected sessions** on the upper\-left corner.<br><br>   > **tip**<br>   <br><br>   > To terminate all sessions, directly click **Kill all sessions** on the upper\-left corner.<br>   <br><br>3. In the pop\-up dialog box, click **OK**.<br><br><br>> **warning**<br><br><br>> Terminating the sessions will cause the connections involved to be automatically disconnected. Please proceed with caution.<br> |
   |View session statistics |* **Summary**<br><br>   The session statistics list contains information such as the total clients involved in instance sessions, and the number of active clients.<br><br>* **Source statistics**<br><br>   Session counts are based on the source (that is client address). To download the source statistics list for local analysis and management, click![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg)icon in the top\-right corner of the list, then select the fields you want to view in the pop\-up dialog box, and finally click **OK**. |

## Relevant APIs

|**API** |**Description** |
|---|---|
|[DeleteAllClientSession](https://docs.byteplus.com/en/docs/redis/deleteallclientsession) |Call the DeleteAllClientSession API to terminate all sessions in target Redis instance. |
