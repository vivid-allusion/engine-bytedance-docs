---
title: "How do I fix pod health check failures?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-health-check-failed"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

The health checks in VKE clusters mainly include **readiness check (readinessProbe)**  and **liveness check (livenessProbe)** .


* If the readiness check fails, the system will remove the IP addresses of the pods from the Service. For application access via the Service, traffic will not be forwarded to pods that fail the readiness check.

* If the liveness check fails, kubelet will stop the containers and attempt to restart them.


A pod health check may fail for various reasons. In addition to application bugs that cause the pod to not respond to health check probes, resulting in the pod status being `unhealthy`, other factors may also be involved.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

A pod may fail the health check for the following reasons:


* Unreasonable health check configuration

* Overloaded nodes​

* Process port listening failure inside the container

* Too small SYN backlog size


<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

<span id=".5YGl5bq35qOA5p-l6YWN572u5LiN5ZCI55CG"></span>
### Unreasonable health check configuration

An improper health check configuration can lead to pod health check failures. For example, if the initial wait time `initialDelaySeconds` is too short and the container starts slowly, probing may begin before the container is fully started. In this case, if the failure threshold `failureThreshold` is set to 1, the pod will be stopped after a single health check failure, resulting in repeated stops and restarts of the pod.

<span id=".6IqC54K56LSf6L296L-H6auY"></span>
### Overloaded nodes​

High node load will prevent processes from obtaining sufficient CPU time slices, typically manifesting as network timeouts, health check failures, or service unavailability.

You can use the `top` command to determine the load average, and you can also identify which processes are consuming most resources by viewing data in the Cpu(s), Mem, %CPU, and %MEM columns. To do so, follow the steps below:


1. Log in to the node and run the `top` command to view the current node load. If the load is less than the number of CPUs, the node is considered to have low load. If the load is 2 to 3 times the number of CPUs, the node is considered to have high load. The following content provides a response example:

   ```Bash
   top - 19:42:06 up 23:59,  2 users,  load average: 34.64, 35.80, 35.76
   Tasks: 679 total,   1 running, 678 sleeping,   0 stopped,   0 zombie
   Cpu(s): 15.6%us,  1.7%sy,  0.0%ni, 74.7%id,  7.9%wa,  0.0%hi,  0.1%si,  0.0%st
   Mem:  32865032k total, 30989168k used,  1875864k free,   370748k buffers
   Swap:  8388604k total,     5440k used,  8383164k free,  7982424k cached
   
     PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
    9783 mysql     20   0 17.3g  16g 8104 S 186.9 52.3   3752:33 mysqld
    6540 nginx     20   0 1306m  40m 7884 S  3.3  0.1   0:02.46 php-fpm
    5553 nginx     20   0 1300m  36m 9568 S  3.0  0.1   0:21.58 php-fpm
    5722 nginx     20   0 1310m  45m 8552 S  3.0  0.1   0:17.25 php-fpm
    5920 nginx     20   0 1302m  36m 8208 S  3.0  0.1   0:14.23 php-fpm
    6432 nginx     20   0 1310m  45m 8420 S  3.0  0.1   0:05.86 php-fpm
    5285 nginx     20   0 1302m  38m 9696 S  2.7  0.1   0:23.41 php-fpm
   ```
   

2. If the load is high but CPU usage is not high, this is typically caused by too many processes or threads running simultaneously.

   * Use the following command to view the current number of PIDs. If the number of PIDs is excessively large, you can briefly review which processes are running. If many processes are created by identical startup commands, this issue may be caused by a bug in the program corresponding to these processes.

      ```bash
      ps -eLf | wc -l
      
      ```
      

   * You can also use the following command to rank processes by thread count. Processes with a high thread count may experience thread leaks, which result in PID exhaustion.

      ```bash
      printf "NUM\tPID\tCOMMAND\n" && ps -eLf | awk '{$1=null;$3=null;$4=null;$5=null;$6=null;$7=null;$8=null;$9=null;print}' | sort |uniq -c |sort -rn | head -10
      ```
      

