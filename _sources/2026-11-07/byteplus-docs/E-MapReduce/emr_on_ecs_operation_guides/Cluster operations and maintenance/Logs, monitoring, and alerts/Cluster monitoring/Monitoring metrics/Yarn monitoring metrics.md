---
title: "Yarn monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_Yarn_monitoring_metrics"
---

This article provides detailed information about Yarn metrics.

The Yarn metrics include the following sections:


* [YARN-Overview](https://docs.byteplus.com/docs/E-MapReduce/105468#yarn-%E6%A6%82%E8%A7%88)

* [YARN-Queues](https://docs.byteplus.com/docs/E-MapReduce/105468#yarn-queues)

* [YARN-ResourceManager](https://docs.byteplus.com/docs/E-MapReduce/105468#yarn-resourcemanager)

* [YARN-NodeManager](https://docs.byteplus.com/docs/E-MapReduce/105468#yarn-nodemanager)

* [YARN-TimeLineSever](https://docs.byteplus.com/docs/E-MapReduce/105468#yarn-timelinesever)


<span id="yarn-概览"></span>
## **YARN\-Overview**


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|Number of nodes |Current number of active NodeManagers |count |
||Current number of decommissioned NodeManagers |count |
||Current number of NodeManagers in NumDecommissioningNMs |count |
||Current number of lost NodeManagers |count |
||Current number of unhealthy NodeManagers |count |
|Memory |Allocated memory resources in the cluster |MB |
||Available memory resources in the cluster |MB |
||Reserved memory resources in the cluster |MB |
||Total memory resources in the cluster |MB |
|Applications |Number of jobs completed in the cluster during the sampling period |count |
||Number of jobs failed in the cluster during the sampling period |count |
||Number of jobs killed in the cluster during the sampling period |count |
||Number of jobs pending in the cluster during the sampling period |count |
||Number of jobs running in the cluster during the sampling period |count |
||Number of jobs submitted in the cluster during the sampling period |count |
|Containers |Number of allocated containers in the cluster |count |
||Number of requested containers in the cluster |count |
||Number of reserved containers in the cluster |count |
|Memory usage |Current memory resource usage rate in the cluster |% |
|Cores |Allocated CPU resources in the cluster |count |
||Available CPU resources in the cluster |count |
||Reserved CPU resources in the cluster |count |
||Total CPU resources in the cluster |count |
|CPU usage |Current CPU resource usage rate in the cluster |% |
|Number of AM launches |Number of AM launches |count |
|Average time for RM to launch AM |Average time for RM to launch AM |ms |
|Total number of registered AMs |Total number of registered AMs |count |
|Average time for AM to register with RM |Average time for AM to register with RM |ms |


<span id="yarn-queues"></span>
## **YARN\-Queues**

Included in the overview


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|Number of CPU cores |Number of VCore allocated in the current queue |Core |
||Number of reserved VCore in the current queue |core |
||Number of available VCore in the current queue |core |
||Number of pending VCore in resource requests of the current queue |core |
|Total number of applications |Number of historical Submit Job entries in the current queue |count |
||Number of running jobs in the current queue |count |
||Number of pending jobs in the current queue |count |
||Number of completed jobs in the current queue |count |
||Number of killed jobs in the current queue |count |
||Number of failed jobs in the current queue |count |
||Number of active jobs in the current queue |count |
||Number of jobs in the current queue with runtime less than 60 minutes |count |
||Number of jobs in the current queue with runtime between 60 and 300 minutes |count |
||Number of jobs in the current queue with runtime between 300 and 1440 minutes |count |
||Number of jobs in the current queue with runtime greater than 1440 minutes |count |
|Memory size |Memory size allocated to the current queue |MB |
||Available memory size in the current queue |MB |
||Pending memory size in resource requests for the current queue |MB |
||Reserved memory size in the current queue |MB |
|Container count |Number of containers allocated to the current queue |count |
||Pending container count in resource requests for the current queue |count |
||Reserved container count in the current queue |count |
|Total container allocation and release |Total number of containers allocated to the current queue |count |
||Total number of containers released from the current queue |count |
||Total number of containers preempted in the current queue |count |
|User count |Number of active users in the current queue |count |


<span id="yarn-resourcemanager"></span>
## **YARN\-ResourceManager**


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|RPC authentication and authorization count |Number of failed RPC authentication attempts |count |
||Number of successful RPC authentication attempts |count |
||Number of failed RPC authorization attempts |count |
||Number of successful RPC authorization attempts |count |
|RPC data received and sent |RPC data received |bytes/s |
||RPC data sent |bytes/s |
|RPC connection count |Number of currently open connections |count |
|RPC request count |RPC request count |times |
||RPC queue request count |times |
|RPC queue length |Current RPC queue length |count |
|RPC average processing time |Average RPC request processing time |s |
||Average time in RPC queue |s |
|GC count |Young GC count |times |
||Full GC count |times |
|GC time |Full GC elapsed time |s |
||Garbage collection elapsed time |s |
||Young GC elapsed time |s |
|Memory region usage ratio |Survivor 0 region memory usage ratio |% |
||Eden region memory usage ratio |% |
||Compressed class space region memory usage ratio |% |
||Survivor 1 region memory usage ratio |% |
||Old region memory usage ratio |% |
||Metaspace region memory usage ratio |% |
|JVM thread count |Number of threads in NEW state |count |
||Number of threads in RUNNABLE state |count |
||Number of threads in BLOCKED state |count |
||Number of threads in WAITING state |count |
||Number of threads in TIMED WAITING state |count |
||Number of threads in Terminated state |count |
|JVM log count |Fatal log count |count |
||Error log count |count |
||Warn log count |count |
||Info log count |count |
|JVM memory |Non\-heap memory used by the process |MB |
||Non\-heap memory committed by the process |MB |
||Heap memory used by the process |MB |
||Heap memory committed by the process |MB |
||Maximum heap memory size of the process |MB |
||Maximum memory size of the process |MB |
|CPU utilization |CPU utilization |% |
|CPU cumulative usage time |CPU cumulative usage time |ms |
|File descriptor count |Maximum file descriptor count |count |
||Open file descriptor count |count |
|Process runtime duration |Process runtime duration |s |
|Worker thread count |Number of daemon threads in the process |count |
||Number of threads in the process |count |


<span id="yarn-nodemanager"></span>
## **YARN\-NodeManager**


|**Dimension** |**metric name** |**Unit** |
|---|---|---|
|GC count |Young GC count |times |
||Full GC count |times |
|GC time |Full GC elapsed time |s |
||Garbage collection elapsed time |s |
||Young GC elapsed time |s |
|Memory region usage ratio |Survivor 0 region memory usage ratio |% |
||Eden region memory usage ratio |% |
||Compressed class space region memory usage ratio |% |
||Survivor 1 region memory usage ratio |% |
||Old region memory usage ratio |% |
||Metaspace region memory usage ratio |% |
|JVM thread count |Number of threads in NEW state |count |
||Number of threads in RUNNABLE state |count |
||Number of threads in BLOCKED state |count |
||Number of threads in WAITING state |count |
||Number of threads in TIMED WAITING state |count |
||Current number of threads in TERMINATED state |count |
|JVM log count |FATAL level log count |count |
||ERROR level log count |count |
||WARN level log count |count |
||INFO level log count |count |
|JVM memory |Non\-heap memory used by the process |MB |
||Non\-heap memory committed by the process |MB |
||Heap memory used by the process |MB |
||Heap memory committed by the process |MB |
||Maximum heap memory size of the process |MB |
||Maximum memory size of the process |MB |
|Total number of containers |Number of launched containers |count |
||Number of containers completed |count |
||Number of failed containers |count |
||Number of killed containers |count |
||Number of containers initializing |count |
||Number of containers running |count |
||Number of containers allocated by NodeManager |count |
|Average container startup time |Average container startup time |ms |
|Number of container startup operations |Number of container startup operations |count |
|Number of CPU cores |Number of available VCore in NodeManager |core |
||Number of VCore allocated by NodeManager |core |
|Memory size |Memory size allocated by NodeManager |GB |
||Memory size available in NodeManager |GB |
|CPU utilization |CPU utilization |% |
|CPU cumulative usage time |CPU cumulative usage time |ms |
|File descriptor count |Maximum file descriptor count |count |
||Open file descriptor count |count |
|Process runtime duration |Process runtime duration |s |
|Worker thread count |Process daemon thread count |count |
||Process thread count |count |


<span id="yarn-timelinesever"></span>
## **YARN\-TimeLineSever**


|**Title** |**Description** |**Unit** |
|---|---|---|
|JVM memory usage |TimelineServer non\-heap space usage |MB |
||TimelineServer non\-heap space committed amount |MB |
||TimelineServer non\-heap space maximum value |MB |
||TimelineServer heap space usage |MB |
||TimelineServer heap space committed amount |MB |
||TimelineServer heap space maximum value |MB |
||TimelineServer maximum memory value |MB |
|GC status |TimelineServer GC count |count |
||TimelineServer GC duration |ms |
|Operation frequency |TimelineServer GetEntities operation frequency |operations per second |
||TimelineServer GetEntity operation frequency |operations per second |
||TimelineServer GetEvents operation frequency |operations per second |
||TimelineServer PostEntities operation frequency |operations per second |
||TimelineServer GetDomain operation frequency |operations per second |
||TimelineServer PutDomain operation frequency |operations per second |
||TimelineServer GetDomains operation frequency |operations per second |
|Average operation time |TimelineServer GetEntities average operation time |ms |
||TimelineServer GetEntity average operation time |ms |
||TimelineServer GetEvents average operation time |ms |
||TimelineServer PostEntities average operation time |ms |
||TimelineServer GetDomain average operation time |ms |
||TimelineServer PutDomain average operation time |ms |
||TimelineServer GetDomains average operation time |ms |
