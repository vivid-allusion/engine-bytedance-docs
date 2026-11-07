---
title: "How do I resolve the issue where the ext4 file system of a GPT partition cannot exceed 16 TiB when I resize the file system with resize2fs in Ubuntu 16.04?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/GPT_partition_cannot_exceed_16TiB"
---

## Problem description

After I expand the data volume of an instance running Ubuntu 16.04, the following error occurs when I use the resize2fs tool to expand the ext4 file system of its GPT partition to more than 16 TiB.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_40c834765b8b9b08e6ffed8ed6c0a48a.png)

## Causes

This issue arises because the built\-in resize2fs tool in the Ubuntu 16.04 operating system is outdated. It does not support operations on file systems larger than 16 TiB.

## Solutions

You need to upgrade the resize2fs tool to a version not lower than 1.43.0.

1. You can download the resize2fs source code (version 1.43.0 or later) from the [SOURCEFORGE](https://sourceforge.net/projects/e2fsprogs/files/e2fsprogs/) website and [upload the file to the target instance](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   > In the example provided in this topic, version 1.47.1 is downloaded.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f4d25188bd80c440c5da1cd58d987bd.png)

2. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

3. In the directory where the e2fsprogs file is located, execute the following command to decompress the file.

   ```Plain Text
   tar -zxvf e2fsprogs-1.47.1.tar.gz
   ```

4. Execute the following command to enter the e2fsprogs directory.

   ```Plain Text
   cd e2fsprogs-1.47.1/
   ```

   > **tip**

   > Replace `e2fsprogs-1.47.1` with the actual directory name.

5. Execute the following command to generate the Makefile.

   ```Plain Text
   ./configure
   ```

6. After you complete the previous compilation, compile the e2fsprogs source code and install the new version of the resize2fs tool.

   ```Plain Text
   make && make install
   ```

7. Execute the following command to view the version of the resize2fs tool.

   ```Plain Text
   resize2fs 2>&1 | head -n 1
   ```

   Sample output:

   If the following output is displayed, version 1.47.1 of the resize2fs tool is installed as expected.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ef3088c944f29b0b211d5ba5aafcfdb.png)

8. Execute the following command to convert the file system to 64\-bit format.

   ```Plain Text
   resize2fs -b /dev/vdb1
   ```

   > **tip**

   > Replace `/dev/vdb1` with the actual partition to be expanded.

   Sample output:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_577e08b7991a7fe4ab4d143860a90d55.png)

9. Execute the following command to expand the file system.

   ```Plain Text
   resize2fs /dev/vdb1
   ```

   > **tip**

   > Replace `/dev/vdb1` with the actual partition to be expanded.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6359c65eaf32d7c23f7c0299572f407f.png)
