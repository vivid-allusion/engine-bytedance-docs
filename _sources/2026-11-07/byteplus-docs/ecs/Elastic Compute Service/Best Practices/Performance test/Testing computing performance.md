---
title: "Testing computing performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-computing-performance"
---

The cloud platform offers a variety of instance types, each providing different computing capabilities to suit a wide range of use scenarios. The performance metrics of computing capabilities include CPU and memory. This topic describes how to test the CPU and memory performance of an Elastic Compute Service (ECS) that runs the Linux operating system.

<span id="testing-cpu-performance"></span>
## Testing CPU performance

We recommend that you use the built\-in binary calculator of Linux to calculate the pi (π) value, which indicates the CPU performance.

<span id="before-you-begin"></span>
### Before you begin

Create an ECS instance by using an image from the cloud platform.

<span id="procedure"></span>
### Procedure


1. Remotely log on to the Elastic Compute Service (ECS) instance. For more information, refer to [Logging on to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to calculate the amount of time that is consumed for calculating 5,000 decimal digits of pi (π).

   `echo "scale=5000; a(1)*4" | time bc -l`

   `scale` indicates the accuracy. `a(1)*4` uses the inverse tangent function. In the trigonometric function, the inverse tangent of 1 is pi/4, while pi = 4\* pi/4. This command uses the binary calculator to calculate the inverse tangent of 1. The result is accurate to the 5,000th decimal digit of pi (π).


<span id="testing-memory-performance"></span>
## Testing memory performance

We recommend that you use the SysBench benchmarking tool to test memory performance. SysBench is a modular, cross\-platform, and multithreaded benchmarking tool.

<span id="before-you-begin"></span>
### Before you begin

Create an ECS instance by using an image from the cloud platform. Associate the ECS instance with an elastic IP address (EIP) to allow the ECS instance to communicate with the internet.

<span id="installing-sysbench"></span>
### Installing SysBench


1. Remotely log on to the Elastic Compute Service (ECS) instance. For more information, refer to [Logging on to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. The installation command varies based on the operating system. In this example, CentOS is used. Run the following command to install SysBench:

   `curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.rpm.sh | sudo bash`

   `sudo yum -y install sysbench`

3. Run the following command to test the memory performance of sequential read and write:

   `sysbench --test=memory --memory-block-size=64m --memory-total-size=100G --num-threads=16 --memory-scope=local --memory-access-mode=seq --time=100 run`

   
   |Parameter |Description |
   |---|---|
   |\-\-test=memory |Use SysBench to test the memory performance. |
   |\-\-memory\-block\-size=64m |The size of the memory block. The default size is 1 KB. We recommend that you set the buf value in a single test to a value that is greater than the L3 cache. If you specify a small buf value, all requests can hit the L3 cache. This reduces the test accuracy. |
   |\-\-memory\-total\-size=100G |The total size of data transfer. The default size is 100 GB. |
   |\-\-num\-threads=16 |The number of concurrent threads. We recommend that you set the value to the number of CPUs on the machine used in this test. If you specify a small value, CPU performance issues may occur. This reduces the test accuracy. |
   |\-\-memory\-scope=local |The access scope of the memory. Valid values: global and local. We recommend that you do not set the value to global, which may cause cache\-to\-cache issues on the CPU. This reduces the test accuracy. |
   |\-\-memory\-access\-mode=seq |The access mode of the memory. Valid values: seq (sequential access) and rnd (random access). We recommend that you set the value to seq. If you use rnd, performance issues may arise in random distribution functions of SysBench. This can cause the test result to be significantly lower than the actual bandwidth of the physical memory. |
