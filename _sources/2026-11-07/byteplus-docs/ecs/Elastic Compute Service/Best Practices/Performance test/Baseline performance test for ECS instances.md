---
title: "Baseline performance test for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ECS-instance-performance-baseline-tests"
---

This topic describes how to use tools to test the performance of the ECS instance CPU, memory, network, and volume. This allows you to learn the ECS instance performance based on the data from test results.

<span id=".5rWL6K-V5Y6f5YiZ"></span>
## Test principles

For the smooth operation of your business, you need to comprehensively test the performance of your ECS instance that hosts the services. Make sure that you follow the principles below during performance tests:


* Objective: Clearly specify the specifications of the ECS instances to be tested (of CPU cores, CPU frequency, memory, storage, network bandwidth, operating system, and other components) and testing methods (such as deployment plans, instance numbers, and service load). This helps generate a fair and objective test result.

* Reasonable: Run the tests based on your needs and actual scenarios.

* Accurate: Select mature, stable, and authoritative testing tools and test cases. This allows the test results to reflect the ECS instance performance accurately.


<span id=".5rWL6K-V5bel5YW35Y-K5Li76KaB5oyH5qCH"></span>
## Testing tools and key metrics


|Type |Test tool |Test metrics |
|---|---|---|
|CPU |UnixBench |Single\-core benchmark score |
|||Multi\-core benchmark score |
||SuperPI |Calculation duration |
||Sysbench |Average number of events completed per second |
|Memory |Stream |Bandwidth |
||MLC |Latency |
||Sysbench |Bandwidth |
|Network |iPerfs |bps, pps |
||Pktgen ||
||Netperf ||
|Volume |FIO |I/O latency |
|||IOPS |
||dd |Bandwidth |
||Sysbench |IOPS, bandwidth |


<span id=".5rWL6K-V546v5aKD"></span>
## Test environment

<span id=".546v5aKD5YeG5aSH"></span>
### Prepare the environment


* [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). Recommended region: **China (Beijing)** .

* In the created VPC, create two ECS instances with the same specification. Then,[ associate an EIP ](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP)with one of the instances and [mount a data volume to it ](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume)(recommended capacity: at least 2 TB).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The test environment and methods provided in this topic are for reference only and do not represent the actual optimal performance of the instance.</div>


<span id=".6L2v5Lu254mI5pys"></span>
### Software version

ECS Instance operating system: In the example provided in this topic, CentOS 8.3 is used.

<span id="86KlQNfN"></span>
## Test CPU performance


<Tabs>
<Tab zoneid="tKS2G1htLR" title="CPU single-core/multi-core performance testing via UnixBench">
<TabTitle>CPU single-core/multi-core performance testing via UnixBench</TabTitle>

**Test description**

UnixBench is an open\-source tool for testing the basic performance of UNIX systems. It is also commonly used for testing ECS instance performance. You can run various tests via UnixBench to assess system performance from different aspects. Each test result is compared against a baseline value to generate an index score. Then, the index scores of all test items are combined to generate an overall test score.

**Procedure**


1. [Log in to the ECS instance to be tested](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to download and install UnixBench.

   ```Plain Text
   wget https://github.com/kdlucas/byte-unixbench/archive/v5.1.3.tar.gz
   tar -zxvf v5.1.3.tar.gz
   cd byte-unixbench-5.1.3/UnixBench
   make
   ```
   

3. Execute the following command to run the single\-core test.

   `./Run -c 1`

   The execution process may take longer, so please wait patiently. The test score will be displayed as shown in the following picture. Refer to the values of "INDEX" for the result. The higher the values, the better the performance.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9065ebdccf62362ad0180a4c84fefb85) </span>

4. Execute the following commands to run the multi\-core test.

   ```Bash
   # Obtain the number of CPU threads (core)
   cat /proc/cpuinfo| grep "processor"| wc -l
   ./Run -c {core}
   ```
   

   The execution process may take longer, so please wait patiently. The test score will be displayed as shown in the following picture. Refer to the values of "INDEX" for the result. The higher the values, the better the performance.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_aec00c4a88c541d9c16b086ebce3170a) </span>


</Tab>
<Tab zoneid="fZjbXjLRyK" title="Calculation duration testing via SuperPI">
<TabTitle>Calculation duration testing via SuperPI</TabTitle>

**Test description**

SuperPI is a computer program for calculating pi (π). It can achieve a maximum precision of 32,000,000 digits after the decimal point. It is a fast baseline test and is often used for overclocking or comparing configurations between different CPUs and hardware.

**Procedure**

Execute the following commands to install SuperPI and start testing.

```Bash
git clone https://github.com/Fibonacci43/SuperPI.git
cd ./SuperPI
gcc -O -funroll-loops -fomit-frame-pointer pi_fftcs.c fftsg_h.c -lm -o pi_css5
# Test the CPU computational capability by calculating the value of pi to a precision of 1<<22=4194304
./pi_css5 $((1<<22))
```


> If prompted that Git is not installed, execute the following commands to install Git.


```Bash
# Install Git on CentOS
yum install git -y

# Install Git on Ubuntu/Debian
apt-get install git -y
```


