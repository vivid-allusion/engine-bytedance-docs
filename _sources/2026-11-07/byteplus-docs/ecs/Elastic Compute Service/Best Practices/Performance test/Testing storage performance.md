---
title: "Testing storage performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-storage-performance"
---

This topic describes how to use Flexible I/O Tester (FIO) to test the storage performance of Linux instances, including I/O latency, IOPS, and bandwidth.

## Background

We recommend that you use FIO to test the I/O latency of block storage. FIO is an I/O tool used for stress\-testing and verifying hardware. It is highly recommended for testing disk performance on Linux.

FIO can run in two modes. In this topic, the fio jobfile is used to run FIO, with a job file that defines the I/O load during simulations. One job file can create multiple threads and files. A classic job file includes a global section that defines shared parameters, and one or more job sections that describe the jobs involved.

## Prerequisite

You have mounted the volume to be tested on an instance.

> **warning**

* > We strongly recommend that you do not use the system volume, where the operating system is installed, or a data volume that contains data as the test object. Running FIO stress tests directly on volumes with partitions, file systems, or other data may lead to file system exceptions and data loss.

* > We recommend that you test volume performance by using tools on a newly created empty data volume. If you need to perform tests on a volume that stores business data, proceed as follows:

   * > Before the test begins, [back up the data on the volume](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) to prevent data loss.

   * > In the test command, specify the `filename` argument to a specific file rather than the entire disk device, `For example, -filename=/data/fiotest`.

## Procedure

> **tip**

> This topic describes how to test volume performance. In the example provided in this topic, we specify the `filename` argument to a specific file.

