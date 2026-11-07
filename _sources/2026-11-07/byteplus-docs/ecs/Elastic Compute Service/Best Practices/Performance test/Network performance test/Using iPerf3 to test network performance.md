---
title: "Using iPerf3 to test network performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-iPerf3-to-test-network-performance"
---

This topic describes how to use iPerf3 to test ECS instance network performance.

## iPerf3 overview

iPerf3 is a tool for testing the maximum available bandwidth on IP networks. It allows you to adjust parameters related to timing, buffers, and protocols (TCP, UDP, SCTP, IPv4, and IPv6). It offers detailed test reports on network bandwidth, delay jitter, and packet loss rate.

## Procedure

> **tip**

> Test results provided in this topic are for reference only and do not represent the actual optimal performance of an ECS instance.

### Step 1: Prepare the environment

Refer to the practice of [purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create the DUT and Testers. The test environment provided in this topic is shown in the table below:

|ECS instance |ECS instance information |Quantity |IP address |Description |
|---|---|---|---|---|
|DUT |* Image: Debian 10 64 bit<br><br>* Instance type: ecs.ebmg2i.32xlarge |1 |172.0.0.1 |The instance under network PPS stress testing. It can serve as both the Client and the Server in an iperf3 test. |
|Tester |* Image: Debian 10 64 bit<br><br>* Instance type: ecs.ebmg2i.32xlarge |4 |172.0.0.2 ~ 172.0.0.5 |The instances for creating control connections with the DUT to transmit test details and results. They can serve as both the Client and the Server in an iperf3 test. |

> **tip**

> All ECS instances need to be associated with the same security group.

### Step 2: Install iperf3

1. Log in to the DUT and the Testers via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. On the DUT and the Testers, execute the following commands to install iperf3.

   ```Plain Text
   apt update
   apt install -y iperf3
   ```

### Step 3: Test network performance

**Inbound direction test**

* On the DUT, start 128 iperf3 server processes.

* Distribute 128 iperf3 servers evenly to four Testers. On each Tester, start 32 iperf3 server processes.

1. On the DUT (172.0.0.1), create the script server.sh, and then grant execution permission.

   1. Execute the `vim server.sh` command to create the server.sh file.

   2. Press `i` to enter the edit mode.

   3. In the server.sh file, enter the following content.

      ```Plain Text
      #! /bin/bash
      
      proc_num=$1
      port_begin=12000
      ls
      for ((i=0; i<proc_num; i++))
      do
          port=$((port_begin + i))
          cpu=$((i%$1 + 1))
      
          iperf3 -s -i 1 -p $port -A $(( $cpu % $1 )) -D > /dev/null &
      done
      
      ```

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x server.sh` command to grant execution permission to the server.sh file.

2. On the DUT (172.0.0.1), run `./ server.sh 128` to start 128 iperf3 server processes.

3. On each Tester, create the script client.sh, and then grant execution permission.

   1. Execute the `vim client.sh` command to create the client.sh file.

   2. Press `i` to enter the edit mode.

   3. In the client.sh file, enter the following content.

      ```Plain Text
      #! /bin/bash
      
      dst_ip=$1
      proc_num=$2
      port_begin=12000
      
      for ((i=0; i<proc_num; i++))
      do
          port=$((port_begin + i))
          iperf3  -c $dst_ip -u -l 16 -b 10000M -i 1 -t 3600 -p $port -A $(( $i % $2)) -P 1 > /dev/null 2>&1 &
      done
      ```

      > **tip**

      > Specify the values of parameter `port_begin` of the four Testers incrementally. For example:

      > 172.0.0.2: 12000

      > 172.0.0.3: 12032

      > 172.0.0.4: 12064

      > 172.0.0.5: 12096

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x client.sh` command to grant execute permission to the client.sh file.

4. On each Tester, execute the `./client.sh 172.0.0.1 32` command to start 32 iperf3 client processes.

5. On the DUT, execute the `sar -n DEV 1` command to view the test results.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bf56e8aafb4d6f883c6b2794e0e8c1ed.png)

**Outbound direction test**

* Distribute 128 ports evenly to four Testers. On each Tester, start 32 iperf client processes.

* The DUT (172.0.0.1) starts 32 iperf3 client processes to each Tester (172.0.0.2 to 172.0.0.5) to generate traffic, resulting in 128 iperf3 client processes in total.

1. On each Tester, create the script server.sh, and then grant execution permission.

   1. Execute the `vim server.sh` command to create the server.sh file.

   2. Press `i` to enter the edit mode.

   3. In the server.sh file, enter the following content.

      ```Plain Text
      #! /bin/bash
      
      proc_num=$1
      port_begin=12000
      
      for ((i=0; i<proc_num; i++))
      do
          port=$((port_begin + i))
          cpu=$((i%$1 + 1))
      
          iperf3 -s -i 1 -p $port -A $(( $cpu % $1 )) -D > /dev/null &
      done
      
      ```

      > **tip**

      > Specify the values of parameter `port_begin` of the four Testers incrementally. For example:

      > 172.0.0.2: 12000

      > 172.0.0.3: 12032

      > 172.0.0.4: 12064

      > 172.0.0.5: 12096

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x server.sh` command to grant execution permission to the server.sh file.

2. Execute `./server.sh 32` on the Testers to start 32 iperf3 server processes.

3. On the DUT (172.0.0.1), create the script client.sh, and then grant execution permission.

   1. Execute the `vim client.sh` command to create the client.sh file.

   2. Press `i` to enter the edit mode.

   3. In the client.sh file, enter the following content.

      ```Plain Text
      #! /bin/bash
      
      dst_ip=$1
      port_begin=$2
      cpu_start=$3
      proc_num=$4
      
      for ((i=0; i<proc_num; i++))
      do
          port=$((port_begin + i))
          cpu=$((cpu_start + i))
          iperf3  -c $dst_ip -u -l 16 -b 10000M -i 1 -t 180 -p $port -A $(( $cpu % $4)) -P 1 > /dev/null 2>&1 &
      done
      ```

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x client.sh` command to grant execute permission to the client.sh file.

4. On the DUT (172.0.0.1), execute the following commands to run the client.sh script file.

   ```Plain Text
   ./client.sh 172.0.0.2  12000  0   128
   ./client.sh 172.0.0.3  12032  32  128
   ./client.sh 172.0.0.4  12064  64  128
   ./client.sh 172.0.0.5  12096  96  128
   ```

5. Execute the `sar -n DEV 1` command on each Tester and view the test results.

   Then, sum up the results obtained in the four Testers to obtain the test result for DUT. For example: 3790019 + 3183582 + 3500913 + 3564047, which adds up to about 14 Mpps.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c15526a2be25d155fe3eb48ccd0ca61.png)
