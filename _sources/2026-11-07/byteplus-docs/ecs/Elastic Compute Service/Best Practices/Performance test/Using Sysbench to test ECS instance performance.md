---
title: "Using Sysbench to test ECS instance performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance"
---

This topic describes how to use Sysbench to test the load of the ECS instance CPU, memory, and FileIO.

[Sysbench](https://github.com/akopytov/sysbench) is a scriptable, multi\-threaded benchmarking tool based on LuaJIT. It is most commonly used for database benchmarking. Due to its simplicity and ease of use, it is also used to test non\-database workloads on instances. To use Sysbench in database tests, refer to [Using Sysbench to test MySQL application performance](https://docs.byteplus.com/en/docs/ecs/Testing-the-performance-of-MySQL-applications).

<span id=".5rWL6K-V546v5aKD"></span>
## Test environment

Create an instance that meets the following conditions. For more information, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


* Image: In the example provided in this topic, Ubuntu 22.04 is used.

* Storage: To test the maximum IOPS and bandwidth, configure the capacity of the volume mounted on the instance ≥ 1000 GiB.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The test environment and methods provided in this topic are for reference only and do not represent the actual optimal performance of the instance.</div>


<span id=".5a6J6KOFU3lzYmVuY2g="></span>
## Install Sysbench


1. [Log in to the ECS instance to be tested](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Install Sysbench as follows:

   * **Method 1: Software repository**

      CPU and memory tests involve only single\-machine operations. As a result, you only need to execute the following commands on the tested machine to quickly install Sysbench using the software repository for Linux operating systems.

      * Ubuntu/Debian

         ```Plain Text
         apt update && apt -y install sysbench
         ```
         

      * CentOS

         ```Plain Text
         yum -y install sysbench
         ```
         

   * **Method 2: Compile source code**

      If you need to compare performance across different operating systems, we recommend referring to the following content to install Sysbench by compiling the source code of the same version. This avoids inconsistencies caused by using different Sysbench versions installed from different software repositories.

      1. Execute the following commands to install the dependency packages.

         * Debian/Ubuntu

            ```Plain Text
            apt update
            apt -y install make automake libtool pkg-config libaio-dev
            ```
            

         * RHEL/CentOS

            ```Plain Text
            yum -y install make automake libtool pkgconfig libaio-devel
            ```
            

      2. (Optional) If you need a database test, execute the following commands to install the corresponding database.

         * Debian/Ubuntu

            ```Plain Text
            apt -y install libmysqlclient-dev libssl-dev   # Install MySQL
            apt -y install libpq-dev   # Install PostgreSQL
            ```
            

         * RHEL/CentOS

            ```Plain Text
            yum -y install mariadb-devel openssl-devel   # Install the MySQL database (replace it with mysql-devel in the RHEL/CentOS 5 system)
            yum -y install postgresql-devel          # Install the PostgreSQL database
            ```
            

      3. Execute the following commands in sequence to download the source code. In the example provided in this topic, version 1.0.20 is used.

         ```Plain Text
         wget -c https://codeload.github.com/akopytov/sysbench/zip/refs/tags/1.0.20 -O sysbench-1.0.20.zip
         unzip sysbench-1.0.20.zip
         cd sysbench-1.0.20
         ```
         

      4. Start compiling.

         ```Plain Text
         ./autogen.sh
         ./configure   # Enable MySQL by default. If there is no mysql library in the system, it needs to be changed to ./configure --without-mysql
         make -j 4
         make install
         ```
         

3. Verify the installation.

   Sysbench will be installed in the directory "/usr/local/bin/sysbench". You can execute the following command to check its version.

   ```Plain Text
   sysbench --version
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b99a78c0d5a3e9e44268ca7a906ebd6c.png) </span>


<span id=".6I635Y-WU3lzYmVuY2jluK7liqk="></span>
## Obtain Sysbench help

Execute the following command to view how to use Sysbench.

```Plain Text
sysbench  --help
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef0da4969352ef4372d17a47256ec9e5.png) </span>


|Parameter​ |Description |
|---|---|
|testname |Specifies the workload to be tested. Currently, supported workloads include fileio (disk I/O), cpu, memory, threads (threads), and mutex (mutex locks). |
|command |Includes common operation commands. Supported commands are prepare, run, cleanup, and help. The "run" command is used in most scenarios. |
|options |Determined by "testname" and mainly used to control the test parameters of the workload. |


To learn the test parameters for a specific workload to be tested, execute the command `sysbench [testname] help`. For example:


* Obtain test parameters of Memory:

   ```Plain Text
   sysbench memory help
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91e7767bbee0efc3275d2ff33694e25d.png) </span>

* Obtain test parameters of FileIO:

   ```Plain Text
   sysbench fileio help
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12280f4e3b47eafb4278206028241570.png) </span>