1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the installation package from [the official FIO website](https://sourceforge.net/projects/fio/), and transfer it to the instance. To upload data, refer to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

   1. Execute the following command to decompress the installation package.

      ```Bash
      tar -zxvf fio-*.tar.gz
      ```

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

   ```Bash
   fdisk -lu
   ```

   If the returned "Start" value is divisible by 8, the volume is 4 KiB\-aligned.

4. Create a test file and mount it.

   1. Execute the following commands in sequence to create the data directory and mount the disk device to this directory.

      ```Bash
      mkdir /data
      mount /dev/vdb /data
      ```

   2. Create the fiotest file in the data directory.

      ```Bash
      vim /data/fiotest
      ```

      Press `Esc` to exit insert mode, then input `:wq` and press Enter to save and exit the vim editor.

5. Run performance testing commands. For details, refer to [Sample testing commands](https://docs.byteplus.com/en/docs/ecs/Testing-storage-performance#EBKAQZ3M).

## Test command examples

### Test I/O latency performance

**Test random read I/O latency**

Create the file "job_file" to test the random read I/O latency. The file content is as follows. After creation, execute the `fio job_file` command to view the test results.

```Plain Text
[global]
ioengine=libaio
userspace_reap
runtime=60
direct=1
group_reporting
randrepeat=0
norandommap
ramp_time=6
iodepth=1
numjobs=1
exitall
[randread4k]
filename=/data/fiotest
rw=randread
bs=4K
size=10G
```

####

**Test random write I/O latency**

Create the file "job_file" to test the random write I/O latency. The file content is as follows. After creation, execute the `fio job_file` command to view the test results.

```Plain Text
[global]
ioengine=libaio
userspace_reap
time_based
runtime=60
direct=1
group_reporting
randrepeat=0
norandommap
ramp_time=6
iodepth=1
numjobs=1
exitall
[randwrite4k]
filename=/data/fiotest
rw=randwrite
bs=4K
size=10G
```

### Test the IOPS performance

**Test random read IOPS**

Create the file "job_file" to test the random read IOPS. The file content is as follows. After creation, execute the `fio job_file` command to view the test results.

```Plain Text
[global]
ioengine=libaio
userspace_reap
time_based
runtime=60
direct=1
group_reporting
randrepeat=0
norandommap
ramp_time=6
iodepth=128
numjobs=8
exitall
[randread4k]
filename=/data/fiotest
rw=randread
bs=4k
size=10G
```

####

**Test random write IOPS**

Create the file "job_file" to test the random write IOPS. The file content is as follows. After creation, execute the `fio job_file` command to view the test results.

```Plain Text
[global]
ioengine=libaio
userspace_reap
time_based
runtime=60
direct=1
group_reporting
randrepeat=0
norandommap
ramp_time=6
iodepth=128
numjobs=8
exitall
[randwrite4k]
filename=/data/fiotest
rw=randwrite
bs=4k
size=10G
```

### Test the bandwidth

We recommend executing the dd command to test the bandwidth performance of block storage. You can execute the dd command to read data from standard input or a file, convert the data based on a specified format, and then write the output to a file or device. You can calculate the storage bandwidth from the data transfer time.

**Test sequential read bandwidth**

Execute the following command:

```Bash
dd if=/data/fiotest of=/dev/null bs=16M count=1024 iflag=direct
```

**Test sequential write bandwidth**

Execute the following command:

```Bash
dd if=/dev/zero of=/data/fiotest bs=16M count=1024 oflag=direct
```

## Parameter description

**FIO parameter descriptions**

|Parameter​ |Description |
|---|---|
|[global] |Indicates job name. The global section name can not be modified. It describes the default configuration values for each job in the job file. |
|ioengine=libaio |Specifies the I/O engine (synchronous and asynchronous I/O are supported) for FIO. Here, we recommend using libaio (asynchronous I/O), which submits a batch of I/O requests at once, waits for the batch to complete, and then submits the next. This reduces interaction overhead and improves efficiency. |
|userspace_reap |Used with libaio to improve the completion speed of asynchronous I/O. |
|time_based |Indicates that read/write operations repeat until the time is reached, if the file is fully read/written before the time specified by the runtime expires. |
|runtime=60 |Specifies the time (in seconds) after which the process stops. 60s is recommended. |
|direct=1 |Whether to use direct I/O. Values:<br><br><br>* 1 (default): Enables direct I/O. This allows operations to bypass I/O caching and write data directly.<br><br>* 0: Disables direct I/O. |
|group_reporting |Displays the aggregate result of information (of each thread/process). |
|randrepeat=0 |Whether the random sequence is repeatable. Values:<br><br><br>* True (1): Indicates that the random sequence is repeatable.<br><br>* False (0): Indicates that the random sequence is not repeatable. We recommend that this be set to 0. |
|norandommap |Typically, for random I/O operations, FIO covers every block of the file. That is, FIO uses a section of memory to record whether a random position is repeated. If the position is repeated, FIO then finds another position not repeated. If this parameter is configured, FIO does not query historical data, which achieves truly random read and write operations. |
|ramp_time=6 |Used to specify the ramp\-up time at the start of testing. It is recommended to set it to 6, which means waiting 6 seconds for the performance to stabilize before recording log data. This reduces the amount of time for generating a valid result. |
|iodepth=1 |Specifies I/O queue depth. This represents the maximum simultaneous I/O operations for asynchronous I/O. |
|numjobs=1 |Recommended value: CPU core number. For example, if the ECS instance has eight CPU cores, the recommended value for numjobs is 8. |
|exitall |Indicates that after one job is completed, all jobs will be stopped. |
|[randread4k], [randwrite4k] |Used to specifically define the relevant configuration for the testing task.<br><br><br>* [randread4k]: Represents a random read test on the disk with a data block size of 4K.<br><br>* [randwrite4k]: Represents a random write test on the disk with a data block size of 4K. |
|filename=/data/fiotest |The path of the file to be tested. If it is a whole disk test, use the disk device name. |
|rw |The read and write policy during testing.<br><br><br>* randread: Random read.<br><br>* randwrite: Random write. |
|bs=4k |Indicates block size (I/O unit). Default value: 4 KiB.<br><br>Read and write block sizes can be specified separately with the "read" and "write" parameters. Either parameter can be left empty to retain its default value. |
|size=10G |Indicates the size of the test file. FIO completes reading/writing the entire specified file size before stopping the test, unless disrupted by other configurations (such as the parameter "runtime").<br><br>This argument can be a unit\-suffixed number, for example, size=10G represents a read/write data volume of 10 GiB, or a percentage, for example, size=20%, where FIO uses 20% of the total space of the given file or device. If this argument is not specified, FIO will use the full size of the given file or device. |

**dd command arguments Description**

|Parameter​ |Description |
|---|---|
|if=/dev/zero |Specifies the source file from which data is read. "if=/dev/zero" indicates testing pure write performance. |
|of=/dev/null |Specifies the file to which the converted data is written. "of=/dev/null" indicates testing pure read performance. |
|bs=16M |Sets the size of a read/write block to bytes. |
|count=1024 |Indicates copying only 1024 blocks. The block size equals the byte value specified by bs. |
|iflag=direct |Indicates direct I/O for reading data. |
|oflag=direct |Indicates direct I/O for writing data. |
