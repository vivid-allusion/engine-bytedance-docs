---
title: "Testing network performance of 3rd-generation instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-the-network-performance-of-third-generation-ECS-instances"
---

In the examples provided in this topic, Pktgen\-DPDK, Kernel Pktgen, iPerf3, and ping tools are used to test the network performance of 3rd\-generation instances, including the network PPS, bandwidth, and latency.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Test results provided in this topic are for reference only and do not represent the actual optimal performance of an ECS instance.

* To avoid data loss, we recommend running network performance tests on a newly created, data\-free instance with the guidance provided in this topic.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created 3rd\-generation ECS instances or 3rd\-generation bare metal instances that meet the [requirements for the corresponding test scenario](https://docs.byteplus.com/en/docs/ecs/Testing-the-network-performance-of-third-generation-ECS-instances#.5YeG5aSH546v5aKD). For more information, see [Purchasing instances via wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* For the same test scenario, all instances need to be associated with the same VPC and the same security group.


<span id=".5YeG5aSH546v5aKD"></span>
## Prepare the environment

For different test scenarios, recommended instance types and quantities are listed below.


* **Test instance network PPS (≤ 6,000,000), bandwidth, and latency**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Testing the network bandwidth and latency of an instance requires no specific network PPS value. You can select any instance type for the test. For details of instance types, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>.   </div>
   

   
   |Sample configuration |Device Under Test (DUT) |Auxiliary test machine (Tester) |
   |---|---|---|
   |Instance specifications |g3i.large |g3i.large |
   |Image |Ubuntu 22.04 |Ubuntu 22.04 |
   |Network interface quantity |1 |1 |
   |Instance quantity |1 |1 |
   

* **Test instance network PPS (\> 6,000,000)** 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before the Pktgen\-DPDK test, associate two network interfaces with each instance. One network interface is for logging in and executing commands, and the other is for DPDK testing. Note that network interface eth1 should be used for the DPDK testing and network interface eth0 for management. Switching eth0 to the user space will disconnect the SSH session.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can refer to this topic for network PPS testing on any 3rd\-generation instance with a network PPS \> 6,000,000. In the example provided in this topic, the instance type g3i.48xlarge (192 vCPU) is used to test the optimal 36,000,000 PPS specified in its instance type specifications.   </div>
   

   
   |Sample configuration |Device Under Test (DUT) |Auxiliary test machine (Tester) |
   |---|---|---|
   |Instance specifications |g3i.48xlarge |g3i.48xlarge |
   |Image |Ubuntu 22.04 |Ubuntu 22.04 |
   |Network interface quantity |2 |2 |
   |Instance quantity |1 |1 |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5rWL6K-V572R57ucUFBT77yIIOKJpCA2MDDkuIfvvIk="></span>
### Test network PPS (≤ 6,000,000)


1. Remotely connect to the DUT and Tester. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. On the Tester, download [pktgen script](https://github.com/torvalds/linux/tree/master/samples/pktgen).

3. Make sure that the Linux kernel includes the pktgen module, and then execute the `modprobe pktgen` command to load the module.

4. On the Tester, switch to the pktgen directory and execute the following command to transmit packets.

   ```Plain Text
   bash pktgen_sample02_multiqueue.sh -i <Network Card Device Name> -d <Private Network IP Address of the Tested Machine> -s 64 -m <MAC Address of the Tested Machine> -c 10 -p 40000-40003 -n 0 -t <Number of Network Card Queues>
   ```
   

   Based on the following configuration in the script, the total number of flows generated at this time is calculated as: (109 \- 9 + 1) \* (40003 \- 40000 + 1) = 101 \* 4 = 404.

   ```Plain Text
   # Flow variation random source port between min and max
   UDP_SRC_MIN=9
   UDP_SRC_MAX=109
   ```
   

5. On the DUT, execute the `sar -n DEV 1` command to view the test results.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b302540ad21b2df5d40c0ed4bd1845dd.PNG) </span>


<span id=".5rWL6K-V572R57ucUFBT77yIID4gNjAw5LiH77yJ"></span>
### Test network PPS (\> 6,000,000)


1. Remotely connect to the DUT and Tester. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. On the DUT and the Tester, execute the following commands to install the dependent software and Pktgen\-DPDK.

   1. Execute the following commands to install the dependent software. Note: Install Python 3.6 or a later version. Otherwise, Python 3 and certain software packages may be incompatible.

      ```Plain Text
      apt update
      apt install -y libpcap-dev
      apt install -y libnuma-dev
      apt-get install python3-pip -y
      apt install -y git
      pip3 install pyelftools -i https://mirrors.ivolces.com/pypi/simple/
      pip3 install ninja -i https://mirrors.ivolces.com/pypi/simple/
      pip3 install meson -i https://mirrors.ivolces.com/pypi/simple/
      ```
      

   2. Execute the following commands to install Pktgen\-DPDK.

      1. Create the `down-pktgen.sh` script to download the source code for DPDK and pktgen.

         1. Execute the `cd /root/;vim down-pktgen.sh` command to create the down\-pktgen.sh file.

         2. Press `i` to enter the edit mode.

         3. In the down\-pktgen.sh file, enter the following content.

            ```Plain Text
            #!/bin/bash    
            
            # Download the source code to the current directory
            cur_dir=$(cd $(dirname $0); pwd)
            
            # If the dpdk folder does not exist, download it
            cd $cur_dir
            if [ ! -e $cur_dir/dpdk ]
              then git clone https://dpdk.org/git/dpdk dpdk ; echo $?
            fi
            
            # If the Pktgen-DPDK folder does not exist, download it
            cd $cur_dir
            if [ ! -e $cur_dir/Pktgen-DPDK ]
              then git clone https://github.com/pktgen/Pktgen-DPDK.git Pktgen-DPDK ; echo $?
            fi
            
            # Switch to the branch compatible with pktgen-21.11.0
            cd $cur_dir/dpdk ; git checkout v21.11 ;
            cd $cur_dir/Pktgen-DPDK ; git checkout pktgen-21.11.0 ;
            ```
            

         4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

         5. Execute the `chmod +x down-pktgen.sh` command to grant execution permission to the `down-pktgen.sh` file.

         6. Execute the `bash down-pktgen.sh` command to run the script.

      2. Modify the packet transmission and reception engine in pktgen.c to optimize the packet transmission and reception processing of pktgen.

         1. Optimize the packet transmission engine in pktgen.c.

            1. Execute the command `vim ./Pktgen-DPDK/app/pktgen.c +341` to open the `pktgen.c file` and jump to line 341.

            2. Press `i` to enter the edit mode.

            3. Add the following code in the line immediately after `cnt -= ret;`.

               ```Plain Text
               if (cnt != 0) {
                   rte_delay_us(8);
               }
               ```
               

               The modified code is shown below.

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a29a8ffef15201d82e24ef4512559ac.png) </span>

            4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

         2. Optimize the packet reception engine in pktgen.c.

            1. Execute the command `vim ./Pktgen-DPDK/app/pktgen.c` to open the `pktgen.c` file.

            2. Enter `/_64` to search for the keyword `_64`.

            3. Press `i` to enter the edit mode.

            4. Replace the code line `info->sizes._64++;` with the following code, and comment out this line.

               ```Plain Text
               {
                       //info->sizes._64++;
                       ;
                   }
               ```
               

               The modified code is shown below.

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98c4c4e7a14d09806dc6a1cf38967636.png) </span>

            5. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

      3. Change the three instances of fclose to pclose in the files `./Pktgen-DPDK/app/pktgen.h` and `./Pktgen-DPDK/lib/common/lscpu.c`.

         1. Execute the following command to open the file.

            `vim ./Pktgen-DPDK/app/pktgen.h`

            `vim ./Pktgen-DPDK/lib/common/lscpu.c`

         2. Press `i` to enter the edit mode.

         3. Change fclose to pclose.

            The modified file `./Pktgen-DPDK/app/pktgen.h` is shown as follows.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a6900de103b6c5e508e3ac727203e14.png) </span>

             The modified file `./Pktgen-DPDK/lib/common/lscpu.c` is shown as follows.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a32371fa81098cd7e2b32679d6fbde6.png) </span>

         4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

      4. Modify pktgen to support 32 queues.

         1. Execute the command `vim ./Pktgen-DPDK/app/pktgen-constants.h +34` to open the ./Pktgen\-DPDK/app/pktgen\-constants.h file.

         2. Press `i` to enter the edit mode.

         3. Specify the NUM_Q value to 32.

            The modified code is shown below.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cb3fccd027611a56b91128c100e02e8.png) </span>

         4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Or, you can complete the operations in steps ii, iii, and iv as follows: copy the patch file in the <a href="https://docs.byteplus.com/en/docs/ecs/Testing-the-network-performance-of-third-generation-ECS-instances#.6ZmE5b2V">appendix</a> to the <code>/root/Pktgen-DPDK</code> directory and then execute the following commands to configure your Git email and to apply the patch directly.      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">      ```Plain Text
      cd /root/Pktgen-DPDK
      git config --global user.email "you@example.com"
      git config --global user.name "Your Name"
      git am --signoff < ./0001-Optimize-performance.patch
      ```
            </div>
      

   3. Execute the command `bash /root/build-dpdk-pktgen.sh` to compile the source code of DPDK and Pktgen. The content of the script build\-dpdk\-pktgen.sh is as follows.

      ```Plain Text
      #!/bin/bash
      # build-dpdk-pktgen.sh  
      
      # Download the source code to the current directory
      cur_dir=$(cd $(dirname $0); pwd)
      
      # Compile and install DPDK
      cd $cur_dir/dpdk ; meson build
      cd $cur_dir/dpdk/build ; ninja ; ninja install ; ldconfig
      
      # Compile and install Pktgen-DPDK
      cd $cur_dir/Pktgen-DPDK ;
      meson build ; ninja -C build
      
      # Check if the compilation result generates an executable file
      ls -l $cur_dir/Pktgen-DPDK/build/app/pktgen
      ```
      

3. Execute the following commands to add the DPDK dynamic libraries to the system configuration.

   ```Plain Text
   echo "/usr/local/lib/x86_64-linux-gnu/" >> /etc/ld.so.conf
   /sbin/ldconfig -v
   ```
   

4. Create the bind\-igbuio.sh script to associate the network interface used for testing with igb_uio.

   1. Execute the `ethtool -i eth1` command to obtain the PCI address of the network interface used for DPDK testing. In the example provided in this topic, the network interface "eth1" is used for DPDK testing. The output is returned as follows.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4cd4405337b43ce9d6f462f15ecb59de.png) </span>

   2. Execute the `cd /root/;vim bind-igbuio.sh` command to create the bind\-igbuio.sh file.

   3. Press `i` to enter the edit mode.

   4. In the bind\-igbuio.sh file, enter the following content and replace the `nic_bdf` value with the network interface PCI address obtained in step a.

      ```Plain Text
      #!/bin/bash
      
      # Specify the DPDK source code directory
      dpdk_dir=/root/dpdk/
      # Specify the PCI address of the network card to be bound to igb_uio
      nic_bdf=0000:11:00.0
      
      # Download the dpdk-kmods source code to the current directory
      cur_dir=$(cd $(dirname $0); pwd)
      net_str=$(ls -l /sys/class/net/ | grep $nic_bdf)
      eth_str=${net_str##*/}
      
      # If the dpdk-kmods folder does not exist, download it
      if [ ! -e $cur_dir/dpdk-kmods/linux/igb_uio ]
        then git clone https://dpdk.org/git/dpdk-kmods ; echo $?
      fi
      
      # Compile igb_uio.ko
      cd $cur_dir/dpdk-kmods/linux/igb_uio/ ; make ; modprobe uio ; insmod igb_uio.ko ; echo $?
      
      ifconfig $eth_str down ; echo $?
      
      # Bind the network card to igb_uio
      cd $dpdk_dir ; ./usertools/dpdk-devbind.py --bind=igb_uio $nic_bdf ; echo $?
      ```
      

   5. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   6. Execute the `chmod +x bind-igbuio.sh` command to grant execution permission to the bind\-igbuio.sh file.

   7. Execute the `bash bind-igbuio.sh` command to associate the network interface used for testing with igb_uio.

5. Execute the command `lscpu | grep 'NUMA node(s)'` to query the number of NUMA nodes in the instance. Based on the NUMA node number, execute the following commands to configure large\-page memory.

   * For instance with one NUMA node

      ```Plain Text
      echo 16384 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
      cat /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
      cat /sys/kernel/mm/hugepages/hugepages-2048kB/free_hugepages
      ```
      

   * For instance with two NUMA nodes

      ```Plain Text
      echo 16384 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages
      echo 16384 > /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages
      cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages
      cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages
      cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/free_hugepages
      cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/free_hugepages
      ```
      

7. On the DUT and the Tester, perform the following steps to run Pktgen.

   1. Execute the `cd /root/;vim run.sh` command to create the run.sh file.

   2. Press `i` to enter the edit mode.

   3. In the `run.sh` file, enter the following content.

      ```Plain Text
      #!/bin/bash
      
      pktgen_dir=/root/Pktgen-DPDK/          # Modify to the directory of the compiled Pktgen-DPDK source code on your server
      nic_bdf=11:00.0                        # Modify to the PCI address of the network card that has been bound to igb_uio on your server
      
      $pktgen_dir/build/app/pktgen -c 0x1ffffffff -n 4 -a $nic_bdf,speed=100000  -- -P -m "[1-32:1-32].0"
      ```
      

      > * 0xffff1: Indicates the CPU mask used by the process. The lowest BIT CPU is for shell control, and other CPUs are for port packet reception and transmission.

      > * [1\-32:1\-32].0: Indicates the CPU number. This number can not exceed the range of CPUs used for packet reception and transmission in the mask.

      > * 1\-32 (before the colon): For packet reception.

      > * 1\-32 (after the colon): For packet transmission.

      > * .0: Indicates port 0.

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   5. Execute the `chmod +x run.sh` command to grant execution permission to the run.sh file.

   6. Execute the `bash run.sh` command to start Pktgen.

7. On the Tester, execute the following commands in Pktgen to transmit packets.

   > * Based on the comment instructions, replace the MAC and private IP addresses of the Tester and the DUT in the command lines with the actual MAC and private IP addresses of your Tester and DUT.

   > * Before you execute the following commands, delete the comments marked with #. Otherwise, the commands may fail to be executed.

   ```Plain Text
   set 0 proto udp
   range 0 src mac start 00:16:3e:5c:xx:xx       #MAC address of the network device on the auxiliary test machine
   range 0 src mac min 00:16:3e:5c:xx:xx         #MAC address of the network device on the auxiliary test machine
   range 0 src mac inc 00:00:00:00:00:00
   range 0 dst mac start 00:16:3e:3b:xx:xx       #MAC address of the network device on the tested machine
   range 0 dst mac min 00:16:3e:3b:xx:xx         #MAC address of the network device on the tested machine
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
   range 0 src ip start 192.XX.XX.17             #Private network IP of the auxiliary test machine
   range 0 src ip min 192.XX.XX.17               #Private network IP of the auxiliary test machine
   range 0 src ip inc 0.0.0.0
   range 0 size start 64                         #Packet size (minimum 64)
   range 0 size min 64
   range 0 size max 64
   range 0 size inc 0
   range 0 dst ip start 192.XX.XX.143            #Private network IP of the tested machine
   range 0 dst ip min 192.XX.XX.143              #Private network IP of the tested machine
   range 0 dst ip inc 0.0.0.0
   enable all range
   start 0
   ```
   

8. On the DUT, observe the PPS of received packets and the corresponding BPS in Pktgen.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e78fac97842cd07392fde9a982357974.png) </span>

9. Re\-associate the network interface with virtio\-pci.

   1. Execute the `cd /root/;vim bind-virtio.sh` command to create the bind\-virtio.sh file.

   2. Press `i` to enter the edit mode.

   3. In the bind\-virtio.sh file, enter the following content.

      ```Plain Text
      #!/bin/bash
      
      dpdk_dir=/root/dpdk/     # Modify to the DPDK source code directory of your cloud server
      nic_bdf=11:00.0          # Change to the PCI address of the network card to be bound to igb_uio
      
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
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   5. Execute the `chmod +x bind-virtio.sh` command to grant execution permission to the bind\-virtio.sh file.

   6. Execute the `bash bind-virtio.sh` command to execute the script.


<span id=".5rWL6K-V572R57uc5bim5a69"></span>
### Test network bandwidth


1. Remotely connect to the DUT and Tester. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. On the DUT and the Tester, execute the following commands to install iPerf3.

   ```Plain Text
   apt update
   apt install -y iperf3
   ```
   

3. On the DUT, create the iperf3\-srv.sh file, and then grant execution permission.

   1. Execute the `vim iperf3-srv.sh` command to create the `iperf3-srv.sh` file.

   2. Press `i` to enter the edit mode.

   3. In the `iperf3-srv.sh` file, enter the following content.

      ```Plain Text
      #!/bin/bash
      # iperf3-srv.sh
      
      lcore_num=$(lscpu | grep "^CPU(s):" | awk '{ print $2; }')
      proc_num=$(($lcore_num < 32 ? $lcore_num : 32))
      core_sibling=$(cat /sys/devices/system/cpu/cpu0/topology/thread_siblings_list)
      for ((i = 0; i < $proc_num ; i = i + 1)); do
          port=$(($i + 5201))
          if [[ $lcore_num -gt 96 && $core_sibling == "0-1" ]]; then
              lcore=$(($i * 2))
          else
              lcore=$(($i % $lcore_num))
          fi
          taskset -c $lcore iperf3 -s -p $port &
      done
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   5. Execute the `chmod +x iperf3-srv.sh` command to grant execution permission to the iperf3\-srv.sh file.

4. On the DUT, execute the `./iperf3-srv.sh` command to start the iperf3 server process.

5. (Optional) If the network bandwidth of the tested instance is 96 Gbit/s, this instance belongs to the following types: c3i.48xlarge (Beta), g3i.48xlarge (Beta), r3i.48xlarge (Beta), or 3rd\-generation bare metal instances. This means that you also need to execute the following script on both the Tester and DUT to interrupt core binding. If the tested instance is of other types, skip this step.

   ```Plain Text
   #!/bin/bash
   # bind-intr.sh
   
   #stop cloud-monitor-agent service
   service cloud-monitor-agent stop > /dev/null 2>&1
   
   #stop irqbalance service
   service irqbalance stop > /dev/null 2>&1
   service irqbalance-ng stop > /dev/null 2>&1
   
   a=$(cat /proc/interrupts | grep virtio | grep put | awk -F ':' '{print $1}')
   MASK="ffffffff"
   for irq in $a; do
       echo $MASK > /proc/irq/$irq/smp_affinity
   done
   ```
   

6. (Optional) If the tested instance is a bare metal instance equipped with a 4th\-generation AMD EPYC™ Genoa processor (for example, ebmg3ad/ebmc3ad), create the following script on the Tester to enable XPS and establish a one\-to\-one mapping between TX queues and CPUs. If the tested instance is of other types, skip this step.

   1. Execute the `vim xps_setup.sh` command to create the xps_setup.sh file and add the following content to the file.

      ```Plain Text
      #!/bin/bash
      # xps_setup.sh
      
      function usage() {
          echo "Change setting of XPS txq to CPU mapping via files"
          echo " /sys/class/net/DEV/queues/tx-*/xps_cpus "
          echo ""
          echo "Usage: $0 [-h] --dev ethX --txq N --cpu N"
          echo "  -d | --dev     : (\$DEV)       Interface/device (required)"
          echo "  --default      : (\$DEFAULT)   Setup 1:1 mapping TXQ-to-CPU"
          echo "  --disable      : (\$DISABLE)   Disable XPS via mask 0x00"
          echo "  -v | --verbose : (\$VERBOSE)   verbose"
          echo ""
      }
      
      ## -- General shell logging cmds --
      function err() {
          local exitcode=$1
          shift
          echo -e "ERROR: $@" >&2
          exit $exitcode
      }
      
      function info() {
          if [[ -n "$VERBOSE" ]]; then
              echo "# $@"
          fi
      }
      
      function sorted_txq_xps_cpus() {
          local queues=$(ls /sys/class/net/$DEV/queues/tx-*/xps_cpus | sort --field-separator='-' -k2n)
          echo $queues
      }
      
      function cpu_to_mask() {
          local cpu=$1
          printf "%X" $((1 << $cpu))
      }
      
      function xps_setup_1to1_mapping() {
          local cpu=0
          local txq=0
          for xps_cpus in $(sorted_txq_xps_cpus); do
      
              if [[ "$DISABLE" != "yes" ]]; then
                  # Map the TXQ to CPU number 1-to-1
                  mask=$(cpu_to_mask $cpu)
              else
                  # Disable XPS on TXQ
                  mask=0
              fi
      
              echo $mask > $xps_cpus
              info "NIC=$DEV TXQ:$txq use CPU $cpu (MQ-leaf :$mqleaf)"
              let cpu++
              let txq++
          done
      }
      
      ##  --- Parse command line arguments / parameters ---
      while true; do
          case "$1" in
              -d | --dev ) # device
                export DEV=$2
                info "Device set to: DEV=$DEV" >&2
                shift 2
                ;;
              -v | --verbose)
                export VERBOSE=yes
                # info "Verbose mode: VERBOSE=$VERBOSE" >&2
                shift
                ;;
              --default )
                info "Setup default 1-to-1 mapping TXQ-to-CPUs" >&2
                export DEFAULT=yes
                shift 1
                ;;
              --disable )
                info "Disable XPS via mask 0x00" >&2
                export DISABLE=yes
                shift 1
                ;;
              -- )
                shift
                break
                ;;
              -h | --help )
                usage;
                exit 0
                ;;
              * )
                shift
                break
                ;;
          esac
      done
      
      if [ -z "$DEV" ]; then
          usage
          err 2 "Please specify device"
      fi
      
      
      if [[ -n "$DEFAULT" ]]; then
          xps_setup_1to1_mapping
      fi
      
      if [[ "$DISABLE" == "yes" ]]; then
          if [[ -z "$DEFAULT" && -z "$TXQ" ]]; then
              err 5 "Use --disable together with --default"
          fi
      fi
      ```
      

   2. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   3. Execute the `chmod +x xps_setup.sh` command to grant execution permission to the `xps_setup.sh` file.

   4. Execute the command`./ xps_setup.sh -d eth0 --default` to enable XPS and establish a one\-to\-one mapping between TX queues and CPUs.

7. On the Tester, create the `iperf3-cli.sh file`, and then grant execution permission.

   1. Execute the `vim iperf3-cli.sh` command to create the `iperf3-cli.sh` file.

   2. Press `i` to enter the edit mode.

   3. In the `iperf3-cli.sh` file, enter the following content.

      ```Plain Text
      #!/bin/bash
      # iperf3-cli.sh
      
      if [ $# -ne 2 ]; then
          echo $0 "<server_ip> <time_secs>"
          exit 255
      fi
      
      lcore_num=$(lscpu | grep "^CPU(s):" | awk '{ print $2; }')
      proc_num=$(($lcore_num < 32 ? $lcore_num : 32))
      core_sibling=$(cat /sys/devices/system/cpu/cpu0/topology/thread_siblings_list)
      for ((i=0 ; i < $proc_num; i = i + 1)); do
          port=$(($i + 5201))
          #check instance is 192C vm
          if [[ $lcore_num -gt 96 && $core_sibling == "0-1" ]]; then
              lcore=$(($i * 2))
          else
              lcore=$(($i % $lcore_num))
          fi
          taskset -c $lcore iperf3 -c $1 -p $port -t $2 -P 4 2>&1 &
      done
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   5. Execute the `chmod +x iperf3-cli.sh` command to grant execution permission to the iperf3\-cli.sh file.

8. On the Tester, execute the following command to start the iperf3 client process.

   ```Plain Text
   ./iperf3-cli.sh <Private IP of the tested machine> 300
   ```
   

9. On the DUT, execute the `sar -n DEV 1` command to view the test results. In the figure below, the data in the `rxkB/s` column represents the receive bandwidth.

   > Unit conversion: [rxkB/s] \* 8 \* 1024 / 1000000000 = Gbps   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73ec53eb25b7bf8fcb4365b017efb9b7.png) </span>