After the above commands are executed, the calculation time will be displayed as shown in the picture below. The smaller the value, the shorter the time and the stronger the computing power.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1033efb3b5908745c38544dbdded46ef) </span>


</Tab>
<Tab zoneid="pDsfiMFLdW" title="CPU load testing via Sysbench">
<TabTitle>CPU load testing via Sysbench</TabTitle>

For more information, refer to [Using Sysbench to test CPU load](https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance).


</Tab>
</Tabs>


<span id="FFXdfE1s"></span>
## Test memory performance


<Tabs>
<Tab zoneid="KIRxFyWNXO" title="Test bandwidth via Stream">
<TabTitle>Test bandwidth via Stream</TabTitle>

**Test description**

Stream is an industry\-recognized tool for testing memory performance comprehensively. Supported operations include Copy, Scale, Add, and Triad.

For more information, visit the [Stream official website](https://www.cs.virginia.edu/stream/) and refer to [Stream user guide](https://www.cs.virginia.edu/stream/ref.html).

**Procedure**


1. Execute the following commands to download and install Stream.

   ```Plain Text
   wget https://www.cs.virginia.edu/stream/FTP/Code/stream.c
   yum -y install gcc
   ```
   

2. Edit the test script.

   `gcc -O -fopenmp -mcmodel=medium -DSTREAM_ARRAY_SIZE=200000000 -DNTIMES=100 stream.c -o stream_omp_exe`

   
   |Parameter​ |Description |
   |---|---|
   |STREAM_ARRAY_SIZE |Specifies the array size used for testing.<br><br>Default value: 10,000,000. Stream creates three arrays of the size value specified in the `STREAM_ARRAY_SIZE` parameter. Default element type: double.<br><br>For reference, the memory used in the script above is 3 × STREAM_ARRAY_SIZE × sizeof(double) = 4.5 GiB. You can modify the value based on your needs. |
   |NTIMES |Specifies the number of runs for the test case. The final result will be the best one among all runs.<br><br>Default value: 10. Typically, you do not need to change this value. |
   

3. Execute the following commands to run the bandwidth test.

   ```Bash
   # On the same NUMA node
   numactl -N 0 -m 0 ./stream_omp_exe 
   # Cross-NUMA nodes
   numactl -N 1 -m 0 ./stream_omp_exe
   ```
   

   
   |Parameter​ |Description |
   |---|---|
   |numactl |Specifies the NUMA policy for process and memory allocation.<br><br>For example, `-N 0 -m 0` means using the CPU and the memory of NUMA node 0; `-N 1 -m 0` means using the CPU of NUMA node 1 and the memory of NUMA node 0. |
   

   After execution, the final result score will be displayed as shown below. Refer to the values of "Best Rate MB/s". The higher the values, the better the performance.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a51cd21e883c5384203ffc11a303f73f) </span>


</Tab>
<Tab zoneid="H90oAyUKzs" title="Test latency via MLC">
<TabTitle>Test latency via MLC</TabTitle>

**Test description**

[MLC](https://www.intel.cn/content/www/cn/zh/download/736633/intel-memory-latency-checker-intel-mlc.html) (Memory Latency Checker) is a memory testing tool developed by Intel. It can effectively and conveniently test memory latency and bandwidth. The tool also supports a series of fine\-grained tests for specific processor cores, caches, and memory.

**Procedure**


1. Execute the following commands to download and install MLC.

   ```Plain Text
   wget https://downloadmirror.intel.com/793041/mlc_v3.11.tgz
   tar -xzvf mlc_v3.11.tgz
   yum install glibc -y
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39354b4ba5ff135f6bea8ecf98acb428.png) </span>

2. Execute the following commands to run the latency test.

   ```Plain Text
   cd ./Linux/
   ./mlc --latency_matrix -e -r
   ```
   

   
   |Parameter​ |Description |
   |---|---|
   |\-\-latency_matrix |Prints the matrix of intra\-NUMA and cross\-NUMA memory latencies |
   |\-e |Outputs test results based on original prefetcher settings |
   |\-r |Outputs the latency result obtained from random accesses |
   

   After the above commands are executed, a matrix of local and cross\-socket memory latencies will be displayed. The lower the values, the lower the latency.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74d09c786588f4d542749708e8c14204.png) </span>


</Tab>
<Tab zoneid="tfpu91conI" title="Test Memory load via Sysbench">
<TabTitle>Test Memory load via Sysbench</TabTitle>

For more information, refer to [Using Sysbench to test Memory load](https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance).


</Tab>
</Tabs>


<span id="vZHHYAke"></span>
## Test network performance


* [Using iPerf3 to test network performance](https://docs.byteplus.com/en/docs/ecs/Using-iPerf3-to-test-network-performance)

* [Using Pktgen to test network performance](https://docs.byteplus.com/en/docs/ecs/Using-Pktgen-to-test-networ-performance)

* [Using Netperf to test network performance](https://docs.byteplus.com/en/docs/ecs/Using-Netperf-to-test-network-performance)


<span id="TBIWOPN4"></span>
## Test volume performance


* [Testing storage performance](https://docs.byteplus.com/en/docs/ecs/Testing-storage-performance)

* [Using Sysbench to test FileIO load](https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance)
