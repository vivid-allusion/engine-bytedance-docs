---
title: "Testing Nginx performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Testing-the-performance-of-NGINX"
---

To learn the network performance of your ECS instance, you may typically analyze requests completed per second of the Nginx service (for long and short connections). This topic describes a test plan to obtain the optimal Nginx performance of ECS instances.

## ​Testing tools and versions

In this topic, the Nginx service is deployed on the Server, and the Wrk pressure testing tool is deployed on the Client.

* Nginx: A high\-performance, lightweight web server for HTTP services and reverse proxy. This topic uses Nginx 1.18.0 as an example.

* Wrk: A lightweight HTTP benchmarking tool. This topic uses wrk [epoll] Copyright (C) 2012 Will Glozer as an example.

## Test metric

`Requests/sec`: The average number of requests completed per second. The higher this value, the better the Nginx performance.

## Test environment

Two ECS instances with the same specifications are used, which serve as the service side (Server) and client side (Client), respectively. The specific configuration is shown in the table below.

> To create an instance, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

|Sample configuration |Server |Client |
|---|---|---|
|Instance type |ecs.g3i.2xlarge |ecs.g3i.2xlarge |
|Image type |Ubuntu 22.04 |Ubuntu 22.04 |
|Instance quantity |1 |1 |

## Procedure

### Step 1: Deploy and start the Nginx service on the Server

