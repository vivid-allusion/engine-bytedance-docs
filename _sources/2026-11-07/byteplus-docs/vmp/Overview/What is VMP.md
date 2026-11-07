---
title: "What is VMP"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus"
---

As a monitoring service hosted on the  cloud, Vital Managed Service for Prometheus (VMP) fully inherits and integrates with the open\-source Prometheus ecosystem.

<span id=".5byA5rqQIFByb21ldGhldXMg566A5LuL"></span>
## Introduction to Prometheus

Prometheus is an open source monitoring system released in January 2015. Prometheus joined the Cloud Native Computing Foundation (CNCF) in May 2016 as the second hosted project, after Kubernetes. The community remains active and has a large customer base. Prometheus has become the de facto standard monitoring solution for Vital Kubernetes Engine (VKE).


* A custom multi\-dimensional data model with time series data consisting of metric names and key/value pairs.

* PromQL, a flexible and useful query language that leverages multi\-dimensional data to perform complex data querying, aggregation, and filtering.

* Time series data is collected via a pull model over HTTP. This applies to scenarios in Kubernetes where monitoring targets are created and deleted at any time.

* Targets are discovered through static and dynamic service discovery.

* Combined with visualization solutions such as Grafana, VMP supports various visualized charts and dashboards.


<span id=".5omY566hIFByb21ldGhldXMg566A5LuL"></span>
## Benefits of VMP

VMP is a standardized Prometheus service hosted on the  cloud. You can quickly create standard Prometheus instances on  to provide a highly available, O&M\-free metric storage solution for  AI services, cloud infrastructure, cloud\-native services, and business workloads deployed in the cloud. In addition, VMP offers standard read/write endpoints such as RemoteWrite, Query, and Pushgateway to meet the requirements for writing and consuming monitoring data.

The following table describes the major differences between self\-built Prometheus and VMP and the benefits of VMP.


|Feature |Vital Managed Service for Prometheus |Self\-built Prometheus |
|---|---|---|
|O&M cost |O&M\-free |Users need to perform O&M by themselves. |
|Data storage |* Supports different storage durations, including 15 days, 30 days, 90 days, 180 days, and 1 year. Allows you to flexibly select monitoring data storage durations based on your business requirements.<br><br>* Allows you to change storage durations. You can increase storage durations with a few clicks if the durations are insufficient. |Storage capacity is limited and cannot be expanded. |
|High availability |Adopts the high\-availability solution that deploys multiple replicas in a single availability zone and across multiple availability zones to ensure data security and availability in case of a single point of failure. |Customers need to design high\-availability solutions by themselves. |
|Data Integration |Supports multiple types of collectors and quick cloud service integration.<br><br><br>* Supports the installation of collector agents in cloud services and the configuration of collection rules. Quickly collects the metrics of cloud services and custom applications.<br><br>* Provides collection agents deployed in different cloud environments and collects various metrics of targets such as nodes and containers in a centralized manner. |You can select a collector to integrate data. |
|Alert notification |Provides common alerting rule templates to help users quickly configure alerts. Provides multiple alerting notification methods such as webhook, phone call, text message, Feishu, DingTalk, and WeCom. |Users need to build alerting notification channels by themselves. |
|Service guarantee |The professional observability support team at  has sustained the normal operation of a large number of internal ByteDance workloads, accumulating extensive best practices and management experience. Provides an SLA that contains the service availability grade indicator and compensation plans. |A professional service team is required, and no Service Level Agreement (SLA) guarantee is provided. |
|Security management |VMP is a fully managed service, with security hardening enabled by default. Comprehensive network isolation and fine\-grained access control are adopted to ensure the security and high availability of services and data. |Users need to guarantee environmental security by themselves. |
|Horizontal services |VMP can be integrated with and monitor various cloud services related to cloud infrastructure, AI, and machine learning to achieve one\-stop cloud monitoring. The services include Machine Learning Platform (MLP), ModelArk, VKE, Elastic Compute Service (ECS), and other services. |Users need to build and integrate horizontal services. |


<span id="MhFM3lqM"></span>
## Product architecture

The following figure shows the product architecture of VMP.

&nbsp;

&nbsp;
