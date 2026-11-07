---
title: "Using Netperf to test network performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-Netperf-to-test-network-performance"
---

This topic describes how to use Netperf to test ECS instance network performance.

<span id=".TmV0cGVyZuS7i-e7jQ=="></span>
## Netperf overview

Netperf is a tool for testing network performance (mainly for TCP\- or UDP\-based data transmission). It supports different modes (bulk data transfer mode and request/response mode) in testing network performance based on the application. Netperf test results mainly indicate the speed at which one system sends data to another and the speed at which another system receives data. For more information, visit the [Netperf official website](http://www.netperf.org/).

<span id=".5YeG5aSH546v5aKD"></span>
## Prepare the environment

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Test results provided in this topic are for reference only and do not represent the actual optimal performance of an ECS instance.</div>


During testing, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to purchase two Linux\-based ECS instances with the same configurations. For ECS instance A, install Netperf netserver to serve as the server side. For ECS instance B, install Netperf to serve as the client side. Make sure that no other applications are running on both ECS instances during the test. Then, use ECS instance B to stress\-test ECS instance A (no packet size specified) for the TCP inbound bandwidth performance of ECS instance A. The network stress test lasts for 5 minutes. For ECS instance A, you can calculate the average bandwidth by using data collected from the 50th second to the 250th second of the test.

ECS instance planning is as follows:


|Host name |Private IP address |Role |
|---|---|---|
|benchmark\-1 |192.168.xx.xx |Server |
|benchmark\-2 |192.168.xx.xx |Client |


<span id=".5a6J6KOFTmV0cGVyZg=="></span>
## Install Netperf


1. On **both** ECS instances, execute the following commands to install Netperf.

   ```Plain Text
   wget https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.7.0
   tar -xzvf netperf-2.7.0
   yum install gcc sysstat -y
   cd ./netperf-netperf-2.7.0
   ./configure             
   make && make install
   ```
   

2. Execute the following command to verify the installation result. If help information is returned, Netperf is installed.

   `netperf -p`

   Parameter descriptions:

   
   |Parameter​ |Description |
   |---|---|
   |\-p |Indicates the port number for listening. |
   |\-H |Indicates the IP address of the recipient. |
   |\-t |Indicates the type of packet transmission protocol. |
   |\-l |Indicates test duration. |
   |\-m |Indicates packet size. Recommended: 1440 for bandwidth and 1 for sending or receiving packets. |
   


<span id=".5rWL6K-V572R57uc5oCn6IO9"></span>
## Test network performance

<span id=".5rWL6K-VVENQIGJwcw=="></span>
### Test TCP BPS


1. On the server side, start the netserver process to listen on port 12000.

   `netserver -p 12000`

2. On the client side, execute the following command. The IP address in the command is the private IP address of the server instance.

   `netperf -H 192.168.xx.xx -p 12000 -t TCP_STREAM -l 300 -- -m 1440 &`

3. On the server side, use sar to view the test results.

   `sar -n DEV 1 200`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68f3b3ef4baa86f191d9b1c9717180f1.png) </span>

   The test results of bps are values of rxkB/s. Unit conversion: kB/s \* 8 / 1000 = Mbps.


<span id=".5rWL6K-VVENQIGNwcw=="></span>
### Test TCP CPS

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before testing the TCP CPS of 3rd\-generation instances, you can optimize performance based on the <a href="https://docs.byteplus.com/en/docs/ecs/Using-Netperf-to-test-network-performance#.6ZmE5b2V">"Optimize the performance of TCP CPS"</a> section for better CPS results.</div>



1. On the server side, start the netserver process to listen on port 12000.

   `netserver -p 12000`

2. On the client side, execute the following command. The IP address in the command is the private IP address of the server instance.

   `netperf -H 192.168.xx.xx -p 12000 -t TCP_CRR -l 300 &`

3. On the server side, use sar to view the test results.

   `sar -n DEV 1`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dc76b583941419c275dde0b302e7b80.png) </span>

   The test results of CPS are the values of rxpck/s divided by 5.


<span id=".5rWL6K-VVURQIHBwcw=="></span>
### Test UDP PPS


1. On the server side, start the netserver process to listen on port 12000.

   `netserver -p 12000`

2. On the client side, execute the following command. The IP address in the command is the private IP address of the server instance.

   `netperf -H 192.168.xx.xx -p 12000 -t UDP_STREAM -l 300 -- -m 1 &`

3. On the server side, use sar to view the test results.

   `sar -n DEV 1 200`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_32dbed986bb42f34477c2a47314bbe4d.png) </span>

   The test results of pps are values of rxpck/s.


<span id=".6ZmE5b2V"></span>
## Appendix

**Optimize the performance of TCP CPS**

On 3rd\-generation instances, TCP CPS performance is affected by multiple factors. To optimize your ECS instance configurations for optimal TCP CPS performance, refer to the instructions below.


* Disable XPS for eth0 (applicable only to 3rd\-generation instances)

   On both instances, execute the following commands in sequence to disable XPS for eth0.

   ```Plain Text
   cd /sys/class/net/eth0/queues/
   for i in `ls  | grep tx` ; do  cat  $i/xps_cpus; done;                     #Check the current XPS configuration
   for i in `ls  | grep tx` ; do  echo "00000000" > $i/xps_cpus; done;        #Disable TX XPS; the number of bits in 0 must match the current xps_cpus
   ```
   

   This topic uses ecs.g3a.8xlarge (32C) as an example, as displayed below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14d10e0585c89236998faf93da39ac61.png) </span>

* Interrupt core binding (applicable only to 3rd\-generation AMD instances)

   1. On both instances, execute the following commands to configure interrupt affinity for eth0.

      ```Plain Text
      #Check the number of queues for the eth0 device
      queue_num=$(ethtool -l eth0 | grep "Combined" | head -n 1 | awk '{print $2}')
      
      #Bind interrupts to CPUs 0 to ($queue_num - 1)
      cat /proc/interrupts | grep virtio | grep input | cut -d: -f1 |  while read i; do        echo -n "irq $i bind cpu: ";     echo $((($i / 2) % $queue_num)) > /proc/irq/$i/smp_affinity_list;     cat /proc/irq/$i/smp_affinity_list; done | sort -n -t ' ' -k2
      
      cat /proc/interrupts | grep virtio | grep output | cut -d: -f1 |  while read i; do        echo -n "irq $i bind cpu: ";     echo $((($i / 2) % $queue_num)) > /proc/irq/$i/smp_affinity_list;     cat /proc/irq/$i/smp_affinity_list; done | sort -n -t ' ' -k2
      ```
      

   2. Run the core\-binding test via Netperf.

      On the server side, start multiple netserver processes for port listening. For example, start 1024 netserver processes.

      ```Plain Text
      queue_num=$(ethtool -l eth0 | grep "Combined" | head -n 1 | awk '{print $2}')
      
      for ((i = 0 ; i < 1024; i++)); do taskset -c $(($i % $queue_num)) netserver
      -p $(($i + 12865)) & done
      ```
      

      On the client side, execute the following command. The IP address in the command is the private network IP address of the server\-side instance.

      ```Plain Text
      queue_num=$(ethtool -l eth0 | grep "Combined" | head -n 1 | awk '{print $2}')
      
      for ((i = 0 ; i < 512; i++)); do taskset -c $(($i % queue_num)) netperf -H 192.168.xx.xx -p $(($i + 12865)) -t TCP_CRR -l 120 & done
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59ecbd9fb20b84706f1fd32b2d0f90e2.jpg) </span>

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e960915dfb487c14ff7dfab00df4196.jpg) </span>