1. [Log in to the ECS instance serving as the Server](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Deploy the Nginx service.

   1. Execute the following command to create an Nginx deployment file.

      `vim nginx_install.sh`

   2. Press `i` key to enter edit mode, and then enter the following content.

      ```Bash
      #!/bin/bash
      # install nginx
      if which yum; then
          rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
          yum -y install nginx
      elif which apt; then
          apt update
          apt -y install nginx
      fi
      
      # close accesslog
      mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.origin
      sed "/ *access_log.*/c\access_log off;" /etc/nginx/nginx.conf.origin > /etc/nginx/nginx.conf
      
      # prepare demo file
      html_dir=$(grep root /etc/nginx/nginx.conf |grep -v "#"|awk '{print $2}'|sed "s/;//")
      if [ ! ${html_dir} ];then
          html_dir=$(grep root /etc/nginx/sites-available/default|grep -v "#"|awk '{print $2}'|sed "s/;//")
      fi
      echo "nginx html dir is ${html_dir}"
      
      cd ${html_dir}
      dd if=/dev/urandom of=1k bs=1k count=1
      dd if=/dev/urandom of=4k bs=4k count=1
      dd if=/dev/urandom of=1M bs=1M count=1
      echo "hello">hello
      
      echo "install and prepare nginx finish"
      nginx -v
      ```

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   4. Execute the following command to install Nginx.

      `bash nginx_install.sh`

3. Start the Nginx service on the Server.

   1. Execute the following command to create a run file "nginx_run.sh".

      `vim nginx_run.sh`

   2. Press `i` key to enter edit mode, and then enter the following content.

      ```Bash
      #!/bin/bash
      # run 
      # change ulimit
      ulimit -n 65535
      ulimit -n
      # start nginx service
      systemctl stop nginx
      systemctl start nginx
      systemctl status nginx
      echo "start nginx finish"
      ```

   3. Execute the following command to start the Nginx service.

      `bash nginx_run.sh`

### Step 2: Optimize instance configurations for optimal Nginx performance (optional)

For detailed items and steps, refer to [Optimal configuration](https://docs.byteplus.com/en/docs/ecs/Testing-the-performance-of-NGINX#.5pyA5L2z6YWN572u).

### Step 3: Deploy Wrk on the Client and create a test script

1. [Log in to the ECS instance serving as the Client](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Deploy Wrk.

   1. Execute the following command to create a Wrk deployment file.

      `vim wrk_install.sh`

   2. Press `i` key to enter edit mode, and then enter the following content.

      ```Bash
      #!/bin/bash
      
      if which wrk; then echo 'wrk is already installed' && exit; fi
      
      if which yum;then yum install -y unzip python3; elif which apt ; then apt update && apt -y install unzip python3; fi
      
      cd $(dirname $0)
      #install wrk
      while true
      do
          wget https://github.com/wg/wrk/archive/refs/heads/master.zip && break
      done
      unzip master.zip
      cd wrk-master/
      make
      cp wrk /usr/bin/
      whereis wrk
      ```

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   4. Execute the following command to install Wrk.

      `bash wrk_install.sh`

3. Create the test script wrk_run.sh.

   1. Execute the following command to create the test script.

      `vim wrk_run.sh`

   2. Press `i` key to enter edit mode, and then enter the following content.

      ```Bash
      #!/bin/bash
      
      ulimit -n 65535
      
      if [ $# -lt 1 ]; then
         echo 'Usage: bash wrk_run.sh $serverIP [$threadNums] [$connNums]'
         exit
      elif [ $# -gt 3 ]; then
         echo 'Usage: bash wrk_run.sh $serverIP [$threadNums] [$connNums]'
         echo "Error: The number of parameters must be between 1-3"
         exit
      fi
      
      dest_host=$1
      if [ $# -eq 2 ]; then
         wrk_thread=$2
      elif [ $# -eq 3 ]; then
         wrk_thread=$2
         wrk_conn=$3
      fi
      
      if [ ! ${wrk_thread} ];then wrk_thread=128; fi
      if [ ! ${wrk_conn} ];then wrk_conn=1024; fi
      
      for data in hello
      do
      
          # long connection
          echo "$(date) BENCHMARK STATR to stress nginx_long_ops[$data] with wrk ${dest_host} ${wrk_thread} ${wrk_conn} "
          wrk -t ${wrk_thread} -c ${wrk_conn} -d 60 http://${dest_host}/$data
          echo ""
      
          # short connection
          echo "$(date) BENCHMARK STATR to stress nginx_short_ops[$data] with wrk ${dest_host} ${wrk_thread} ${wrk_conn} "
          wrk -t ${wrk_thread} -c ${wrk_conn} -d 60 -H "Connection: close" http://${dest_host}/$data
      done;
      ```

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

### Step 4: Run the test script on the Client and obtain results

1. Obtain the **private IP address** of the Server, and then execute the following command on the Client to run the test.

   `bash wrk_run.sh <serverIP> <threadNums> <connNums>`

   > * serverIP (required): Indicates the private IP address of the Server. To obtain the private IP address, go to the Instances page in the ECS console, and then view it in the "Primary IPv4 address" column.

   > * threadNums (optional): Indicates the number of threads to be created. Default value: 128.

   > * connNums (optional): Indicates the number of connections to be created. Default value: 1,024.

   The test results are as follows. Pay attention to the `Requests/sec` metric, because it indicates the average number of requests completed per second. The higher this value, the better the Nginx performance.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c514b3a7a5444dba721118921c2949e.png)

   Detailed result descriptions are as follows.

   ```Bash
   Tue Apr 25 02:50:05 PM CST 2023 BENCHMARK STATR to stress nginx_long_ops[hello] with wrk $serverIP 128 1024
   Running 1m test @ http://$serverIP/hello
     128 threads and 1024 connections (Total 128 threads, 1024 connections)
     Thread Stats   Avg      Stdev     Max   +/- Stdev
                  (Mean) (Standard Deviation) (Maximum Value) (Proportion within Standard Deviation)
       Latency     1.03ms  182.06us  19.56ms   95.21%
       (Latency)
       Req/Sec     7.83k   550.46    37.53k    99.67%
      (Requests per Second)
     59976763 requests in 1.00m, 14.74GB read (Total runtime 1 minute, completed 59,976,763 requests, read 14.74GB of data)
   Requests/sec: 997958.48
    (Average requests completed per second)
   Transfer/sec:    251.21MB
    (Average bytes transferred per second)
   ```

## Optimal configuration

Multiple factors can impact Nginx performance, such as parameter configurations of the Nginx service, kernel parameters, and network card queues. To optimize your ECS instance configurations for optimal Nginx performance, refer to the instructions below.

### Disable napi_tx

Disabling napi_tx can reduce the number of hardware and software interrupts when the network interface transmits packets. As a result, Nginx performance can be improved.

This feature is enabled by default only when the Linux kernel version is ≥ 5.3. You can execute the `uname -r` command to check the kernel version, and then disable napi_tx as follows.

* Ubuntu

   ```Bash
   # Disable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=0 && systemctl restart systemd-networkd.service
   # Enable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=1 && systemctl restart systemd-networkd.service
   ```

* Debian

   ```Bash
   # Disable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=0 && systemctl restart networking.service
   # Enable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=1 && systemctl restart networking.service
   ```

* CentOS

   ```Bash
   # Disable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=0 && nmcli c reload
   # Enable napi_tx:
   rmmod virtio_net && modprobe virtio_net napi_tx=1 && nmcli c reload
   ```

Execute the `cat /sys/module/virtio_net/parameters/napi_tx` command. If `N` is returned, napi_tx is disabled successfully.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60a1a7b3dc0d834ae286b0f44c399dae.png)

### Mitigate contention issues

For large\-specification instances, contention issues may occur due to the increased number of CPU cores and thereby impact Nginx performance. These mainly include contention for HTML files and socket contention. Below are solutions for these two types of contention to improve Nginx performance.

#### Solution 1: Modify the number of Nginx worker processes and enable reuseport

After deploying the Nginx service on the Server, you can enable the Nginx reuseport option to allow multiple sockets to listen on the same port to mitigate contention. Or, specify an appropriate number of Nginx worker processes when HTML files are being accessed to improve Nginx performance. The optimal number of Nginx worker processes varies by instance specification, with details shown below.

|Instance type |Optimal number of Nginx worker processes for long connections |Optimal number of Nginx worker processes for short connections |
|---|---|---|
|ecs.g3i.2xlarge (8 vCPU) |8 |8 |
|ecs.g3i.8xlarge (32 vCPU) |12 |6 |
|ecs.g3i.16xlarge (64 vCPU) |13 |13 |

To modify the number of Nginx worker processes and enable reuseport, follow these steps:

1. Execute the following command to open the /etc/nginx/nginx.conf configuration file.

   `vim /etc/nginx/nginx.conf`

2. Press `i` to enter the edit mode.

3. Modify the number of Nginx worker processes and enable reuseport.

   1. Modify the value of `worker_processes` based on the specification.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4714d50e766a2542ff21bcff2fc14a54.png)

   2. Add the following content to the end of the configuration file to enable reuseport.

      ```JSON
      http{
              server{
                      listen 80 reuseport;
                      listen [::]:80 reuseport;
              }
      }
      ```

4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

5. Execute the following command to restart the Nginx service and apply the configuration.

   `systemctl restart nginx.service`

#### Solution 2: Install irqbalance\-ng

You can follow the guide in [network interface interrupt binding](https://docs.byteplus.com/en/docs/ecs/Network-interface-interrupt-binding) to install irqbalance\-ng, which automatically configures interrupts for physical network interfaces. This enables interrupt load balancing and thereby enhances network performance.

### Disable sniffer

1. Execute the following command to check whether sniffer is enabled.

   `cat /proc/net/ptype`

   * If the following output is displayed, the sniffer is not enabled. Then, skip this step.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_468a79da60ce7add14cf1d2c9b52ed91.jpg)

   * If the following output is displayed, sniffer is enabled. Proceed to the next step.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca738fd4c91f778f600dbbb30c4776bf.jpg)

2. Execute the following command to check if the dhclient process is present.

   `ps aux | grep dhclient`

   The output is displayed below, which indicates that the dhclient process is present. Execute the following command to terminate the dhclient process and thus disable the sniffer.

   `kill -9 <process_id>`

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc6372badfbc77dbc0965da5a8f4c9da.jpg)