<span id=".5rWL6K-VQ1BV6LSf6L29"></span>
## Procedure


<Tabs>
<Tab zoneid="bRTBw6LIt4" title="Test CPU load">
<TabTitle>Test CPU load</TabTitle>

**Description**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to the methods provided in this topic, you can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/ECS-instance-performance-baseline-tests">Testing performance benchmark of ECS instances</a> to test CPU single\-core/multi\-core performance via UnixBench and calculate computation duration via SuperPI.</div>


Typically, a Sysbench test for CPU involves a large number of computing tasks being executed. To be more specific, you specify a value for the `--cpu-max-prime` parameter (default: 10000). Then, Sysbench defines "calculating all prime numbers (also called primes, which are numbers divisible only by 1 and themselves) in the range from 1 to this value" as one event. This allows you to learn CPU performance based on the number of events the CPU can compute per second.

**Procedure**


1. Execute the following commands to test the CPU single\-core or multi\-core performance.

   ```Plain Text
   # Result of testing single-core CPU
   sysbench cpu --cpu-max-prime=20000 --threads=1 --time=120  run
   # Result of testing multi-core CPU
   sysbench cpu --cpu-max-prime=20000 --threads=`nproc` --time=120  run
   ```
   

   
   |Parameter​ |Description |
   |---|---|
   |\-\-cpu\-max\-prime |Default value: 10000. This indicates that one event involves calculating all prime numbers up to 10000. |
   |\-\-threads |Indicate thread number. Default value: 1. The default value "1" indicates that Sysbench starts only 1 thread for prime number calculation. If other values are specified (representing the number of threads), Sysbench starts the corresponding number of threads and calculates prime numbers at the same time.<br><br>In the above multi\-core related commands, `nproc` is used to calculate the number of CPU cores in the test system. Then, the corresponding number of cores is specified for testing. |
   |\-\-time |Indicates test duration (unit: seconds). Default value: 10. This indicates that Sysbench calculates prime numbers repeatedly within 10 seconds, and each completed round is counted as one "event". |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">With Sysbench, you can also use the <code>--events</code> to specify the number of events to complete before the test stops. However, because this parameter is harder to set across different core counts, using the <code>--time</code> parameter is recommended.   </div>
   

2. Analyze test results.

   * Single\-core performance

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b55ee5588d4a60e3dc1bb429b89a13e.png) </span>

   * Multi\-core performance

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_00f2fb004cf0858abfaff92954556eda.png) </span>

   As shown in the picture above, the CPU metric of the Sysbench test is represented by the value of `events per second` (average number of events completed per second). The higher this value, the better the CPU computing performance.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Due to the event\-related configurations, outputs of different values of the \-\-cpu\-max\-prime parameter can not be compared with each other.   </div>
   


</Tab>
<Tab zoneid="IEYEyVeUW5" title="Test Memory load">
<TabTitle>Test Memory load</TabTitle>

**Description**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For memory performance testing, Sysbench is not the first choice. Refer to <a href="https://docs.byteplus.com/en/docs/ecs/ECS-instance-performance-baseline-tests">Testing performance benchmark of ECS instances</a> for testing bandwidth and latency via Stream and MLC, respectively.</div>


Testing memory performance via Sysbench mainly involves sequential or random read/write operations on blocks of different sizes. In memory performance testing, "events" refers to the reading or writing of one memory block.

For memory performance testing, Sysbench is more complex than Stream and MLC. It supports more parameters, and you need to configure the parameters correctly to obtain the expected performance results. Before testing, you can check the Memory test parameters of Sysbench. For details, see [Obtaining Sysbench help](https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance).

**Procedure**


