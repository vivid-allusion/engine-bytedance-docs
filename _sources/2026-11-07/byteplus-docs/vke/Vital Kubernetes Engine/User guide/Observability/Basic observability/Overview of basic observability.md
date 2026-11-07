---
title: "Overview of basic observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-overview"
---

VKE supports cloud\-native observability. This enables you to collect, monitor, and trigger alerts on metrics for clusters, basic resources, and applications.

<span id=".5Z-65pys5Y6f55CG"></span>
## Basic principles

Basic observability is built on Vital Managed Service for Prometheus (VMP), which is compatible with open\-source Prometheus APIs and the community Exporter ecosystem. This enables rapid monitoring of cluster infrastructure resources and user workloads.

Compared with a self\-managed Prometheus environment, you do not manually need to download or configure Prometheus, or worry about the storage cost of large volumes of data. Basic observability provides a setup\-free, maintenance\-free integrated Prometheus environment, reducing development and O&M costs.

<span id=".5Li76KaB54m55oCn"></span>
## Main features

The main features of cloud\-native basic observability are shown in the table below.


|Category |Feature |Basic observability |
|---|---|---|
|Installation and deployment |Data collection |The prometheus\-agent add\-on. |
||High availability |Unmanaged add\-ons, which support sharding and automatic scaling. |
||Data storage |Data storage is implemented based on VMP. Workspaces with different specifications are supported. For details, see [Workspace specifications](https://docs.byteplus.com/en/docs/vmp/workspaces-types). |
|Monitoring |Cluster monitoring |Cluster resource monitoring and custom application monitoring. Valid values:<br><br><br>* **Basic resources**, including clusters, nodes, workloads, pods, containers, volumes, and more.<br><br>* **Control plane add\-ons**, including kube\-apiserver, kube\-scheduler, etcd, and more.<br><br>* **Other resources**, including GPU, P2P acceleration, Nydus, RDMA, and more. |
||Custom monitoring |* Custom cloud\-native application monitoring is supported.<br><br>* Application metrics can be exposed by using the Prometheus SDK to enable application monitoring. |
||Self\-built Exporter monitoring |* Various types of Exporters provided by the open\-source Prometheus community can be used to collect metrics from different services. Examples of these services are databases, hardware, message middleware, storage systems, and HTTP servers.<br><br>* Custom Exporters can be created based on the Client Library available in the open\-source Prometheus community. The Prometheus community provides support for Go, Java, Python, Ruby, and other languages. |
|Metric viewing |Built\-in dashboards |Supported, with a wide variety. |
||Custom dashboards |Supported. You can create one based on open\-source Grafana. |
||Metric query |Metrics can be queried by using Explore. |
|Alert center |Metric alerting |Supported |
||Alert levels |Supported |
||Alerting templates |Supported |
||Alert silencing |Supported |
||Alert notification methods |Email, Webhook, phone, Feishu, DingTalk, WeCom, and more. |
