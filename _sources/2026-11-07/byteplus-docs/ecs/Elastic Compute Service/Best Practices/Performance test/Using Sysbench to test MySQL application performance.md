---
title: "Using Sysbench to test MySQL application performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-the-performance-of-MySQL-applications"
---

This topic describes how to use Sysbench to test MySQL application performance of ECS instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background


* **MySQL overview**

   MySQL is a Relational Database Management System (RDBMS) and uses SQL, the most common Structured Query Language, for database management. In web application scenarios, when web applications are under high load, MySQL has high requirements for virtual machine performance, including the performance of CPU computing capacity, network, and storage. As a result, MySQL is often used to test the overall performance of a virtual machine.

* **Sysbench**

   Sysbench is a modular, cross\-platform, open\-source multi\-threaded benchmarking tool. You can use it to test the performance of databases, CPU, memory, threads, and IO. Typically, it is used to test database loads under different system parameters. For detailed instructions, refer to [Using Sysbench to test ECS instance performance](https://docs.byteplus.com/en/docs/ecs/Using-Sysbench-to-test-ECS-performance).


<span id=".5rWL6K-V5oyH5qCH"></span>
## Test metrics


* TPS (Transactions Per Second): The number of transactions the database executes per second.

* QPS (Queries Per Second): The number of queries received per second. This refers to the number of SQL statements the database executes per second (including `INSERT`, `SELECT`, `UPDATE`, and `DELETE`).


<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* MySQL/MariaDB: In the example provided in this topic, MariaDB 10.6.12 is used.

* Sysbench: In the example provided in this topic, Sysbench 1.0.19 is used.


<span id=".5rWL6K-V546v5aKD"></span>
## Test environment

Two ECS instances with the same specifications are used as the Server and Client, respectively. The specific configuration is shown in the table below.

> To create an instance, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).



|Sample configuration |Server |Client |
|---|---|---|
|Instance specifications |ecs.g3i.2xlarge |ecs.g3i.2xlarge |
|Image type |Ubuntu 22.04 |Ubuntu 22.04 |
|Data volume specification |Data volume: 1000GiB \* 1 |\- |
|Instance quantity |1 |1 |


Refer to the table below to optimize configurations for the Server and the Client (perform optimization for the Client as needed) for optimal MySQL application performance.


