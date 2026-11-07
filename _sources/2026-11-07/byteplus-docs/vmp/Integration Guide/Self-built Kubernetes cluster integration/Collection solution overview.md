---
title: "Collection solution overview"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Collection-solution-overview"
---

Vital Managed Service for Prometheus (VMP) provides you with ready\-to\-use data collection solutions tailored for self\-managed Kubernetes clusters. This topic describes the collection solutions.

<span id=".6YeH6ZuG5pa55qGI5qaC6L-w"></span>
## Collection solution overview

VMP offers a high\-availability collection solution based on the VM Agent collector. As a production\-oriented solution, it supports flexible scale\-out for collectors and the kube\-state\-metrics add\-on.

VM Agent is a tool provided by VictoriaMetrics, which has similar features and roles to the Agent mode of Prometheus. VM Agent is specially used for service discovery and collection, which is an alternative to Prometheus without providing a read interface.

<span id=".6auY5Y-v55So5oCn6K-05piO"></span>
## High availability description

The VM Agent collector comes with an operator, which achieves sharding and data collection for the collector and the kube\-state\-metrics add\-on, achieving high performance and availability. 

<span id=".6YeH6ZuG5pa55qGI5a-55q-U"></span>
## Collection solution description

The following table describes the high\-availability collection solution.


|Metric parameters |High\-availability collection solution |
|---|---|
|Collector |VM Agent collector |
|Performance |Excellent |
|Authentication Method |Basic Auth authentication |
|Come with an operator |Yes |
|Support shards |Yes |
|service discovery |* Supports service discovery configuration based on ServiceMonitor, PodMonitor, and Probe.<br><br>* Supports service discovery configuration based on service/pod annotations. |
|Available for production |Yes |
