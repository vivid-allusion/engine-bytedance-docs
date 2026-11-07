---
title: "Test tool"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Test_tool"
---

SysBench is a cross\-platform and multi\-threaded modular benchmarking tool for evaluating the performance of a system on core parameters when running a high\-load database.

<span id="下载安装测试工具"></span>
## Download and install the test tool

Execute the following command on ECS to complete the download and installation of SysBench. The selected version of SysBench is 1.0.18.

```bash
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysqlgit clone https://github.com/akopytov/sysbench.git##Download sysbench from Gitcd sysbench##Open the sysbench directorygit checkout 1.0.18##Switch to sysbench version 1.0.18./autogen.sh##Run autogen.sh ./configure --prefix=/usr --mandir=/usr/share/manmake##Compile make install
```


<span id="修改-ecs-参数"></span>
#### Modify ECS parameters

Execute the following command to configure the SysBench client so that the kernel can process data packets with all CPU cores (default is 2 cores), while reducing context switching between CPU cores.

```bash
sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>fffffff</code> means 32 cores are used. Please modify according to the actual configuration, for example, ECS is 8 cores, you need to replace it with <code>ff</code>.</div>


```bash
sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"
```
