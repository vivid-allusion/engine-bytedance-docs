---
title: "FAQs"
product: "Machine Learning Platform"
product_code: "mlp"
section: "Document"
source: "https://docs.byteplus.com/en/docs/mlp/FAQs"
---

<span id="开发机"></span>
# Development machine

<span id="q：基于开发机构建镜像时，开发机可以高频操作吗"></span>
## Q: When building an image based on a development machine, can the development machine be operated frequently?

A: During the process of building an image based on a development machine, do not perform any operations on the development machine, including but not limited to shutting down, restarting, and reading/writing data in the container, etc. Otherwise, image building will fail.

<span id="q：基于开发机构建镜像失败"></span>
## Q: Image building based on a development machine failed

A: The following are some error messages that cause failures and corresponding solutions for reference.


* **`BUILD\_FAILED\_NO\_SPACE`**

   Insufficient space on the development machine. Expand or clean up space and try again.

* **`CR\_BUILD\_FAILED\_SHUTDOWN`**

   Build failed. You may have turned off the development machine or performed data writing. During image building, ensure the development machine is in running state and do not perform write operations.

* **`BASIC\_CR\_BUILD\_FAILED\_TOO\_LARGE`**

   Build failed. You may be using the CR Trial Edition image repository, which limits the single\-layer data size of images to no more than 10GiB. You can save the image **to the Standard Edition image repository**, or **exclude unnecessary files or directories** when saving, such as temporary data files, checkpoints, etc. For more restrictions of the Trial Edition image repository, see [Image Repository Usage Restrictions](https://docs.byteplus.com/en/docs/cr/limits).

* **`BASIC\_CR\_PUSH\_FAILED\_TOO\_LARGE`**

   Push failed. You may be using the CR Trial Edition image repository, which limits the single\-layer data size of images to no more than 10GiB. You can save the image to the Standard Edition image repository, or exclude unnecessary files or directories when saving, such as temporary data files, checkpoints, etc.

* **`BASIC\_CR\_PUSH\_FAILED\_TOO\_MANY\_REQUEST`**

   Push failed. You may be using the CR trial version image repository, which limits the number of concurrent image requests to no more than 20. Select a standard namespace to save the image.


<span id="volc-命令行"></span>
# volc command line

<span id="q：提交任务进度条显示完成之后还会卡很久"></span>
## Q: After the submit task progress bar shows completion, it still freezes for a long time

A: The current submit task may contain large files (such as logs, model files, etc.) and requires patience to wait. Or host the model files on shared storage (e.g., vePFS, TOS).

<span id="q：提交任务能否忽略掉一些文件不上传"></span>
## Q: Can some files be ignored and not uploaded when submitting a task

A: Supports configuring `.gitignore` in the upload directory; the volc tool will ignore the corresponding files according to the configuration.

<span id="q：volc-如何升级"></span>
## Q: How to upgrade volc

A: You can use the following two methods to upgrade; for details, see [User Documentation](https://docs.byteplus.com/docs/mlp/54967).

Method 1: `volc upgrade`.

Method 2:

```shell
sh -c "$(curl -fsSL https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/cli-binary/install.sh)"  && export PATH=$HOME/.volc/bin:$PATH
```


<span id="q：开发机未开启公网配置，怎么通过-volc-上传代码至-tos"></span>
## Q: The development machine has not turned on public network configuration; how to upload code to TOS via volc

A: First, add configuration in `.volc/config` as follows:

```shell
[ml_platform]
private = True
```


After configuration is completed, complete the upload via the `submit` or `upload` command. See [User Documentation](https://docs.byteplus.com/docs/mlp/54967) for details.

<span id="tos（对象存储）"></span>
# TOS (Object Storage)

<span id="q：logging-打印日志出现错误"></span>
## Q: logging encounters an error when printing logs

A: Mounting TOS via CloudFS does not support append mode for writing, so logging will report an error. The solution is to reopen a log file for each task and simply write logs to this new file. It is recommended to use time as the suffix for log files.

<span id="q：ls-rm-文件夹出现出现-“no-buffer-space-available”"></span>
## Q: Encountering "No buffer space available" when using ls/rm on a folder

A: In the development machine scenario, users use ls/rm frequently. For large folders (directories containing a large number of small files), operations like ls need to pull a large amount of metadata. This puts significant pressure on the system, causing the WebIDE of the development machine to freeze. To maintain system stability, operations like ls on large folders are restricted. The above error occurs when exceeding `10000`.

<span id="q：如何访问-tos-并进行文件操作"></span>
## Q: How to access TOS and perform file actions

A: View the official TOS Documentation [Access TOS using Rclone](https://docs.byteplus.com/en/docs/tos/docs-accessing-tos-with-rclone).

<span id="q：程序往-tos-写报错-“input-output-error”"></span>
## Q: Program writing to TOS errors with "Input/output error"

A: 1. Need to confirm the opening method. 2. If multiple machines/cards write to the same file simultaneously, multi\-process security cannot be ensured. Currently, writing the same file is simulated by CloudFS fuse via the rm and write method. If the business side cannot ensure multi\-process safety, the file written by process A may be deleted by process B, resulting in an "Input/output error".

<span id="q：挂载-tos-不支持的操作"></span>
## Q: Unsupported actions for mounting TOS

A：chmod、ln、chown、tuncate。

<span id="q：挂载-tos-后异常退出"></span>
## Q: Abnormal exit after mounting TOS

A: Mounting TOS has certain resource requirements. It is recommended to ensure at least 8GiB of container memory (some resources will be used for file caching services to improve training efficiency), and the prompt information for this part is also being continuously optimized.

<span id="q：挂载了-tos-的任务成功拉起之后需要过段时间才能看到挂载的文件内容"></span>
## Q: After a task with mounted TOS is successfully started, it takes some time to see the mounted file content

A: The invisibility time is related to the specifications of the mount task. High\-spec containers load faster, resulting in shorter invisibility time. If the specifications cannot be changed, adjustments can be made via the SideCarMemoryRatio (0.05 ~ 0.5) parameter. For details, refer to [User Documentation](https://docs.byteplus.com/docs/mlp/54967)

<span id="q：训练任务第一个-epoch-训练慢"></span>
## Q: Slow training in the first epoch of a training task

A: When training a model by mounting TOS, the training data for the first epoch needs to be pulled from remote TOS to the local CloudFS. Starting from the second epoch, all data requests can be obtained through the local CloudFS, which will provide a certain acceleration effect.

<span id="q：在-tos-中创建存储桶（bucket）代码报错-you-have-attempted-to-create-more-buckets-than-allowed"></span>
## Q: When creating a bucket in TOS, the code reports an error: "You have attempted to create more buckets than allowed."

A: This error occurs when the number of buckets under the current account exceeds 99. At this time, you can enter rclone lsd: in the command line to view the list of buckets under the current account. Then enter rclone purge:to delete unused buckets, then recreate the bucket to succeed.

 &nbsp;

<span id="vepfs-parallel-file-system"></span>
# vePFS (Parallel File System)

<span id="q：观察到的网络带宽比真实的业务侧有效带宽要大很多"></span>
## Q: The observed network bandwidth is much larger than the actual effective bandwidth on the business side.

A: It may be read amplification caused by vePFS prefetching, which needs to be analyzed in detail in combination with the business. A common scenario is opening files via mmap; the default prefetch mechanism causes read amplification, and in random access mode, this prefetching does not help business performance and needs to be turned off.

<span id="q：mmap-性能不及预期，没有云盘性能好"></span>
## Q: mmap performance is not as expected and is not as good as cloud disk performance.

A: vePFS has poor support for mmap read methods. Recommend the business side to switch to small file methods or other packaging methods (e.g., tfrecord, webdataset). Also check if the business side opens files in read\-write mode; opening in `r+/w` mode causes vePFS to enable read\-write locks for resource access, resulting in low performance. During training, open files in read\-only mode as much as possible.

<span id="q：使用-dali-加速效果不佳"></span>
## Q: Poor acceleration performance when using DALI

A: DALI uses the mmap feature; try using dont_use_mmap to turn off mmap.