1. Execute the following commands to test memory performance.

   ```Plain Text
   # Read operations on memory
   sysbench --memory-total-size=40000G --memory-block-size=512MB  --memory-scope=global --memory-oper=read  memory --threads=`nproc`  --time=120  run
   # Write operations on memory
   sysbench --memory-total-size=40000G --memory-block-size=512MB  --memory-scope=local  --memory-oper=write memory --threads=`nproc`  --time=120  run
   ```
   

   
   |Parameters |Description |
   |---|---|
   |\-\-memory\-total\-size |Indicates the total data transfer size. Specify the total amount of memory read/written by Sysbench before the test can stop. Default value: 100 G. In multi\-core scenarios, the default value may cause the test to stop in less than 1 second, thereby impacting accuracy. Therefore, a larger value is recommended. |
   |\-\-memory\-block\-size |Indicates memory block size. One read/write operation on a block counts as one "event". We recommend specifying a value larger than the CPU L3 Cache. For example, when the L3 Cache is 100 MB, the specified memory block size can be:<br><br><br>* For single\-threaded testing: Specify the value of block\-size as 128 MB.<br><br>* For multi\-threaded testing:<br><br>   * If memory\-scope=global, specify the value of block\-size as 128 MB.<br><br>   * If memory\-scope=local and threads=8, specify the value of block\-size to be more than 16 MB.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To check the L3 Cache capacity, execute the <code>lscpu</code> command.</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb0a1aa57aa450ae6f7448e84c1ea29d.png" width="300px" /></div><br> |
   |\-\-memory\-scope |Indicates memory access scope. Values:<br><br><br>* global (default): Whole block of the allocated memory<br><br>* local: Part of the allocated memory block<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For multi\-threaded stress testing, this parameter can be used to specify whether threads can access the whole block of the allocated memory or each thread accesses its own small memory block. To calculate the total allocated memory:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">memory\-scope=global: Total allocated memory = memory_block_size.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">memory\-scope=local: Total allocated memory = memory_block_size \* threads.</div><br> |
   |\-\-memory\-oper |Indicates memory operation type. Values:<br><br><br>* write (default)<br><br>* read<br><br>* none |
   |\-\-threads |Indicate thread number. Default value: 1. When the value is 1, Sysbench starts only one thread for testing. In the above commands, `nproc` is used to calculate the number of CPU cores in the test system. Then, the corresponding number of cores is specified for testing. |
   |\-\-time |Indicates test duration (unit: seconds). By default, Sysbench runs the test for 10 seconds. Memory tests of Sysbench can also stop earlier after writing operations specified by "total\-size" are completed. Since a large value is specified for "memory\-total\-size", the "time" parameter can be used here to specify the memory test duration. |
   

2. Analyze test results.

   * Read operations on memory

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66988e9ebb27a6ecaa11f80a9ac66393.png) </span>

   * Write operations on memory

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7cd9f42108cdafddf46bbd7929514cce.png) </span>

   As shown above, the memory performance metric tested via Sysbench is represented by `MiB/sec`, the average memory processed per second. You can also calculate the memory read/write bandwidth based on the total number of events and total completion time. For example, as shown in the result of testing write operations on memory, one event equals writing one block with a size of 512 MB (specified by block\-size), and 26,619 events were completed in 120.1638 seconds. This indicates a total of 26,619 \* 512 MB of memory was written. By dividing the total written memory by total completion time, you can learn the memory write bandwidth, which is 26,619 \* 512 MB / 120.1638 s = 113,418 MB/s.





</Tab>
<Tab zoneid="qBjcQlXSKr" title="Test FileIO load">
<TabTitle>Test FileIO load</TabTitle>

**Description**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For disk I/O testing, Sysbench is not the first choice. To test I/O latency, IOPS, and storage bandwidth via FIO, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Testing-storage-performance">Testing storage performance</a>.</div>


The principle of Sysbench FileIO tests is to create files and perform different read/write operations (via file\-test\-mode) on them. Supported operations include sequential write, sequential read, sequential read/write, random read, random write, and random read/write. The test involves three phases: preparation (prepare), execution (run), and cleanup (cleanup). In the preparation phase, data required for the test is created, and then deleted in the cleanup phase. Note that in these two phases, certain parameters in the prepare and cleanup commands are required to be configured consistently.

The key differences between FIO and Sysbench testing are as follows:


* For Sysbench testing, you need to mount the disk and change to that directory to run the test (that is, test read/write operations on files in the file system). FIO, by contrast, is more often used to test raw disks, so the results may differ.

* In Sysbench FileIO tests, pwrite/pread is used by default, which causes lower performance than that in FIO\-involved tests (where libaio is used as the backend). Therefore, you need to specify using libaio via parameters during testing.

* Sysbench calculates latency based on event statistics, and its statistical approach may differ from that of FIO. FIO is typically chosen for I/O latency testing, with iodepth set to 1, and it can provide latency data at the microsecond (USEC) level. Sysbench does not have the above capacities and, therefore, can not be used for testing I/O latency.


**Procedure**


