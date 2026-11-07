---
title: "Best practices for optimizing performance"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Performance-optimization-plan"
---

This topic describes how to achieve high performance for applications with TOS implementations.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

TOS is a distributed object storage product designed for scenarios involving massive data. To provide high service capabilities to applications, TOS offers linear performance scaling and dynamic data load balancing. Internal indexes are partitioned based on the UTF\-8 encoding range of **bucket name + object name**. In sequential read\-write mode, TOS limits QPS to 2000 per second. For more information about TOS constraints, see [constraints](https://docs.byteplus.com/docs/tos/docs-restrictions).

If you use sequential prefixes (such as prefixes in time or alphabetical order) to name objects in a bucket, many object access requests may be sent to a particular partition, leading to partition access hotspots. The service capacity of hotspot partitions is limited by the read\-write upper bounds of storage media, which may cause request rates to drop. You can refer to the methods listed below to optimize program performance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Whether reading or writing objects, performance optimization occurs gradually rather than immediately. After you optimize sequential prefixes, you may still encounter some errors; these errors will disappear once optimization is complete.</div>


<span id=".5LyY5YyW5pa55byP"></span>
## Optimization methods

To prevent these issues from affecting your application's normal operation, we recommend considering the following optimizations during the application design phase:


* [Hotspots caused by adjacent objects](https://docs.byteplus.com/docs/tos/Performance-optimization-plan#.55u46YK75a-56LGh6YCg5oiQ55qE6K6_6Zeu54Ot54K5)

* [Hotspots caused by the same object](https://docs.byteplus.com/docs/tos/Performance-optimization-plan#.55u45ZCM5a-56LGh6YCg5oiQ55qE6K6_6Zeu54Ot54K5)

* [TOS traffic throttling triggered frequently by the business](https://docs.byteplus.com/docs/tos/Performance-optimization-plan#.5Lia5Yqh6aKR57mB6Kem5Y-RLXRvcy3mtYHmjqc=)

* [Adjustment of server-side traffic throttling of TOS](https://docs.byteplus.com/docs/tos/Performance-optimization-plan#.6LCD5pW0LXRvcy3nmoTmnI3liqHnq6_mtYHmjqfpmZDliLY=)


<span id=".55u46YK75a-56LGh6YCg5oiQ55qE6K6_6Zeu54Ot54K5"></span>
### Hotspots caused by adjacent objects


* Write data from different businesses to different buckets.

   ```json
   bucket:log
   object:
   20220610-001.log.tar.gz
   20220610-002.log.tar.gz
   20220610-003.log.tar.gz
   ...... 20220610-0xx.log.tar.gz
   ```
   

   ```json
   bucket:meta
   object:
   20220610-001.log.meta
   20220610-002.log.meta
   20220610-003.log.meta
   ...... 20220610-0xx.log.meta
   ```
   

* Distribute object names or prefixes in the same bucket

   If a bucket still has massive sequential objects, name them in the following ways to distribute object names or prefixes.

   * Add a random prefix. For example, calculate the hash value of the object name and use 2–10 digits as the object prefix.

      ```json
      //original
      20220610-001.log.tar.gz//sha256:fa473ff003b91aa20239e20e41... 20220610-002.log.tar.gz//sha256:dba85a4f69850bd8b7ba6fbe79... 20220610-003.log.tar.gz//sha256:bd6665a44717e3bda18d12ea51...
      ...... 20220610-0xx.log.tar.gz//sha256:a70364eaa3ce1b037c5707b06e... //After splitting\nfa473f-20220610-001.log.tar.gz\ndba85a-20220610-002.log.tar.gz\nbd6665-20220610-003.log.tar.gz\n...... a70364-20220610-0xx.log.tar.gz
      ```
      

   * Reverse the sequential object prefix. For example, reverse the date in the object name.

      ```javascript
      //Original\n20220610-001.log.tar.gz\n20220610-002.log.tar.gz\n20220610-003.log.tar.gz\n...... 20220610-0xx.log.tar.gz\n//After reversing\n100-01602202.log.tar.gz\n200-01602202\n300-01602202\n...... 1xx-01602202
      ```
      


<span id=".55u45ZCM5a-56LGh6YCg5oiQ55qE6K6_6Zeu54Ot54K5"></span>
### Hotspots caused by the same object

If your application sends many requests to the same object concurrently, the access speed will be subject to the TOS bandwidth and region restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. 

<span id=".5Lia5Yqh6aKR57mB6Kem5Y-RLXRvcy3mtYHmjqc="></span>
### TOS traffic throttling triggered frequently by the business

TOS adopts server\-side traffic throttling so that all users can have a positive experience. For detailed traffic throttling rules, please refer to [constraint limits](https://docs.byteplus.com/docs/tos/docs-restrictions). TOS traffic throttling is as follows:


* List actions: TOS is a key\-value\-based storage service and provides list APIs for better O&M. However, we recommend that you not rely heavily on these APIs in your application. Particularly in scenarios involving frequent writes and paginated listing, your application will not be able to detect newly written or deleted objects from the previous page in real time, potentially leading to errors.

* Reads and writes: If TOS traffic throttling is triggered frequently even if the above optimizations are made for hotspot prevention, we recommend that you implement peak staggering for your application.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When TOS traffic throttling is triggered, TOS explicitly responds with a 429 status code. It is recommended that your application actively performs throttling on TOS traffic control. For methods of throttling, see the <a href="https://docs.byteplus.com/docs/tos/SDK-overview">SDK documentation</a>.</div>


<span id=".6LCD5pW0LXRvcy3nmoTmnI3liqHnq6_mtYHmjqfpmZDliLY="></span>
### Adjustment of server\-side traffic throttling of TOS

If the performance of your application is still unsatisfying after the above optimizations, You can [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to request an increase in the throttling limit.
