---
title: "Best practices for configuring PFS data flow directories"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Best_practices_for_configuring_vePFS_Data_Flow_directories"
---

This topic provides typical examples of directory configuration for creating Data Flow tasks.

<span id="22b3e204"></span>
## Import tasks

<span id="3e98d6ce"></span>
### Directory\-based Import


* Prerequisites:

   * The PFS file system is mounted at `/mnt/pfs` on client nodes.

   * Data Flow paths are configured as follows:

      * File System path: `/dataset`.

      * Object storage path: `/bucket/prefix`.

* File paths before and after Import:

   * TOS source path before Import:

      ```JSON
      /bucket/prefix/a/b/c/file-001
      ```
      

   * PFS destination path after Import:

      ```JSON
      /mnt/pfs/dataset/a/b/c/file-001
      ```
      


<span id="86ca5a77"></span>
### File list\-based Import


* Prerequisites:

   * The PFS file system is mounted at `/mnt/pfs` on client nodes.

   * Data Flow paths are configured as follows:

      * File System path: `/dataset`.

      * Object storage path: `/bucket/prefix`.

* File paths before and after Import:

   * TOS source path before Import:

      ```JSON
      /bucket/prefix/a/b/c/file-001
      /bucket/prefix/a/b/c/file-002
      /bucket/prefix/a/b/c/file-003
      ```
      

   * File list format for Import:

      ```JSON
      prefix/a/b/c/file-001
      prefix/a/b/c/file-002
      prefix/a/b/c/file-003
      ```
      

   * PFS destination path after Import:

      ```JSON
      /mnt/pfs/dataset/a/b/c/file-001
      /mnt/pfs/dataset/a/b/c/file-002
      /mnt/pfs/dataset/a/b/c/file-003
      ```
      


<span id="846e63c5"></span>
## Export tasks

<span id="55815552"></span>
### Directory\-based Export


* Prerequisites:

   * The PFS file system is mounted at `/mnt/pfs` on client nodes.

   * Data Flow paths are configured as follows:

      * File System path: `/dataset`.

      * Object storage path: `/bucket/prefix`.

* File paths before and after Export:

   * PFS source path before Export:

      ```JSON
      /mnt/pfs/dataset/a/b/c/file-001
      ```
      

   * TOS destination path after Export:

      ```JSON
      /bucket/prefix/a/b/c/file-001
      ```
      


<span id="109140dc"></span>
### File list\-based Export


* Prerequisites:

   * The PFS file system is mounted at `/mnt/pfs` on client nodes.

   * Data Flow paths are configured as follows:

      * File System path: `/dataset`.

      * Object storage path: `/bucket/prefix`.

* File paths before and after Export:

   * File list format for Export:

      ```JSON
      /dataset/a/b/c/file-001
      /dataset/a/b/c/file-002
      /dataset/a/b/c/file-003
      ```
      

   * TOS destination path after Export:

      ```JSON
      /bucket/prefix/a/b/c/file-001
      /bucket/prefix/a/b/c/file-002
      /bucket/prefix/a/b/c/file-003
      ```
      


<span id="OFqbMQjc"></span>
##
