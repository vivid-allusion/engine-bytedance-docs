---
title: "Expanding file systems FAQ"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Expanding-file-systems-FAQ"
---

This topic introduces common issues you may encounter when expanding a file system for your reference.

<span id="扩容文件系统时操作失败或卡住怎么办？"></span>
### What should I do if the operation of expanding the file system fails or gets stuck?

When the file system is at a high water level, there may be a high degree of file fragmentation and slow disk addressing, which may result in performance degradation of the file system. It is recommended to plan for capacity expansion before the file system reaches 90%. If you encounter a failure or freeze during the expansion operation, it may be due to a high file system utilization. It is recommended to delete some data first, and then re\-upload after a successful expansion. For more detailed information on capacity expansion, please refer to [Expanding a file system](https://docs.byteplus.com/docs/pfs/Expanding-a-file-system).
