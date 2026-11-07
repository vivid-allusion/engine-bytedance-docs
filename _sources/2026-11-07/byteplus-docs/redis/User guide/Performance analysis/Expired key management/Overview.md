---
title: "Overview"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Expired_key_management"
---

Cache for Redis provides an expired key management feature, supporting one\-click scanning (SCAN) of all keys and immediate deletion of expired ones to free up memory.

<span id="jC4G7eir"></span>
## Feature introduction

Cache for Redis offers the following default cleanup strategies for expired keys.


|Default clear strategy |Strategy description |
|---|---|
|Regular cleanup |The system periodically scans and automatically clears expired keys in the background. You can configure the number of scan tasks executed per second via the `hz` parameter. For more details, refer to [Supported parameter](https://docs.byteplus.com/en/docs/redis/supported-parameter). |
|Passive clear (lazy clear) |When a user accesses an expired key, the system will automatically delete it. |
|Forced eviction<br><br> |When Redis memory space is insufficient, to ensure the hit rate, it will select corresponding data for eviction based on the key eviction policy set by the [maxmemory-policy](https://docs.byteplus.com/en/docs/redis/supported-parameter) parameter.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The default key eviction policy for Cache for Redis is <code>volatile-lru</code>, which means selecting the least recently used keys from those that have been set to expire for deletion. You can also select an appropriate eviction policy based on your business needs. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy">Setting key expiration and eviction policies</a>.</div><br> |


To ensure instance read/write performance, expired data is not immediately deleted but gradually cleaned up through asynchronous deletion (including active cleanup, passive cleanup, and forced eviction), so expired data still occupies memory space.

If a large number of keys expire within a short period (for example, hundreds of thousands or even millions of keys expire within 1~2 hours) and the instance's key count remains significantly lower than expected, there may be a large number of expired keys in the Redis instance that have not been promptly cleaned up. In such cases, you can use the expired key management feature provided by Cache for Redis to scan all keys and immediately clear the expired ones to free up memory.

<span id="2GwsNtg2"></span>
## Expired key clear task status

The following table summarizes the details of Cache for Redis expired key clear tasks.


|Task status |Status code |Description or impact |
|---|---|---|
|Task created. |Created |Successfully created the expired key clear task. You can manually cancel the task at this point. For specific procedures, refer to [Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task). |
|Task running. |Running |Expired key clear task is in progress. You can manually cancel the task at this point. For specific procedures, refer to [Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task). |
|Task finished. |Finished |Expired key clearance task finished. Expired keys will be deleted, and the corresponding memory space will also be released. |
|Task failed. |Failed |Expired key clear task failed. You can try recreating a clear task. If still fails, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support. |
|Task cancelled. |Interrupted |Expired key clear task cancelled. You can initiate the expired key clear task again during off\-peak hours, as needed for your business. |


<span id="hS5EyTQl"></span>
## **Relevant documents**


* [Clearing expired key](https://docs.byteplus.com/en/docs/redis/clear_expired_key)

* [Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task)