|Optimization item |Configuration details |
|---|---|
|Partition volume |We recommend that when you partition a volume, set the starting cylinder value to ≥ 2048 and a multiple of 8. For detailed operations, refer to [Partitioning and formatting volumes](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the example provided in this topic, the volume is partitioned and mounted to the file system in <a href="https://docs.byteplus.com/en/docs/ecs/Testing-the-performance-of-MySQL-applications#.5q2l6aqk5LiA77yaU2VydmVy56uv6YOo572yTXlTUUzlupTnlKg=">Step 1</a>. You can skip this step.</div><br> |
|Install irqbalance\-ng |Follow the guide in [network interface interrupt binding](https://docs.byteplus.com/en/docs/ecs/Network-interface-interrupt-binding) to install irqbalance\-ng, which automatically configures interrupts for physical network interfaces. This helps enhance network performance. |
|Disable napi_tx |This feature is enabled by default only when the Linux kernel version is ≥ 5.3. You can execute the `uname -r` command to check the kernel version, and then disable napi_tx as follows.<br><br><br>* Ubuntu<br><br><br>```Plain Text```<br>```# Disable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=0 && systemctl restart systemd-networkd.service```<br>```# Enable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=1 && systemctl restart systemd-networkd.service```<br><br><br><br>* Debian<br><br><br>```Plain Text```<br>```# Disable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=0 && systemctl restart networking.service```<br>```# Enable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=1 && systemctl restart networking.service```<br><br><br><br>* CentOS<br><br><br>```Plain Text```<br>```# Disable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=0 && systemctl restart nmcli c reload```<br>```# Enable napi_tx:```<br>```rmmod virtio_net && modprobe virtio_net napi_tx=1 && systemctl restart nmcli c reload```<br><br><br>Execute the `cat /sys/module/virtio_net/parameters/napi_tx` command. If `N` is returned, napi_tx is disabled.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60a1a7b3dc0d834ae286b0f44c399dae.png) </span> |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Test results provided in this topic are for reference only and do not represent the actual optimal performance of an ECS instance.</div>


* <div data-tips="true" data-tips-type="tip">To avoid data loss, we recommend running performance tests on a newly created, data\-free instance with the guidance provided in this topic.</div>



<span id=".5q2l6aqk5LiA77yaU2VydmVy56uv6YOo572yTXlTUUzlupTnlKg="></span>
### Step 1: Deploy MySQL application on the Server


1. [Log in to the ECS instance serving as the Server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to create the install_mysql.sh script.

   `vim install_mysql.sh`

3. Press `i` key to enter edit mode, and then enter the content of the following file.

   > This file is used to install the MySQL application, partition the volume, mount the volume to a file system, and specify the MySQL persistent storage path on this file system.   
   

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a39540fb8b63927026c08bbde6b2ea0.sh" name="install_mysql.sh">install_mysql.sh</Attachment>
   

4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

5. Execute the following commands to run the script.

   `bash install_mysql.sh >> install_mysql.log`


<span id=".5q2l6aqk5LqM77yaQ2xpZW5056uv5a6J6KOFU3lzQmVuY2jlt6XlhbflubbliJvlu7rmtYvor5XohJrmnKw="></span>
### Step 2: Install Sysbench on the Client and create test scripts


1. [Log in to the ECS instance serving as the Client](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Install Sysbench.

   1. Execute the following command to create the install_sysbench.sh file.

      `vim install_sysbench.sh`

   2. Press `i` key to enter edit mode, and then enter the following content.

      ```Plain Text
      #!/bin/bash
      
      if which apt;then
          apt update
          apt-get install -y automake libtool pkg-config default-libmysqlclient-dev:amd64 
      elif which yum;then
          yum install -y libtool mysql-devel automake
      fi
      
      wget https://github.com/akopytov/sysbench/archive/1.0.19/sysbench-1.0.19.tar.gz
      tar xzvf sysbench-1.0.19.tar.gz
      
      cd sysbench-1.0.19/
      ./autogen.sh
      ./configure --with-mysql
      make -j8
      make install
      ```
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   4. Execute the following command to install Sysbench.

      `bash install_sysbench.sh`

3. Create the runtime script mysql_test_run.sh for testing.

   1. Execute the following command to create a runtime script for testing.

      `vim mysql_test_run.sh`

   2. Press `i` key to enter edit mode, and then enter the following content. Do not execute this script at this time.

      ```Plain Text
      #!/bin/bash
      
      dest_host=$serverIP
      thread_count=128
      
      VIRT_BENCHMARCK_TARGET=/usr/local
      VIRT_BENCHMARCK_OUTPUT=$(pwd)
      
      echo "------------------------------------------------"
      date
      echo "BENCHMARK PREPARE sysbench mysql ${dest_host} ${thread_count}"
      
      for MYSQLTEST in oltp_read_only oltp_write_only
      do
         $VIRT_BENCHMARCK_TARGET/bin/sysbench --mysql-host=${dest_host} --mysql-port=3306 --mysql-user=sbtest --mysql-password=sbpasswd $VIRT_BENCHMARCK_TARGET/share/sysbench/oltp_common.lua --tables=10 --table_size=100000 prepare > $VIRT_BENCHMARCK_OUTPUT/oltp_prepare.log
          echo "------------------------------------------------"
          
          echo "BENCHMARK STATR [$MYSQLTEST] ${dest_host} ${thread_count}"
          $VIRT_BENCHMARCK_TARGET/bin/sysbench --threads=${thread_count} --time=120 --report-interval=1 --mysql-host=${dest_host} --mysql-port=3306 --mysql-user=sbtest --mysql-password=sbpasswd $VIRT_BENCHMARCK_TARGET/share/sysbench/$MYSQLTEST.lua --tables=10 --table_size=100000 run > $VIRT_BENCHMARCK_OUTPUT/$MYSQLTEST.log
          
          echo "BENCHMARK RESULT [$MYSQLTEST] ${dest_host} ${thread_count}"
          grep -E "transactions:|queries:" $VIRT_BENCHMARCK_OUTPUT/$MYSQLTEST.log
          $VIRT_BENCHMARCK_TARGET/bin/sysbench --mysql-host=${dest_host} --mysql-port=3306 --mysql-user=sbtest --mysql-password=sbpasswd $VIRT_BENCHMARCK_TARGET/share/sysbench/oltp_common.lua --tables=10 --table_size=100000 cleanup > $VIRT_BENCHMARCK_OUTPUT/oltp_cleanup.log
          
          sleep 300s # Avoid MySQL's WAL mechanism affecting QPS test
      done
      ```
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

4. Create the script mysql_test_result.sh to obtain the test result.

   1. Execute the following command to create a script to obtain the result.

      `vim mysql_test_result.sh`

   2. Press `i` key to enter edit mode, and then enter the following content. Do not execute this script at this time.

      ```Plain Text
      #!/bin/bash
      VIRT_BENCHMARCK_OUTPUT=$(pwd)
      
      write_tps=$(grep -E "transactions:" $VIRT_BENCHMARCK_OUTPUT/oltp_write_only.log |awk '{print $3}')
      read_qps=$(grep -E "queries:" $VIRT_BENCHMARCK_OUTPUT/oltp_read_only.log |awk '{print $3}')
      
      echo "{\"mysql_write_tps\":"${write_tps:1}",\"mysql_read_qps\":"${read_qps:1}"}"
      ```
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.


<span id=".5q2l6aqk5LiJ77yaQ2xpZW5056uv5omn6KGM6ISa5pys5rWL6K-V5bm26I635Y-W57uT5p6c"></span>
### Step 3: Execute the test script on the Client and obtain the result


1. Obtain the **private IP address of the Server**, [log in to the Client](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance), and then execute the following command to run the test.

   > To obtain the private IP address of the Server, go to the Instances page in the ECS console, and then view it in the "Primary IPv4 address" column.   
   

   `serverIP=192.168.x.xx bash mysql_test_result.sh`

2. After the execution, execute the following command to obtain the test result.

   `bash mysql_test_result.sh`

   The output is shown below. "mysql_write_tps" indicates the TPS metric of MySQL in this test, and "mysql_read_qps" indicates the QPS metric of MySQL.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ade364e6c7a6ef7fd2fbdb3866444706.png) </span>

   After the test on the Client is completed, you can execute the following commands for detailed test results.

   * View QPS metric: `cat oltp_read_only.log`

   * View TPS metric: `cat oltp_write_only.log`

   In the example provided in this topic, oltp_read_only (QPS) is used. Below are the relevant metric descriptions.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_00f64106901d388d5e2bc6f655198684.jpg) </span>

   ```Plain Text
   SQL statistics:
       queries performed:
           read:                            49552244  // Total number of read requests executed, such as SELECT operations
           write:                           0         // Total number of write requests executed, such as UPDATE, INSERT, and DELETE operations
           other:                           7078892   // Total number of other requests executed, such as CREATE, DROP, and COMMIT operations
           total:                           56631136  // Total number of all requests executed
       transactions:                        3539446 (29492.41 per sec.)    // The former represents the total number of completed transactions, and the latter represents TPS (Transactions Per Second)
       queries:                             56631136 (471878.50 per sec.)  // The former represents the total number of completed queries, and the latter represents QPS (Queries Per Second)
       ignored errors:                      0      (0.00 per sec.)   // Number of errors that occurred and have been ignored
       reconnects:                          0      (0.00 per sec.)   // Number of request reconnection attempts
   
   General statistics:
       total time:                          120.0110s    // Test duration
       total number of events:              3539446      // Total number of events completed
   
   Latency (ms):
            min:                                    1.48  // Represents the shortest time taken to complete one event
            avg:                                    4.34  // Represents the average time taken to complete all events
            max:                                  210.23  // Represents the longest time taken to complete one event
            95th percentile:                        6.79  // Represents the time within which 95% of events were completed
            sum:                             15356801.48  // Represents the total time spent by all threads during the test
   
   Threads fairness:
       events (avg/stddev):           27651.9219/929.10  // The former represents the average number of events completed per thread, and the latter represents the standard deviation
       execution time (avg/stddev):   119.9750/0.00     // The former represents the average execution time per thread, and the latter represents the standard deviation
   ```
