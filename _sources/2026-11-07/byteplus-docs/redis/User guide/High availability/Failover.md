---
title: "Failover"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/failover"
---

Cache for Redis supports failover. When an instance failure is detected, the system will immediately trigger a failover to restore the instance to normal operation, ensuring high availability of the instance. Additionally, Redis supports manually triggering failover to meet the needs of disaster recovery drills or enable close\-by access involving multiple availability zones.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance type is the **Primary\-secondary** instance. Failover is not available in single\-node instances. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

<span id=".6Kem5Y-R5Y6f5Zug"></span>
## Trigger events


* Manual trigger

   You may also trigger failovers manually to meet the needs of disaster recovery drills or enable close\-by access involving multiple availability zones. For specific procedures, refer to [Executing failover manually](https://docs.byteplus.com/en/docs/redis/switch-primary-node-manually).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After manually switching the primary node, if the instance fails, the system will immediately trigger a failover to ensure the high availability of the instance. At this time, the primary node of the instance may be inconsistent with the primary node you selected during the manual switch of the primary node.   </div>
   

* Failure trigger

   Cache for Redis adopts a health check mechanism based on the High Availability (HA) system for failure detection. The HA system conducts health checks to verify the health status of primary and secondary nodes. Instances will switch nodes based on different failure levels to ensure the instance resumes service within the shortest time possible. The failure levels and corresponding response mechanisms are illustrated in the table below.

   
   |Failure level |Failure response mechanism |
   |---|---|
   |The failure only affects the primary node |When only the primary node fails:<br><br><br>1. The system automatically escalates the secondary node with the shortest sync delay to be the new primary node.<br><br>2. A new node is created to replace the failed node and complete data synchronization with the new primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After the primary node switch is completed, it is not necessary to modify the client address code.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Due to the asynchronous implementation of data synchronization between primary and secondary nodes, some recently written data on the primary node may be lost.</div><br> |
   |The failure affects the primary node and some secondary nodes |When the primary node and some secondary nodes fail:<br><br><br>1. The system automatically escalates the secondary node with the shortest sync delay to be the new primary node.<br><br>2. A corresponding number of new nodes is created to complete data synchronization with the new primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After the primary node switch is completed, it is not necessary to modify the client address code.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Due to the asynchronous implementation of data synchronization between primary and secondary nodes, some recently written data on the primary node may be lost.</div><br> |
   |The failure affects the primary node and all secondary nodes |When all nodes in the instance fail:<br><br><br>1. The system automatically creates the same number of primary and secondary nodes as the source instance.<br><br>2. The new primary and secondary nodes will replace the failed nodes playing the related roles. After the replacement is complete, all nodes will be cold started.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When all nodes fail, data that has not yet been written to the cloud disk will be lost.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the nodes are restored, it is not necessary to modify the client address code.</div><br> |
   


<span id=".5YiH5o2i5b2x5ZON5Y-K5bu66K6u"></span>
## Failover impact and suggestions


* **Failover impact**

   * The node being switched has a temporary disconnection of a few seconds.

   * The node being switched may be not writable briefly (less than 30 seconds), which aims to avoid potential data loss risks caused by failover and data double\-write caused by the DNS cache.

   * Pub/Sub does not support data persistence, and there may be a risk of data loss for data in the subscription buffer during failover.

* **Suggestions**

   Your application should have an automatic reconnection mechanism and the ability to handle exceptions. If not, the application will prompt an exception message during the failover of an instance, such as `READONLY You can't write against a read only replica`.


<span id="7ynmBqQz"></span>
## Relevant APIs


|API |Description |
|---|---|
|[SwitchOver](https://docs.byteplus.com/en/docs/redis/switchover) |Call the SwitchOver API to perform primary\-secondary node switchover for a specified instance. |
|[TestShutDownDBInstanceNodes](https://docs.byteplus.com/en/docs/redis/testshutdowndbinstancenodes) |Call the TestFailoverDBInstanceZone API to simulate an availability zone\-level failover for the target Redis instance. |
