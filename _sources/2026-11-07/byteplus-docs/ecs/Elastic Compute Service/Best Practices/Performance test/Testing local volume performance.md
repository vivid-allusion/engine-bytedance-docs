---
title: "Testing local volume performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-local-volume-performance"
---

This topic describes how to use the Flexible I/O Tester (FIO) tool to test the storage performance of local volumes on a Linux instance, including I/O ​latency, IOPS, and throughput.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

We recommend using FIO to test the local volume performance. FIO is an I/O tool used for stress\-testing and verifying hardware. It is highly recommended for testing local volume performance on the Linux platform.

FIO can run in two modes. In this topic, the fio jobfile is used to run FIO, with a job file that defines the I/O load during simulations. One job file can be used to create multiple threads and files. A classic job file includes a global section that defines shared parameters, and one or more job sections that describe the jobs involved.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created the Local SSD instance to be tested. To learn about local volumes and standard performance data, refer to [Local volume overview](https://docs.byteplus.com/en/docs/ecs/Local-volumes). To create an instance, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid data loss, we recommend running a performance test for local volumes on a newly created, data\-free instance.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the installation package from the [official FIO website](https://sourceforge.net/projects/fio/), and transfer it to the instance. To upload data, refer to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   1. Execute the following command to decompress the installation package.

      `tar -zxvf fio-*.tar.gz`

   2. Execute the following commands to install FIO.

      ```Plain Text
      cd fio-*
      ./configure
      make
      make install
      ```
      

   3. Execute the following commands in sequence to install libaio.

      ```Plain Text
      sudo yum -y install libaio
      sudo yum -y install libaio-devel
      ```
      

3. Execute the following command to check whether the storage device is 4 KiB\-aligned. If it is not 4 KiB\-aligned, the performance will be greatly affected.

   `fdisk -lu`

   If the returned "Start" value is divisible by 8, the storage device is 4 KiB\-aligned.

4. Execute the following command to switch the directory:

   `cd /tmp`

5. Execute the commands for testing local volume performance. For command examples, refer to [Test command examples](https://docs.byteplus.com/en/docs/ecs/Testing-local-volume-performance#.5rWL6K-V5ZG95Luk56S65L6L).

6. If the error "`NMI watchdog: BUG: soft lockup - xxx`" occurs during stress testing, follow the practice of [adjusting the use_threaded_interrupts parameter in Linux operating systems](https://docs.byteplus.com/en/docs/ecs/use_threaded_interrupts) to enable interrupt threading. This improves real\-time performance and responsiveness.


<span id=".5rWL6K-V5ZG95Luk56S65L6L"></span>
## Test command examples

The following test commands are applicable to NVMe SSD local volumes and SATA HDD local volumes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In this example, the device name used is /dev/your_device. Replace it with your actual device name. For example, if the local volume to be tested is /dev/vdb, replace /dev/your_device in the example commands below with /dev/vdb.</div>


* <div data-tips="true" data-tips-type="tip">The parameter values in the command examples are for reference only. Replace them based on your needs. For parameter descriptions, refer to <a href="https://docs.byteplus.com/en/docs/49/12819#.RklP5Y-C5pWw6K-05piO">FIO parameter descriptions</a>.</div>



<span id=".5rWL6K-VSU9QUw=="></span>
### Test IOPS


* **Random read**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=32 --rw=randread --ioengine=libaio --bs=4k --size=100% --numjobs=8 --runtime=600 --filename=/dev/your_device --name=test
   ```
   

* **Random write**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=32 --rw=randwrite --ioengine=libaio --bs=4k --size=100% --numjobs=8 --runtime=600 --filename=/dev/your_device --name=test
   ```
   


<span id=".5rWL6K-V5ZCe5ZCQ6YeP"></span>
### Test throughput


* **Sequential read**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=128 --rw=read --ioengine=libaio --bs=128k --size=100% --numjobs=1 --runtime=600 --filename=/dev/your_device --name=test
   ```
   

* **Sequential write**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=128 --rw=write --ioengine=libaio --bs=128k --size=100% --numjobs=1 --runtime=600 --filename=/dev/your_device --name=test
   ```
   


<span id=".5rWL6K-V6K6_6Zeu5pe25bu2"></span>
### Test access latency


* **Random read**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=1 --rw=randread --ioengine=libaio --bs=4k --size=100% --numjobs=1 --runtime=600 --filename=/dev/your_device --name=test
   ```
   

* **Random write**

   ```Plain Text
   fio --group_reporting=1 --direct=1 --iodepth=1 --rw=randwrite --ioengine=libaio --bs=4k --size=100% --numjobs=1 --runtime=600 --filename=/dev/your_device --name=test
   ```
   


<span id=".RklP5Y-C5pWw6K-05piO"></span>
## FIO parameter descriptions


|**Parameter​**  |**Description** |
|---|---|
|group_reporting |Indicates a display mode of test results.<br><br>If this parameter is specified, in the test results, aggregate statistics of each process are displayed, instead of grouped statistics by different tasks. |
|direct |Whether to use direct I/O. Values:<br><br><br>* 1 (default): Enables direct I/O. This allows operations to bypass I/O caching and write data directly.<br><br>* 0: Disables direct I/O. |
|iodepth |Indicates I/O queue depth during testing. For example, `-iodepth=128` means FIO controls a maximum of 128 I/O requests at a time. |
|rw |Indicates read/write policy during testing. Values:<br><br><br>* randwrite: Random write.<br><br>* randread: Random read.<br><br>* read: Sequential read.<br><br>* write: Sequential write.<br><br>* randrw: Mixed random read/write. |
|ioengine |Indicates the I/O engine for FIO testing. libaio is commonly used, as it better fits typical application scenarios. |
|bs |Indicates block size (I/O unit). Default value: 4 KiB.<br><br>Read and write values can be specified separately in read,write format. Either value can be left empty to retain its default value. |
|size |Indicates test file size. FIO completes reading/writing the entire specified file size before stopping the test, unless disrupted by other configurations (such as the parameter "runtime").<br><br>If this parameter is not specified, FIO uses the full size of the given file or device. You can also specify the size as a percentage (between 1 and 100). For example, size=20% means that FIO uses 20% of the full size of the given file or device. |
|numjobs |Indicates the number of concurrent threads for testing. Default value: 1. |
|runtime |Indicates test duration (how long FIO runs).<br><br>If the value of this parameter is not specified, FIO will continue reading/writing the file of the size specified by "size" above in blocks of the size specified by "bs" until completion. |
|filename |Indicates the path of the test target. You can specify the path as a storage device name or a file address. All FIO tests in this topic target entire volumes, which are raw volume tests that involve no file systems. To avoid accidentally testing other volumes (which may cause data loss), replace `/dev/your_device` (the example path in this topic) with your actual path. |
|name |Indicates test task name. Set a name for your test task as you wish. The task name in this example is `test`. |


For more information, refer to [FIO documents](https://fio.readthedocs.io/en/latest/index.html).
