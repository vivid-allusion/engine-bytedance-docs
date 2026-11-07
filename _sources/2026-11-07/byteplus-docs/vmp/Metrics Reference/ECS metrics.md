---
title: "ECS metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ecs-metrics"
---

When you purchase and create an ECS instance in the BytePlus console, `cloud-monitor-agent` is built into the public image used to create the instance, enabling monitoring for the ECS instance. This topic describes common ECS metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more metrics of ECS instances, refer to <a href="https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric&namespace=VCM_ECS">Cloud Monitor metric queries</a>.</div>


<span id="CPU"></span>
## CPU


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|CPU utilization |CpuTotal |% |The total CPU utilization. |
||DDHInstanceCpuTotal |% |The CPU utilization of a Dedicated Host (DDH) instance. |
|CPU load |LoadPerCore15m |\- |The average load of a core per 15 minutes. |
||LoadPerCore1m |\- |The average load of a core per minute. |
||LoadPerCore5m |\- |The average load of a core per 5 minutes. |


<span id=".5YaF5a2Y"></span>
## Memory


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|Memory |MemoryUsedSpace |Bytes |The used memory. |
||MemoryUsedUtilization |% |The utilization of used memory. |


<span id=".5a2Y5YKo"></span>
## Storage


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|Storage |DiskInodesUsedPercent |% |The disk inode utilization. |
||DiskReadBytes |Bytes/s |The number of bytes read by a disk per second. |
||DiskReadIops |\- |The number of input/output operations read by a disk per second. |
||DiskTotal |Bytes |The total disk capacity. |
||DiskUsageAvail |Bytes |The available capacity of a disk. |
||DiskUsageUtilization |% |The disk utilization. |
||DiskUsed |Bytes |The used capacity of a disk. |
||DiskWriteBytes |Bytes/s |The number of bytes written by a disk per second. |
||DiskWriteIops |\- |The IOPS written by a disk per second. |


<span id=".572R57uc"></span>
## Network


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|Host NIC |NetworkInDrop |\- |The number of discarded inbound network packets. |
||NetworkInErrorPackages |\- |The number of inbound network packets in error. |
||NetworkInPackages |Packet/s |The inbound network packet rate. |
||NetworkInRate |Bits/s |The inbound network traffic rate. |
||NetworkOutDrop |\- |The number of discarded outbound network packets. |
||NetworkOutErrorPackages |\- |The number of outbound network packets in error. |
||NetworkOutPackages |\- |The number of outbound network packets. |
||NetworkOutRate |Bits/s |The outbound network traffic rate. |
||EthMTU |\- |The maximum transmission unit (MTU) of a network interface card (NIC). |
|Transport layer (TCP/UDP) |NetTcpConnection |\- |The number of TCP connections. |
||NetTcpConnectionStatus |\- |The number of TCP connections in different states. |
||TCPInSegs |Packet |The number of TCP packets received per minute. |
||TCPOutSegs |Packet |The number of TCP packets sent per minute. |


<span id=".6L-b56iL"></span>
## Process


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|Process |ProcessCPUPct |% |The process CPU utilization. |
||ProcessChildMajorPgFaults |\- |The major page faults of a child process. |
||ProcessChildMinorPgFaults |\- |The minor page faults of a child process. |
||ProcessIOReadBytes |Bytes |The number of bytes read by a process. |
||ProcessIOReadCount |\- |The number of times that a process reads a disk. |
||ProcessIOWriteBytes |Bytes |The number of bytes written by a process. |
||ProcessIOWriteCount |\- |The number of times that a process is written to a disk. |
||ProcessInvoluntaryCtxSwitches |\- |The number of involuntary context switches for a process. |
||ProcessVoluntaryCtxSwitches |\- |The number of voluntary context switches for a process. |
||ProcessMajorPgFaults |\- |The major page faults of a process. |
||ProcessMemPct |% |The memory utilization of a process. |
||ProcessMemRSS(KB) |KB |The size of the resident set for a process. |
||ProcessMemVMS(KB) |KB |The virtual memory size of a process. |
||ProcessMinorPageFaults |\- |The minor page faults of a process. |
||ProcessOpenFds |\- |The number of open files of a process. |
||ProcessThreads |\- |The number of threads used by a process. |
||NumDiskSleepProc |\- |The number of processes in the D state. |
||NumZombieProc |\- |The number of processes in the Z state. |


<span id="GPU"></span>
## GPU


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|GPU |GpuUsedUtilization |% |The GPU utilization. |
||GpuTemperature |℃ |The GPU temperature. |
||GpuPowerReadingsPowerDraw |W |The GPU power. |
||GpuDecoderUtilization |% |The GPU decoder utilization. |
||GpuEncoderUtilization |% |The GPU encoder utilization. |
||GpuMemoryFreeSpace |Bytes |The idle memory of a GPU. |
||GpuMemoryFreeUtilization |% |The idle rate of the GPU memory. |
||GpuMemoryTotalSpace |Bytes |The total memory of a GPU. |
||GpuMemoryUsedSpace |Bytes |The memory usage of a GPU. |


<span id="RDMA"></span>
## RDMA


|Category |Metric Name |Metric Unit |Metric Definition |
|---|---|---|---|
|RDMA |port_RdmaRxBits |Bits/s |The receive throughput in the Remote Direct Memory Access (RDMA) network. |
||port_RdmaTxBits |Bits/s |The transmission throughput in the RDMA network. |
||port_RdmaRxPackets |Packet/s |The number of received network packets in the RDMA network. |
||port_RdmaTxPackets |Packet/s |The number of sent network packets in the RDMA network. |
||Port_RxCnpHandledPackets |\- |(Receive path) The number of Congestion Notification Packets (CNPs) processed by a NIC in the RDMA network within 60 seconds. |
||Port_RxEcnReceivedPackets |\- |(Receive path) The number of ECN\-marked packets received by a NIC in the RDMA network within 60 seconds. |
||Port_RxCnpIgnoredPackets |\- |(Receive path) The number of CNPs ignored by a NIC in the RDMA network within 60 seconds. |
||Port_TxCnpSendPackets |\- |(Send path) The number of CNPs sent by a NIC in the RDMA network within 60 seconds. |
||Port_TxAckTimeoutTimes |\- |The number of timeouts at the RDMA sender. |
||Port_RxOutOfSequenceTimes |\- |The number of out\-of\-sequence events at the RDMA receiver. |
||Port_TxOutOfSequenceTimes |\- |The number of out\-of\-sequence events at the RDMA sender. |
||Port_ReadRespOutOfSequenceTimes |\- |The number of out\-of\-sequence read response packets in the RDMA network. |