<span id=".5rWL6K-V572R57uc5pe25bu2"></span>
### Test the network latency


1. Remotely connect to the DUT and Tester. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. (Optional) For tests on virtual machines, skip this step. For tests on bare metal instances, the following steps are required to enable CPU performance mode.

   1. On the DUT and the Tester, execute the following command to install cpupower.

      ```Plain Text
      apt update
      apt install -y linux-intel-iotg-tools-common linux-tools-5.15.0-48-generic
      ```
      

      During linux\-tools\-5.15.0\-48\-generic installation, the following error may occur:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9320d0734e232a8abb56519fd7c24cee.png) </span>

      This error occurs because the tool `/usr/bin/acpidbg` is already installed in the first installation package linux\-intel\-iotg\-tools\-common. To fix this, execute the command below (use the linux\-tools\-common version from the error message) to force overwrite the package marked in the red box.

      ```Plain Text
      dpkg -i --force-overwrite /var/cache/apt/archives/linux-tools-common_5.15.0-66.73_all.deb
      ```
      

   2. On the DUT and the Tester, execute the following command to set all CPUs to performance mode.

      ```Plain Text
      cpupower -c all frequency-set -g performance
      ```
      

   3. On the DUT, execute the following command to test the network latency.

      > min: Minimum latency. avg: Average latency. max: Maximum latency. Unit: ms      
      

      ```Plain Text
      ping -f -c 10000 <Private network IP address of the auxiliary test machine>
      ```
      


<span id=".6ZmE5b2V"></span>
## Appendix

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfe68a00cfe182d1e0c9c5f0ca3f5f8e.patch" name="0001-Optimize-performance.patch">0001-Optimize-performance.patch</Attachment>
