---
title: "Key value management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/key-value-management-for-redis"
---

This topic describes how to visually create, delete, and edit key values in the command execution window of the Database Workshop (DBW) console to achieve full lifecycle management of key values.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [set a password for the default account](https://docs.byteplus.com/en/docs/redis/create-manage-account).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The value range of DB is [0, 255].

* If you need to search for a Key, it is recommended to use exact search. Fuzzy search is executed through the `scan` command. When the number of KEYs is large, timeouts or certain impacts on the instance may occur.

* The current Console only supports the Resp2 protocol, with Resp3 protocol not yet available.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu66ZSu5YC8"></span>
## Create Key value


1. Log on to the [data interaction platform for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis).

2. In the visual area of the **Data interaction platform** page, switch to the target **DB**, and then click **Create**.

3. On the **Create KEY@{database name}**  tab, configure the Key value information, as shown in the following table.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Type** |From the drop\-down list, select the key type. The following options are supported:<br><br><br>* String<br><br>* zset<br><br>* set<br><br>* hash<br><br>* list |
   |**Key name** |Custom key name. |
   |**TTL (time to live)** <br><br> |(Optional) Set the key's expiration time, in seconds. The input box automatically displays the remaining TTL of the current key (displayed as  **\-1** when there is no expiration time). If the value is not modified upon submission, the original TTL is retained. To set it to never expire, enter  **\-1**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Setting the Key's TTL can help you effectively manage the lifecycle of caches and data, and it is suitable for scenarios such as cache validity control, scheduled tasks, and session management.</div><br> |
   |**Key value** |Based on the key type, select a value configuration scheme as needed:<br><br><br>* When the key type is **string**, enter the corresponding value in the **Key value** area.<br><br>* When the key type is **zset**, click **Add rows** and configure the following parameters:<br><br>   * **Element name**: Custom.<br><br>   * **Element fraction**: Set the element fraction as required.<br><br>* When the key type is **set**, click **Add rows** to configure the **Element name**. The element name supports customizing.<br><br>* When the key type is **hash**, click **Add rows** to configure the following parameters:<br><br>   * **Field name**: Custom.<br><br>   * **Element value**: Set the element value as required.<br><br>* When the key type is **list**, click **Add rows** to configure the **Element value**. The element value supports customizing. |
   

4. Click **Submit**.

5. In the **Execute command** dialog box, confirm the execution statement, and click **Execute**.

   If there are many key values created, you can accurately query the Key value information through Key in the visual area.


<span id=".57yW6L6R6ZSu5YC8"></span>
## Edit Key value

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only modifying the value of Key is supported. Modifying the type and name of Key is not supported.</div>


* <div data-tips="true" data-tips-type="warning">When the key type is <code>zset</code>, <code>hash</code>, or <code>set</code>, be aware that the current Table only saves the operation records of the current page. Switching the page will lose the operation records of the current page. Proceed with caution.</div>


1. Log on to the [data interaction platform for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis).

2. On the **Data interaction platform** page, switch to the target database.

3. Select the target Key value, right\-click the **Key name**, and then click **Edit Key**.

4. On the **Edit KEY@{database name}**  tab, edit the following information.

   
   |**Parameter** |**Description** |
   |---|---|
   |**TTL (time to live)** <br><br> |(Optional) Set the key's expiration time, in seconds. The input box automatically displays the remaining TTL of the current key (displayed as  **\-1** when there is no expiration time). If the value is not modified upon submission, the original TTL is retained. To set it to never expire, enter  **\-1**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Setting the Key's TTL can help you effectively manage the lifecycle of caches and data, and it is suitable for scenarios such as cache validity control, scheduled tasks, and session management.</div><br> |
   |**Key value** |Based on the key type, select a value configuration scheme as needed:<br><br><br>* When the key type is **string**, enter the corresponding value in the **Key value** area.<br><br>* When the key type is **zset**, click **Add rows** and configure the following parameters:<br><br>   * **Element name**: Custom.<br><br>   * **Element fraction**: Set the element fraction as required.<br><br>* When the key type is **set**, click **Add rows** to configure the **Element name**. The element name supports customizing.<br><br>* When the key type is **hash**, click **Add rows** to configure the following parameters:<br><br>   * **Field name**: Custom.<br><br>   * **Element value**: Set the element value as required.<br><br>* When the key type is **list**, click **Add rows** to configure the **Element value**. The element value supports customizing. |
   

5. Click **Submit**.

6. In the **Execute command** dialog box, confirm the execution statement, and click **Execute**.


<span id=".5Yig6Zmk6ZSu5YC8"></span>
## Delete Key value

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deleted Key values can not be recovered. Proceed with caution.</div>



1. Log on to the [data interaction platform for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis).

2. On the **Data interaction platform** page, switch to the target database.

3. Select the target Key value, right\-click **Key name**, and then click **Delete Key**.

4. In the **Execute command** dialog box, confirm the execution statement, and click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec API to cancel SQL execution. |