3. In the output of the `top` command, you can view the `wa` value for CPU cores. This value represents the percentage of time that the CPU remains idle while waiting for pending disk I/O operations to complete. Press the 1 key on the keyboard to view the `wa` value for each core, as shown below.

   ```bash
   top - 19:42:08 up 23:59,  2 users,  load average: 34.64, 35.80, 35.76
   Tasks: 679 total,   1 running, 678 sleeping,   0 stopped,   0 zombie
   Cpu0  : 29.5%us,  3.7%sy,  0.0%ni, 48.7%id, 17.9%wa,  0.0%hi,  0.1%si,  0.0%st
   Cpu1  : 29.3%us,  3.7%sy,  0.0%ni, 48.9%id, 17.9%wa,  0.0%hi,  0.1%si,  0.0%st
   Cpu2  : 26.1%us,  3.1%sy,  0.0%ni, 64.4%id,  6.0%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu3  : 25.9%us,  3.1%sy,  0.0%ni, 65.5%id,  5.4%wa,  0.0%hi,  0.1%si,  0.0%st
   Cpu4  : 24.9%us,  3.0%sy,  0.0%ni, 66.8%id,  5.0%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu5  : 24.9%us,  2.9%sy,  0.0%ni, 67.0%id,  4.8%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu6  : 24.2%us,  2.7%sy,  0.0%ni, 68.3%id,  4.5%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu7  : 24.3%us,  2.6%sy,  0.0%ni, 68.5%id,  4.2%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu8  : 23.8%us,  2.6%sy,  0.0%ni, 69.2%id,  4.1%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu9  : 23.9%us,  2.5%sy,  0.0%ni, 69.3%id,  4.0%wa,  0.0%hi,  0.3%si,  0.0%st
   Cpu10 : 23.3%us,  2.4%sy,  0.0%ni, 68.7%id,  5.6%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu11 : 23.3%us,  2.4%sy,  0.0%ni, 69.2%id,  5.1%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu12 : 21.8%us,  2.4%sy,  0.0%ni, 60.2%id, 15.5%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu13 : 21.9%us,  2.4%sy,  0.0%ni, 60.6%id, 15.2%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu14 : 21.4%us,  2.3%sy,  0.0%ni, 72.6%id,  3.7%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu15 : 21.5%us,  2.2%sy,  0.0%ni, 73.2%id,  3.1%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu16 : 21.2%us,  2.2%sy,  0.0%ni, 73.6%id,  3.0%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu17 : 21.2%us,  2.1%sy,  0.0%ni, 73.8%id,  2.8%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu18 : 20.9%us,  2.1%sy,  0.0%ni, 74.1%id,  2.9%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu19 : 21.0%us,  2.1%sy,  0.0%ni, 74.4%id,  2.5%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu20 : 20.7%us,  2.0%sy,  0.0%ni, 73.8%id,  3.4%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu21 : 20.8%us,  2.0%sy,  0.0%ni, 73.9%id,  3.2%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu22 : 20.8%us,  2.0%sy,  0.0%ni, 74.4%id,  2.8%wa,  0.0%hi,  0.0%si,  0.0%st
   Cpu23 : 20.8%us,  1.9%sy,  0.0%ni, 74.4%id,  2.8%wa,  0.0%hi,  0.0%si,  0.0%st
   Mem:  32865032k total, 30209248k used,  2655784k free,   370748k buffers
   Swap:  8388604k total,     5440k used,  8383164k free,  7986552k cached
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>wa</code> value should typically be 0%. If it frequently fluctuates above 1%, it indicates that the storage device speed cannot keep up with the CPU processing speed.   </div>
   

4. Use the `atop` command to view the current disk I/O status. In this example, the disk vda is 100% busy, indicating a serious performance bottleneck has been reached.

   ```Plain Text
   PRC | sys    0.61s  | user   0.73s |  #proc    282 |  #trun      1 | #tslpi   872  | #tslpu   103 |  #zombie    0 |  #exit     92 |
   CPU | sys       6%  | user      7% |  irq       0% |  idle   1589% | wait      0%  | steal     0% |  guest     0% |  curf 2.39GHz |
   CPL | avg1    0.10  | avg5    0.10 |  avg15   0.08 |               | csw    79864  | intr   51369 |               |  numcpu    16 |
   MEM | tot    62.4G  | free   44.1G |  cache  15.8G |  dirty   0.2M | buff  709.1M  | slab  909.4M |  shrss   0.0M |  numnode    1 |
   SWP | tot     0.0M  | free    0.0M |  swcac   0.0M |               |               |              |  vmcom   4.5G |  vmlim  31.2G |
   NUM | tot    62.4G  | free   44.1G |  file   16.5G |  numanode0000 | activ   2.0G  | inact  15.2G |  slab  909.4M |  frag      0% |
   PSI | cpusome   0%  | memsome   0% |  memfull   0% |  iosome    0% | iofull    0%  | cs     1/3/8 |  ms     0/0/0 |  is     0/0/0 |
   DSK |          vda  | busy    100% |  read       0 |  write     17 | KiB/w      7  | MBr/s    0.0 |  MBw/s    2.8 |  avio 0.18 ms |
   DSK |          vdb  | busy      0% |  read       0 |  write     13 | KiB/w      6  | MBr/s    0.0 |  MBw/s    0.0 |  avio 0.23 ms |
   NET | transport     | tcpi    3252 |  tcpo    9626 |  udpi       1 | udpo       1  | tcpao     19 |  tcppo     15 |  tcprs      0 |
   NET | network       | ipi     3727 |  ipo     9892 |  ipfrw    221 | deliv   3253  |              |  icmpi      0 |  icmpo      0 |
   NET | eth0    ----  | pcki    3513 |  pcko    9656 |  sp    0 Mbps | si  311 Kbps  | so 1339 Kbps |  erri       0 |  erro       0 |
   
       PID  SYSCPU  USRCPU  RDELAY   VGROW   RGROW   RDDSK   WRDSK  RUID      EUID      ST  EXC   THR  S  CPUNR    CPU  CMD        1/5
      2693   0.06s   0.18s   0.05s      0B  760.0K      0B      0B  root      root      --    -    29  S     14     2%  php-fpm
     69735   0.11s   0.12s   0.01s      0B      0B      0B      0B  root      root      --    -     1  R      5     2%  php-fpm
     63223   0.08s   0.04s   0.00s      0B      0B      0B      0B  root      root      --    -     1  S      2     1%  php-fpm
      2464   0.03s   0.06s   0.06s      0B  264.0K      0B   12.0K  root      root      --    -    27  S     13     1%  php-fpm
   3064644   0.02s   0.04s   0.00s      0B      0B      0B      0B  root      root      --    -    21  S     14     1%  php-fpm
   3622214   0.03s   0.02s   0.00s   92.0K      0B      0B   28.0K  root      root      --    -     1  S     15     1%  php-fpm
     55040   0.04s   0.00s   0.00s      0B      0B      0B      0B  root      root      --    -     1  I      6     0%  php-fpm
   3064483   0.01s   0.02s   0.00s      0B   -0.1M      0B      0B  root      root      --    -    13  S     13     0%  php-fpm
      1043   0.02s   0.01s   0.01s      0B      0B      0B      0B  unscd     unscd     --    -     1  S      1     0%  php-fpm
     59090   0.03s   0.00s   0.00s      0B      0B      0B      0B  root      root      --    -     1  I      2     0%  php-fpm
   3034537   0.01s   0.01s   0.00s      0B      0B      0B      0B  root      root      --    -    27  S      4     0%  php-fpm
      6331   0.01s   0.01s   0.00s      0B      0B      0B      0B  root      root      --    -    22  S     13     0%  php-fpm
   ```
   


<span id=".5a655Zmo5YaF6L-b56iL56uv5Y-j55uR5ZCs5pWF6Zqc"></span>
### Process port listening failure inside the container

Use the `netstat -tunlp` command to check whether the listening ports inside the container are functioning properly. If they are not functioning properly, the health check will fail. The example is as follows:

```bash
20:15:17.890996 IP 172.16.2.1.38074 > 172.16.2.23.8888: Flags [S], seq 96880261, win 14600, options [mss 1424,nop,nop,sackOK,nop,wscale 7], length 0
20:15:17.891021 IP 172.16.2.23.8888 > 172.16.2.1.38074: Flags [R.], seq 0, ack 96880262, win 0, length 0
20:15:17.906744 IP 10.0.0.16.54132 > 172.16.2.23.8888: Flags [S], seq 1207014342, win 14600, options [mss 1424,nop,nop,sackOK,nop,wscale 7], length 0
20:15:17.906766 IP 172.16.2.23.8888 > 10.0.0.16.54132: Flags [R.], seq 0, ack 1207014343, win 0, length 0
```


Connection anomalies will trigger health check failures. This situation may arise when multiple pods using hostNetwork to listen on the same host port are deployed on a single node. Only one pod can successfully bind to the port. If the business logic of the pods that fail to bind allows failure and does not terminate the process, and health checking is configured for these pods, kubelet will send health check probe packets to them. Since these pods are not listening on the target port, their health checks will fail.

<span id=".c3luLWJhY2tsb2ct6K6-572u6L-H5bCP"></span>
### Too small SYN backlog size

The SYN backlog size refers to the SYN queue size. If many new connections are initiated in a short time and the SYN backlog size is too small, new connection attempts will fail. Use the `netstat -s | grep TCPBacklogDrop` command to view how many new connections were dropped due to a full backlog.

If packet loss is confirmed to be caused by a full backlog, we recommend increasing the backlog size by modifying the kernel parameter `net.ipv4.tcp_max_syn_backlog`.