1. (Optional) Prepare the volume.

   Sysbench does not support testing raw volumes directly. If you need to test a data volume mounted on an ECS instance, refer to the following content to mount the volume to a file system.

   > By default, when you create an ECS instance, a system volume is provided, partitioned, and formatted automatically. As a result, you do not need to partition or format the system volume.   
   

   * [Partitioning and formatting volumes (less than or equal to 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB)

   * [Partitioning and formatting volumes (larger than 2 TiB)](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB)

2. Prepare for the FileIO test.

   Execute the following command to enter the preparation phase (prepare). After completion, a test file will be added to the test directory, as shown below.

   ```Plain Text
   sysbench fileio --file-total-size=20G --file-num=1 prepare
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf1024427b7d76468b246348e7acecc7.png) </span>

3. Execute the following commands to test the IOPS and bandwidth of the volume.

   * Test the random write IOPS of the volume

      ```Plain Text
      sysbench fileio --file-total-size=20G --file-num=1 --file-test-mode=rndwr --file-block-size=4k --max-requests=0 --file-io-mode=async  --file-extra-flags=direct --file-rw-ratio=1 --file-fsync-freq=0 --time=300 run
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07de41abe018aaf71afca145b05c06f9.png) </span>

   * Test the random read IOPS of the volume

      ```Plain Text
      sysbench fileio --file-total-size=20G --file-num=1 --file-test-mode=rndrd --file-block-size=4k --max-requests=0 --file-io-mode=async  --file-extra-flags=direct --file-rw-ratio=1 --file-fsync-freq=0 --time=300 run
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9a0edeb62e7b9c3d6780ca2991d7bd1.png) </span>

   * Test the sequential write bandwidth of the volume

      ```Plain Text
      sysbench fileio --file-total-size=20G --file-num=1 --file-test-mode=seqwr --file-block-size=1024k --max-requests=0 --file-io-mode=async  --file-extra-flags=direct --file-rw-ratio=1 --file-fsync-freq=0 --time=300 run
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f067580789619f38fdf22fcb6eb55ad.png) </span>

   * Test the sequential read bandwidth of the volume

      ```Plain Text
      sysbench fileio --file-total-size=20G --file-num=1 --file-test-mode=seqrd --file-block-size=1024k --max-requests=0 --file-io-mode=async  --file-extra-flags=direct --file-rw-ratio=1 --file-fsync-freq=0 --time=300 run
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_559474a3f9580103f199ec6113ce66d5.png) </span>

   
   |Parameter​ |Description |
   |---|---|
   |\-\-file\-total\-size |Indicates the total size of files to be created. |
   |\-\-file\-num |Indicates test file number. |
   |\-\-file\-test\-mode |Indicates file read/write mode. Supported modes include seqwr (sequential write), seqrewr (sequential rewrite), seqrd (sequential read), rndrd (random read), rndwr (random write), and rndrw (random read\-write). |
   |\-\-file\-block\-size |Indicates the block size used in all I/O operations. |
   |\-\-file\-io\-mode |Indicates the file operation mode. Supported modes include sync (synchronous, the default mode), async (asynchronous), and mmap. Since sync impacts performance, specify the mode as async to ensure that libaio takes effect. |
   |\-\-file\-extra\-flags |Indicates the additional flag for opening files. Supported additional flags include sync, dsync, and direct. Here, specify "direct" to avoid writing after file system caching. |
   |\-\-file\-fsync\-freq |Specify the number of requests after which fsync is executed. 0: No need to execute fsync. |
   |\-\-file\-rw\-ratio |Indicates read/write ratio for combined tests (default: 1.5). Configure this parameter for scenarios that involve mixed read\-write (rw). |
   |\-\-time |By default, Sysbench runs tests for 10 seconds. Memory tests of Sysbench can also stop earlier after reading/writing operations specified by "file\-total\-size" are completed. To specify a test duration, configure the "time" parameter. |
   

4. FileIO test cleanup.

   Since test files are created during the test, you need to execute the command cleanup. Note that the value of certain parameters in the prepare and cleanup commands is required to be configured consistently.

   ```Plain Text
   sysbench fileio --file-total-size=100G --file-num=1 cleanup
   ```
   

5. Analyze test results.

   The output example of the Sysbench test result is shown in Step 3. You only need to focus on the "File operations" (for IOPS) and "Throughput" (for bandwidth) sections.

   * File operations:

      * reads/s: Read IOPS

      * writes/s: Write IOPS

   * Throughput:

      * read, MiB/s: Read bandwidth

      * written, MiB/s: Write bandwidt


</Tab>
</Tabs>
