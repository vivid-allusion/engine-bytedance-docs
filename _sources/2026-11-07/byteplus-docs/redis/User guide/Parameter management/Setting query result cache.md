---
title: "Setting query result cache"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set_query_result_cache"
---

Cache for Redis provides query result cache feature. After enabling, the system caches eligible hot keys at the proxy layer to offload read request pressure on backend server nodes. This effectively mitigates issues such as uneven node load, resource overload, and even node unavailability caused by hot keys, ultimately reducing business access failure rates and improving overall service stability. This topic describes how to set query result cache in the Redis console.

## Prerequisites

The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Applicable scenarios

The query result cache feature is suitable for business scenarios with frequent reads but infrequent writes, where brief data inconsistency is acceptable. The following are common typical applications:

* **Trending searches or rankings**: For example, trending lists or real\-time Top N rankings, where data is updated infrequently but read pressure is extremely high.

* **High\-profile user information**: For example, basic profile data or follower counts of celebrities and key opinion leaders (KOLs), which are frequently accessed.

* **Global configurations or announcements**: For example, game announcements, event configurations, or system parameters that require global reads but change infrequently.

* **Flash sale or promotional product details**: For example, product information and pricing during events, where content is relatively static but access surges.

* **Hot content aggregated data**: For example, click counts or impressions for viral content, which are statistical data requiring frequent reads.

## Precautions

* To use the query result cache feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for application.

* Enabling the query result cache feature will introduce a 1\-second delay when reading hot keys. Before enabling this feature, confirm whether your business can tolerate brief data inconsistency.

* Only read requests for hot keys and their corresponding query results are cached; write operations on hot keys are not supported.

* Simple key\-value structures (such as String) yield better caching results, while complex data structures (such as ZSet) are less effective.

* Each Redis instance provides the proxy layer with 100 MB of hot key cache space, using an LRU (Least Recently Used) cache eviction policy.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Hot key analysis** sub\-tab, then click **Query result cache**.

6. In the pop\-up dialog box, set the following parameters according to your business needs.

   |Parameters |Description |
   |---|---|
   |Query result cache |Select **Enable** or **Disable** query result cache.<br><br>After the instance is successfully created, the query result cache feature is disabled by default. |
   |Cache validity period |Set the cache validity period for query results. Value range: 100~60000. Unit: milliseconds (ms).<br><br>> **tip**<br><br><br><br>* > This parameter takes effect only after **enabling** query result cache.<br><br><br>* > During the cache validity period, if the source data changes, cached query results are not automatically synchronized and updated, which may cause business side to read stale data.<br><br><br>* > It is recommended to comprehensively evaluate the cache validity period by considering [hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis) results and business tolerance for stale data:<br><br><br>   * > If the validity period is too short, ordinary keys may be frequently written to the cache, resulting in wasted cache resources.<br><br><br>   * > If the validity period is set too long, clients may continuously read stale data for an extended period.<br> |

7. Click **OK**.

   > **tip**

   * > After clicking **OK**, the instance status changes to **Parameter modifying**. When the instance status changes back to **Running**, confirm the feature status on the right side of **Query result cache** under the **Hot key analysis** sub\-tab.

   * > After enabling query result cache feature, you can view the cached hot keys under the **Hot key analysis** tab. For more details, refer to [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).
