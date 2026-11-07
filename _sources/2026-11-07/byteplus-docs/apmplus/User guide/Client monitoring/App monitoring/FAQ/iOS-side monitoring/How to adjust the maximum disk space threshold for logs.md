---
title: "How to adjust the maximum disk space threshold for logs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_adjust_the_maximum_disk_space_threshold_for_logs"
---

The algorithm used by MemoryGraph to determine whether the SDK module's own memory usage exceeds the threshold is as follows: When the upper limit for its own memory usage is set to 100 MB, if the number of memory nodes exceeds between 2.6 million and 2.7 million (with some fluctuation), a downgrade will be triggered. As the memory usage upper limit increases, the threshold for the number of memory nodes that triggers a downgrade also increases proportionally. The threshold should not be set too high; otherwise, when the APP's available memory falls below the threshold, a downgrade will be triggered. It is recommended to set the configuration threshold to 100 MB to 200 MB. If there are a large number of nodes, you can lower the memory collection start threshold to reduce the number of nodes being collected and thereby avoid degradation.
