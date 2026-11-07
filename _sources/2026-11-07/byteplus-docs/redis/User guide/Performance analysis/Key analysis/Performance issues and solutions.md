---
title: "Performance issues and solutions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/performance-issue-and-solution"
---

Incorrect database usage, unreasonable business planning, and other factors can generate hot keys and big keys. Failure to discover and handle them in time may lead to degraded database performance and severely impact business operations. Cache for Redis supports performance analysis feature that helps timely discover and analyze details of hot keys and big keys in the database, providing data references for optimizing them.

<span id=".5Yik5pat5qCH5YeG"></span>
## Detection criteria


* **Big key**

   A typical big key contains a large amount of data or a large number of elements, such as members and the number of lists. The criteria for the big keys of Cache for Redis are as follows:

   * For String data, it is considered a big key if memory usage exceeds 10 KiB.

   * For non\-String data, it is considered a big key if the number of elements exceeds 5,000.

* **Hot key**

   A hot key is usually much more frequently visited than other keys. The criteria for the hot keys of Cache for Redis are as follows:

   Sample all visits in the database within the query time range (such as last 1 day). When the sampling times are in the hundreds (such as the 100th or 200th time), if the number of visits to the corresponding key of the sample exceeds 3,000, it is considered a hot key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to increase the sampling frequency (for example, sample once every 50 visits) to improve hot key detection accuracy, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Increasing the sampling frequency can improve data accuracy, but it also creates some performance overhead. It is recommended to choose an appropriate sampling frequency to ensure data accuracy while minimizing the impact on instance performance.   </div>
   


<span id=".5Lqn55Sf55qE5Y6f5Zug5LiO5bim5p2l55qE6Zeu6aKY"></span>
## Causes and potential issues


|Key type |Causes |Potential issues |
|---|---|---|
|Big key |* Ineffective service planning, application of Redis in unsuitable scenarios, or deficiencies in data structure design, for example, a failure to split keys, may result in excessive values or elements contained in certain keys.<br><br>* Inadequate consideration of data cleanup policy settings, such as failing to regularly clean up invalid data or not staggering the cache deletion times for big keys. |* **Slow access due to Redis blocking**: Due to Redis's single\-threaded nature, if an operation related to a big key (such as accessing or deleting it) takes a long time, it severely affects subsequent requests, can even cause Redis to block, and also impacts master\-replica replication.<br><br>* **Poor instance performance resulting from uneven memory usage**: In Redis instances with sharding clusters enabled, nodes with big Keys consume more memory space, and the memory in the cluster instance cannot be evenly distributed, resulting in memory capacity bottlenecks and degradation of overall instance performance.<br><br>* **Adverse effects on other services or applications**: Big keys mean Redis consumes more server network bandwidth. Besides degrading Redis's own performance, this also affects other services or applications on the server. |
|Hot key |Unexpected hot data (such as flash sale items and trending topics) can lead to hot key issues when access to a single key is overly concentrated or surges. This is common in read\-heavy and write\-light scenarios. |* **Concentrated traffic consumes CPU and network resources**: Excessive traffic concentration on a hot key can consume a substantial amount of CPU and network resources, resulting in uneven instance load and data skew issues, which may, in turn, cause other requests to timeout and be inaccessible.<br><br>* **Excessive requests lead to instance downtime and service avalanches**: A sudden surge in hot key traffic within a short period of time, exceeding the processing limit of Redis instances, may lead to instance downtime and service unavailability, which can easily lead to cache penetration and even avalanche, causing backend database services to crash. |


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

Cache for Redis supports performance analysis, allowing you to view the details of big keys and hot keys in the database in real time while using Redis. It also supports viewing historical details of big keys and hot keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).
