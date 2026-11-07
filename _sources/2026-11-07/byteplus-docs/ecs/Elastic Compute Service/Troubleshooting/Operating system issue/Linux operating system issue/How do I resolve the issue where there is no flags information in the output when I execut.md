---
title: "How do I resolve the issue where there is no flags information in the output when I execute the lscpu command in CentOS 7?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve-no-flag-information-displayed"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

When the `lscpu` command is executed on an instance running the CentOS 7 operating system, the output does not include the flags parameter and its corresponding information.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc076b173a59e7db40b5b9a9d01c046e.png) </span>

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

In some CentOS 7 versions (such as CentOS 7.1 to 7.3), the version of util\-linux is too old to display CPU flags information.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

<span id=".5pa55qGI5LiA77ya5Y2H57qndXRpbC1saW51eA=="></span>
### Solution 1: Upgrade util\-linux

You can execute the following command in the affected instance to upgrade util\-linux.

```Plain Text
yum makecache && yum install util-linux
```


<span id=".5pa55qGI5LqM77ya5pu05o2i5pON5L2c57O757uf"></span>
### Solution 2: Change the operating system

The `lscpu` command in CentOS 7 supports the display of CPU flags information only when the version of util\-linux is 2.23.2\-43 or higher. You can refer to the following table to change the operating system of the instance to a newer version. For more information, see [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS).

util\-linux versions in different CentOS 7 releases.


|Operating system version |util\-linux version |
|---|---|
|CentOS 7.9 |2.23.2\-65.el7_9.1 |
|CentOS 7.8 |2.23.2\-63.el7 |
|CentOS 7.7 |2.23.2\-61.el7_7.1 |
|CentOS 7.6 |2.23.2\-59.el7_6.1 |
|CentOS 7.5 |2.23.2\-52.el7_5.1 |
|CentOS 7.4 |2.23.2\-43.el7_4.2 |
|CentOS 7.3 |2.23.2\-33.el7_3.2 |
|CentOS 7.2 |2.23.2\-26.el7_2.3 |
|CentOS 7.1 |2.23.2\-22.el7_1.1 |


<span id=".5pa55qGI5LiJ77ya5p-l55yLL3Byb2MvY3B1aW5mb-iOt-WPlkNQVSBmbGFnc-S_oeaBrw=="></span>
### Method 3: View /proc/cpuinfo to obtain CPU flags information

You can execute the following command on the instance where the issue occurs to view the /proc/cpuinfo file and obtain CPU flags information.

```Plain Text
cat /proc/cpuinfo | head -50
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70d6532af31e683fd464d1f4dd441f55.png) </span>
