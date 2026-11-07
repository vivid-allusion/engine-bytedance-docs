---
title: "Using Pktgen to test network performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-Pktgen-to-test-networ-performance"
---

This topic describes how to use Pktgen to test the network performance of ECS instances.

## Test tools

* To test Packets Per Second (PPS) for the performance of network small\-packet transmission, Linux pktgen or DPDK\-based applications are typically used as packet generators.

* To test Bits Per Second (BPS) for the performance of network bulk data transmission, the large\-packet transmission bandwidth of TCP and UDP is typically involved.

   |Tool |Test metric |Download link |
   |---|---|---|
   |Linux pktgen |UDP PPS, UDP BPS |[https://github.com/torvalds/linux/tree/master/samples/pktgen](https://github.com/torvalds/linux/tree/master/samples/pktgen) |
   |iperf2 |TCP BPS |[https://sourceforge.net/projects/iperf2](https://sourceforge.net/projects/iperf2/) |
   |Pktgen\-DPDK |UDP PPS, UDP BPS |[https://github.com/pktgen/Pktgen-DPDK](https://github.com/pktgen/Pktgen-DPDK) |

## Procedure

> **tip**

> Test results provided in this topic are for reference only and do not represent the actual optimal performance of an ECS instance.

### Step 1: Prepare the environment

Refer to the practice of [purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create a Device Under Test (DUT) and an Auxiliary test machine (Tester). Before the Pktgen\-DPDK test, associate two network interfaces with each ECS instance. One network interface is for logging in and executing commands, and the other is for DPDK testing.

The test environment provided in this topic is shown in the table below:

|ECS instance |ECS Information |Quantity |IP address |Description |
|---|---|---|---|---|
|Device Under Test (DUT) |* Image: Debian 10 64 bit<br><br>* Specification: ecs.g1.16xlarge |1 |192.168.222.151 |The instance under network throughput stress testing. |
|Auxiliary test machine (Tester) |* Image: Debian 10 64 bit<br><br>* Specification: ecs.g1.16xlarge<br><br><br>> We recommend that the network performance of the Tester is no lower than that of the DUT. For details of instance types, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |1 |192.168.222.240 |The instance for creating control connections with the DUT to transmit test details and results. |

### Step 2: Install software

On the DUT and the Tester, perform the following steps in sequence to install the test software.

#### Install dependencies

1. Connect to the ECS instance remotely. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands to install dependencies.

   ```Bash
   apt update
   apt install -y libpcap-dev
   apt install -y libnuma-dev
   apt-get install python3-pip -y
   pip3 install pyelftools -i https://mirrors.ivolces.com/pypi/simple/
   pip3 install ninja -i https://mirrors.ivolces.com/pypi/simple/
   pip3 install meson -i https://mirrors.ivolces.com/pypi/simple/
   ```

   > Note: Install Python 3.6 or a later version. Otherwise, an incompatibility occurs between Python 3 and certain packages.

#### Install test software

Select the test tool as needed, and then install it based on the steps below accordingly.

**Linux Pktgen**

1. Download [pktgen script](https://github.com/torvalds/linux/tree/master/samples/pktgen).

2. Make sure that the Linux kernel includes the pktgen module, and then execute the `modprobe pktgen` command to load the module.

**iperf**

Install iperf from the software repository or use the following commands to download and compile the source code.

```Bash
git clone https://git.code.sf.net/p/iperf2/code iperf2-code
cd iperf2-code/
./configure
make
make install
iperf -v         # Check the compilation or installation result
```

**Pktgen-DPDK**

Before the Pktgen\-DPDK test, associate two network interfaces with each instance. One network interface is for logging in and executing commands, and the other is for DPDK testing.

1. Create the build.sh script to download and compile the source code for DPDK and pktgen.

   1. Execute the `vim build.sh` command to create the build.sh file.

   2. Press `i` to enter the edit mode.

   3. In the build.sh file, enter the following content.

      ```Bash
      #!/bin/bash
      
      # Download the source code to the current directory
      cur_dir=$(cd $(dirname $0); pwd)
      
      # If the "dpdk" folder does not exist, then download via:
      cd $cur_dir
      if [ ! -e $cur_dir/dpdk ]
        then git clone https://dpdk.org/git/dpdk dpdk ; echo $?
      fi
      
      # If the "Pktgen-DPDK" folder does not exist, then download via:
      cd $cur_dir
      if [ ! -e $cur_dir/Pktgen-DPDK ]
        then git clone https://github.com/pktgen/Pktgen-DPDK.git Pktgen-DPDK ; echo $?
      fi
      
      # Compile and install DPDK
      cd $cur_dir/dpdk ; git checkout v21.11 ; meson build
      cd $cur_dir/dpdk/build ; ninja ; ninja install ; ldconfig
      
      # Compile and install Pktgen-DPDK
      cd $cur_dir/Pktgen-DPDK ; git checkout pktgen-21.11.0 ;
      meson build ; ninja -C build
      
      # Check the compilation result to confirm whether an executable file is generated
      ls -l $cur_dir/Pktgen-DPDK/build/app/pktgen
      ```

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x build.sh` command to grant execution permission to the build.sh file.

   6. Execute the `bash build.sh` command to run the script.

   > **tip**

   > If the number of queues for the test network ports exceeds 16, modify the value of the `NUM_Q` constant in the source file `app/pktgen-constants.h` before compilation for matching.

2. Execute the following commands to add the DPDK dynamic libraries to the system configuration.

   ```Bash
   echo "/usr/local/lib/x86_64-linux-gnu/" >> /etc/ld.so.conf
   /sbin/ldconfig -v
   ```

3. Execute the `ethtool -i eth1` command to obtain the PCI address of the network interface used for DPDK testing. In the example provided in this topic, the network interface "eth1" is used for DPDK testing.

   The following output is returned:

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ce79e44bd26697b76e83a24591931644.png)

4. Create the bind\-igbuio.sh script to associate the network interface used for testing with igb_uio.

   1. Execute the `vim bind-igbuio.sh` command to create the bind\-igbuio.sh file.

   2. Press `i` to enter the edit mode.

   3. In the bind\-igbuio.sh file, enter the following content.

      ```Bash
      #!/bin/bash
      
      # Specify a directory for the DPDK source code
      dpdk_dir=/root/dpdk/
      # Specify the PCI address of the network interface to be associated with igb_uio
      nic_bdf=00:07.0
      
      # Download the source code of dpdk-kmods to the current directory
      cur_dir=$(cd $(dirname $0); pwd)
      net_str=$(ls -l /sys/class/net/ | grep $nic_bdf)
      eth_str=${net_str##*/}
      
      # If the "dpdk-kmods" folder does not exist, then download via:
      if [ ! -e $cur_dir/dpdk-kmods/linux/igb_uio ]
        then git clone https://dpdk.org/git/dpdk-kmods ; echo $?
      fi
      
      # Compile igb_uio.ko
      cd $cur_dir/dpdk-kmods/linux/igb_uio/ ; make ; modprobe uio ; insmod igb_uio.ko ; echo $?
      
      ifconfig $eth_str down ; echo $?
      
      # Associate the network interface with igb_uio
      cd $dpdk_dir ; ./usertools/dpdk-devbind.py --bind=igb_uio $nic_bdf ; echo $?
      ```

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x bind-igbuio.sh` command to grant execution permission to the bind\-igbuio.sh file.

   6. Execute the `bash bind-igbuio.sh` command to run the script.

5. Execute the following commands to configure large\-page memory. In the example provided in this topic, the instances have 2 NUMA nodes.

   ```Bash
   echo 8192 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages
   echo 8192 > /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages
   cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages
   cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages
   cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/free_hugepages
   cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/free_hugepages
   ```

###

### Step 3: Run performance tests

#### Test small\-packet transmission performance (PPS)

**Use Linux pktgen to test UDP PPS**

1. On the Tester, enter the pktgen directory, and execute the following command to transmit packets.

   ```Bash
   bash pktgen_sample02_multiqueue.sh -i [eth_dev] -d [dut_ip] -s 64 -m [dut_mac] -c 10 -p 40000-40003 -n 0 -t [queue_num]
   ```

   > * [eth_dev]: Network interface name

   > * [dut_ip]: DUT private IP address

   > * [dut_mac]: DUT MAC address

   > * [queue_num]: Queue number

   Based on the following configuration in the script, the total number of flows generated at this time is calculated as: (109 \- 9 + 1) \* (40003 \- 40000 + 1) = 101 \* 4 = 404.

   ```Bash
   # Flow variation random source port between min and max
   UDP_SRC_MIN=9
   UDP_SRC_MAX=109
   ```

2. On the DUT, execute the `sar -n DEV 1` command to observe the network throughput.

   The following output is displayed:

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6e683245c726d134184effc4aa262060.png)

**Use Pktgen-DPDK to test UDP PPS**

##### > **tip**

> Before the Pktgen\-DPDK test, associate the network interfaces used for testing with igb_uio on the DUT and the Tester, respectively. Then, configure large\-page memory for the machines. For detailed instructions, refer to the steps above for [installing Pktgen\-DPDK](https://docs.byteplus.com/en/docs/ecs/Using-Pktgen-to-test-networ-performance#jump).

1. On the DUT and the Tester, perform the following steps to run pktgen.

   1. Execute the `vim run.sh` command to create the run.sh file.

   2. Press `i` to enter the edit mode.

   3. In the run.sh file, enter the following content.

      ```Bash
      #!/bin/bash
      
      pktgen_dir=/root/Pktgen-DPDK/          # Replace the value with the directory where the compiled Pktgen-DPDK source code is located on your server
      nic_bdf=00:07.0                        # Replace the value with the PCI address of the network interface associated with igb_uio on your server
      
      $pktgen_dir/build/app/pktgen -c 0xffff1 -n 4 -a $nic_bdf -- -P -m "[1-32:1-32].0"
      ```

      > * 0xffff1: Indicates the CPU mask used by the process. The lowest BIT CPU is for shell control, and other CPUs are for port packet reception and transmission.

      > * [1\-32:1\-32].0: Indicates the CPU number. This CPU number can not exceed the range of CPUs used for packet reception and transmission in the mask.

      >    * 1\-32 (before the colon): For packet reception

      >    * 1\-32 (after the colon): For packet transmission

      >    * .0: Indicates port 0

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x run.sh` command to grant execution permission to the run.sh file.

   6. Execute the `bash run.sh` command to run the script.

2. On the Tester, execute the following commands in pktgen to transmit packets.

   ```Bash
   set 0 proto udp
   range 0 src mac start 00:16:3e:2c:3b:5d        #MAC address of the Tester network interface
   range 0 src mac min 00:16:3e:2c:3b:5d          #MAC address of the Tester network interface
   range 0 src mac inc 00:00:00:00:00:00
   range 0 dst mac start 00:16:3e:37:78:b8        #MAC address of the DUT network interface
   range 0 dst mac min 00:16:3e:37:78:b8          #MAC address of the DUT network interface
   range 0 dst mac inc 00:00:00:00:00:00
   range 0 src port start 10000
   range 0 src port min 10000
   range 0 src port max 10000
   range 0 src port inc 0
   range 0 dst port start 2000
   range 0 dst port min 2000
   range 0 dst port max 2255
   range 0 dst port inc 1
   range 0 proto udp
   range 0 src ip start 192.168.222.240            #Tester private IP address
   range 0 src ip min 192.168.222.240              #Tester private IP address
   range 0 src ip inc 0.0.0.0
   range 0 size start 64                           # Packet size (minimum value: 64)
   range 0 size min 64
   range 0 size max 64
   range 0 size inc 0
   range 0 dst ip start 192.168.222.151            #DUT private IP address
   range 0 dst ip min 192.168.222.151              #DUT private IP address
   range 0 dst ip inc 0.0.0.0
   enable all range
   start 0
   ```

3. On the DUT, observe the PPS of received packets and the corresponding BPS in pktgen.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9961453cf232813704b6d3174d6a2b8b.png)

#### Test bulk data transmission performance (BPS)

**Use iperf to test TCP BPS**

1. On the DUT, execute the following command to run the iperf server.

   `iperf -s -i 1`

2. On the Tester, execute the following command to run the iperf client.

   `iperf -c [dut_ip] -P 32 -t 60 -i 1`

   > [dut_ip]: DUT private IP

3. On the DUT, execute the `sar -n DEV 1` command to observe the network throughput. Unit conversion: [rxkB/s] \* 8 / 1000000 = Gbps.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_70b16198ffd058ee01e31be3bad8b12d.png)

**Use Pktgen-DPDK to test UDP BPS**

> **tip**

> Before the Pktgen\-DPDK test, associate the network interfaces used for testing with igb_uio on the DUT and the Tester, respectively. Then, configure large\-page memory for the machines. For detailed instructions, refer to the steps above for [installing Pktgen\-DPDK](https://docs.byteplus.com/en/docs/ecs/Using-Pktgen-to-test-networ-performance#jump).

1. On the DUT and the Tester, perform the following steps to run pktgen.

   1. Execute the `vim run.sh` command to create the run.sh file.

   2. Press `i` to enter the edit mode.

   3. In the run.sh file, enter the following content.

      ```Bash
      #!/bin/bash
      
      pktgen_dir=/root/Pktgen-DPDK/          # Replace the value with the directory where the compiled Pktgen-DPDK source code is located on your server
      nic_bdf=00:07.0                        # Replace the value with the PCI address of the network interface associated with igb_uio on your server
      
      $pktgen_dir/build/app/pktgen -c 0xffff1 -n 4 -a $nic_bdf -- -P -m "[1-32:1-32].0"
      ```

      > * 0xffff1: Indicates the CPU mask used by the process. The lowest BIT CPU is for shell control, and other CPUs are for port packet reception and transmission.

      > * [1\-32:1\-32].0: Indicates the CPU number. This number can not exceed the range of CPUs used for packet reception and transmission in the mask.

      >    * 1\-32 (before the colon): For packet reception

      >    * 1\-32 (after the colon): For packet transmission

      >    * .0: Indicates port 0

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x run.sh` command to grant execution permission to the run.sh file.

   6. Execute the `bash run.sh` command to run the script.

2. On the Tester, execute the following commands to transmit packets.

   ```Bash
   set 0 proto udp
   range 0 src mac start 00:16:3e:2c:3b:5d        #MAC address of the Tester network interface
   range 0 src mac min 00:16:3e:2c:3b:5d          #MAC address of the Tester network interface
   range 0 src mac inc 00:00:00:00:00:00
   range 0 dst mac start 00:16:3e:37:78:b8        #MAC address of the DUT network interface
   range 0 dst mac min 00:16:3e:37:78:b8          #MAC address of the DUT network interface
   range 0 dst mac inc 00:00:00:00:00:00
   range 0 src port start 10000
   range 0 src port min 10000
   range 0 src port max 10000
   range 0 src port inc 0
   range 0 dst port start 2000
   range 0 dst port min 2000
   range 0 dst port max 2255
   range 0 dst port inc 1
   range 0 proto udp
   range 0 src ip start 192.168.222.240            #Tester private IP address
   range 0 src ip min 192.168.222.240              #Tester private IP address
   range 0 src ip inc 0.0.0.0
   range 0 size start 1400                           #Packet size (minimum value: 64)
   range 0 size min 1400
   range 0 size max 1400
   range 0 size inc 0
   range 0 dst ip start 192.168.222.151            #DUT private IP address
   range 0 dst ip min 192.168.222.151              #DUT private IP address
   range 0 dst ip inc 0.0.0.0
   enable all range
   start 0
   ```

3. On the DUT, observe the PPS of received packets and the corresponding BPS in pktgen. Unit conversion: [MBit/s] /1000 = Gbps.

   ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_338ea9c5a3721c2e9e50e6ef26f75c83.png)

## Subsequent operations

After the Pktgen\-DPDK test, you can associate the network interfaces used for testing with their original drivers as needed. In the example provided in this topic, the network interface is associated with virito\-pci.

1. Create the script bind\-virtio.sh to associate the network interface used for testing with igb_uio.

   1. Execute the `vim bind-virtio.sh` command to create the bind\-virtio.sh file.

   2. Press `i` to enter the edit mode.

   3. In the bind\-virtio.sh file, enter the following content.

      ```Bash
      #!/bin/bash
      
      dpdk_dir=/root/dpdk/     # Modify to the DPDK source code directory of your cloud server
      nic_bdf=00:07.0          # Need to change to the PCI address of the network card to which you want to bind igb_uio
      
      ifconfig $eth_str down ; echo $?
      
      cd $dpdk_dir ; ./usertools/dpdk-devbind.py --unbind $nic_bdf ; echo $?
      
      rmmod igb_uio ; echo $?
      
      cd $dpdk_dir ; ./usertools/dpdk-devbind.py --bind=virtio-pci $nic_bdf ; echo $?
      
      eth_int=0
      while [ "$eth_int" == "0" ]
      do
        eth_int=$(ls -l /sys/class/net/ | grep $nic_bdf | wc -l)
      done
      
      net_str=$(ls -l /sys/class/net/ | grep $nic_bdf)
      eth_str=${net_str##*/}
      
      eth_int=0
      while [ "$eth_int" == "0" ]
      do
        eth_int=$(ifconfig -a | grep $eth_str | wc -l)
      done
      
      ifconfig $eth_str up; echo $?
      
      ```

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   5. Execute the `chmod +x bind-virtio.sh` command to grant execution permission to the bind\-virtio.sh file.

   6. Execute the `bash bind-virtio.sh` command to execute the script.
