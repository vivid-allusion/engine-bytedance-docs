---
title: "MSE metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Microservices-Engine"
---

Microservices Engine (MSE) provides registration discovery and configuration management capabilities for microservices applications by hosting microservices core add\-ons. This topic describes common MSE metrics in VMP.


|**Type** |**Parameter** |**Description** |VMP metric |
|---|---|---|---|
|Resource usage overview |Outbound traffic |The outbound network traffic of each node in a cluster where an instance is deployed. |`mse_nacos_server_network_transmit_bytes` |
||Inbound traffic |The inbound network traffic of each node in a cluster where an instance is deployed. |`mse_nacos_server_network_receive_bytes` |
||CPU utilization |The CPU utilization of each node in a cluster where an instance is deployed. |`mse_nacos_server_cpu_usage` |
||Memory utilization |The memory utilization of each node in a cluster where an instance is deployed. |`mse_nacos_server_mem_usage` |
||Number of nodes |The number of nodes configured in an instance rule. |`mse_nacos_server_cpu_usage` |
||Load metric |The average number of tasks using or waiting for CPU per minute on each node in a cluster where an instance is deployed. |`mse_system_load_average_1m` |
|Instance information overview |Number of nodes |The number of nodes specified in the instance specification. |`mse_nacos_server_cpu_usage` |
||Number of configurations |The number of configurations added in the configuration center. |`mse_nacos_monitor{module="config",name="configCount"}` |
||Number of service providers |The number of service providers registered in the registration center. |`mse_nacos_monitor{module="naming",name="ipCount"}` |
||QPS |The total number of read operations per second of all nodes in an instance. |`mse_nacos_monitor_reader_seconds_count {module="naming"}+mse_nacos_timer_seconds_count{module="config",name=~"readConfigRpcRt\|readConfigRt"}` |
||Operations per second |The total number of write operations per second of all nodes in an instance. |`mse_nacos_monitor_writer_seconds_count+mse_nacos_timer_seconds_count` |
||Number of connections |The total number of connections of each node in an instance. |`mse_nacos_monitor{name="longConnection"}` |
|Registration center monitoring |Number of services |The total number of services registered in the registration center. |`mse_nacos_monitor{module="naming",name="serviceCount"}` |
||Number of service providers |The number of service providers registered in the registration center. |`mse_nacos_monitor{module="naming",name="ipCount"}` |
||Number of service subscribers |The number of service subscribers in the registration center. |`mse_nacos_monitor{module="naming",name="subscriberCount"}` |
||Registration center TPS |The total number of write requests processed by all nodes per second in the registration center. |`mse_nacos_monitor_writer_seconds_count {module="naming"}` |
||Registration center QPS |The total number of read requests processed by all nodes per second in the registration center. |`mse_nacos_monitor_reader_seconds_count{module="naming"}` |
||Write RT of the registration center |The average write operation latency of all nodes in the registration center. |`mse_nacos_monitor_writer_seconds_sum {module="naming"}/mse_nacos_monitor_writer_seconds_count {module="naming"}` |
||Read RT of the registration center |The average read operation latency of all nodes in the registration center. |`mse_nacos_monitor_reader_seconds_sum {module="naming"}/mse_nacos_monitor_reader_seconds_count {module="naming"}` |
|Configuration center monitoring |Number of configurations |The number of configurations added in the configuration center. |`mse_nacos_monitor{module="config",name="configCount"}` |
||Number of listeners |The number of Nacos clients listening to the configuration in the configuration center. |`mse_nacos_monitor{module="config",name="listenerCount"}` |
||Configuration center TPS |The total number of write requests processed by all nodes per second in the configuration center. |`mse_nacos_timer_seconds_count{module="config",name=~"writeConfigRpcRt\|writeConfigRt"}` |
||Configuration center QPS |The total number of read requests processed by all nodes per second in the configuration center. |`mse_nacos_timer_seconds_count{module="config",name=~"readConfigRpcRt\|readConfigRt"}` |
||Write RT of the configuration center |The average write operation latency of all nodes in the configuration center. |`mse_nacos_timer_seconds_sum{module="config",name=~"writeConfigRt\|writeConfigRpcRt"}/mse_nacos_timer_seconds_count{module="config",name=~"writeConfigRt\|writeConfigRpcRt"}` |
||Read RT of the configuration center |The average read operation latency of all nodes in the configuration center. |`mse_nacos_timer_seconds_sum{module="config",name=~"readConfigRt\|readConfigRpcRt"}/mse_nacos_timer_seconds_count{module="config",name=~"readConfigRt\|readConfigRpcRt"}` |
|Client data monitoring |Service push success rate |The success rate of service push operations in an instance. |`1-mse_nacos_monitor{module="naming",name="failedPush"}/mse_nacos_monitor{module="naming",name="totalPush"}` |
||Service push latency |The average service push latency of all nodes in an instance. |`mse_nacos_monitor{module="naming",name="avgPushCost"}` |
||Service push TPS |The total number of tasks pushed by all nodes per second in an instance. |`mse_nacos_monitor{module="naming",name="totalPushCountForAvg"}` |
||Number of client versions |The number of Nacos client versions in an instance. |`mse_nacos_clients_total` |
||Number of persistent connections |The number of persistent connections of each node in an instance. |`mse_nacos_connections_total` |
|JVM overview |Young GC duration |The time consumed for young garbage collections (GCs) of each node in an instance. |`mse_jvm_gc_pause_seconds_sum{action="end of minor GC"}` |
||Number of young GCs |The number of young GCs performed by each node in an instance. |`mse_jvm_gc_pause_seconds_count{action="end of minor GC"}` |
||Full GC duration |The time consumed for full GCs of each node in an instance. |`mse_jvm_gc_pause_seconds_sum {action="end of major GC"}` |
||Number of full GCs |The number of full GCs performed by each node in an instance. |`mse_jvm_gc_pause_seconds_count{action="end of major GC"}` |
||Heap memory utilization |The Java virtual machine (JVM) heap memory utilization of each node in an instance. |`mse_jvm_memory_used_bytes{area="heap"}/mse_jvm_memory_max_bytes{area="heap"}` |
