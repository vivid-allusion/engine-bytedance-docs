---
title: "How to resolve the issue that the kworker hangs when it detaches a disk device from a Linux ECS instance?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve-kworker-hangs"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description​

In an instance using a Linux image (such as CentOS Stream 9), the kworker thread hangs when a disk device is unplugged.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

This issue is caused by a bug in Kernel block layer. The bug has been fixed in the latest Linux Kernel versions. For details, refer to:


* [block: drain file system I/O on del_gendisk](https://github.com/torvalds/linux/commit/8e141f9)

* [block: simplify disk shutdown](https://github.com/torvalds/linux/commit/6f8191f)


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


* If your image version is an EOL platform version, replace the operating system by following the [OS replacement](https://docs.byteplus.com/en/docs/ecs/Changing-OS) guide, or fix this issue via hot patch.

* If your image version is not an EOL platform version, monitor the progress of its backports for fixes, such as [Linux Backports](https://backports.wiki.kernel.org/index.php/Main_Page), [Debian Backports](https://backports.debian.org/Instructions/), and [Ubuntu Backports](https://help.ubuntu.com/community/UbuntuBackports).
