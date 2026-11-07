---
title: "Recommendations for accessing symlinks in Linux"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Recommendations-for-accessing-symlinks-in-linux"
---

This topic explains the implementation mechanisms and usage recommendations for TOS symlinks in Linux systems, to help you correctly access and use TOS symlinks in Linux.

<span id="d9e3f6d4"></span>
## Implementation mechanism

After a bucket is mounted on a Linux system using FSX, the system may not be able to resolve the target object path of a symlink in the bucket, because the TOS console and standard file systems handle symlinks differently. The following explains the implementation mechanisms for symlinks in the TOS console, TOS APIs, and standard file systems:


* In a standard Linux file system, resolving a path when accessing a symlink works as follows:

   * For absolute paths, the system starts at the root directory (`/`) and resolves the path step by step through directory lookups until reaching the final target object.

   * For relative paths, the system uses the current working directory at the time the symlink was created as its base. The system then converts the relative path into an absolute path and continues the lookup based on this absolute path.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5ab9dea324d4743872454ed73cdc2e7~tplv-goo7wpa0wc-image.image) </span>

* For a symlink created via the TOS console, the target object path is relative to the bucket's root directory. Once the bucket containing the symlink is mounted on an ECS instance, the symlink appears as a symbolic link in the file system. At that point, the target object path is resolved as a file path relative to the mounted bucket's root directory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3026177114184355a91c0e4534c862b3~tplv-goo7wpa0wc-image.image) </span>

* TOS APIs allow for the creation of symlinks and support path referencing, similar to a standard file system. Once a bucket is mounted to an ECS instance, the target object path of a symlink created via a TOS API in the bucket is resolved as **a relative path starting from the directory where the symlink is located**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6947a959f7e1887319b057402366d9c7.png) </span>


<span id="G5ihacmc"></span>
## Recommendations

Standard file systems cannot resolve the target object paths of symlinks created via the TOS console. However, symlinks created via TOS APIs can be accessed normally. To use TOS symlinks in a Linux system, create them via a TOS API so that they can be recognized and resolved correctly. For instructions on how to create a symlink via a TOS API, see [PutSymlink](https://docs.byteplus.com/docs/tos/Putsymlink).

When using PutSymlink to create a symlink, set the `x-tos-symlink-target` parameter to the relative path of the object that the symlink points to in Linux. You can use Python to calculate the target object path for the` x-tos-symlink-target` parameter value. A sample is shown below:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you only mount a prefix of a bucket on an ECS instance, both the symlinks and their target objects must be located under that prefix. Otherwise, accessing the symlinks in Linux will fail.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a69395cc3dfed8c66fc08235de588020.png) </span>

&nbsp;

&nbsp;
