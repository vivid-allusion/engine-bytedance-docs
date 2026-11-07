---
title: "Application scenarios"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Use-scenarios"
---

<span id="1LYiqqpq"></span>
## Machine learning platform observability

VMP can be deeply integrated with Machine Learning Platform (MLP) and ModelArk of . VMP can monitor the computing power, tasks, data, services, and performance of large AI models and provide various preset dashboards and rules.

<span id=".5a655Zmo5pyN5Yqh6KeC5rWL"></span>
## Inference suite and training suite observability

VMP can be deeply integrated with cloud services and AI frameworks to achieve comprehensive centralized monitoring and provide various preset dashboards and rules.

<span id="Few2U9Pe"></span>
## Cloud service observability

You can use the Cloud Monitor exporter to export the cloud service monitoring data from Cloud Monitor to VMP in real time and merge the data with business monitoring data in your clusters. This achieves centralized observability of business data and resource data. It helps you collect and visualize the resource status and monitoring information of various cloud services for , including Elastic Compute Service (ECS), Vital Kubernetes Engine (VKE), API Gateway (APIG), Direct Connect (DC), and Torch Object Storage (TOS). In addition, you can use Grafana, which is natively compatible with VMP, to build business\-related dashboards.

<span id=".5byA5rqQ55Sf5oCB6KeC5rWL"></span>
## Custom observability

Featuring an excellent open source ecosystem affinity, VMP supports third\-party exporters provided by the open source community for monitoring metrics of the open source ecosystem, including middleware and database. VMP has the following characteristics:


* **Open source community compatibility**: VMP supports the SDKs provided by the Prometheus community for direct business metric tracking and quick integration.

* **Cloud\-native compatibility**: VMP can be used to collect the metrics of cloud\-native applications without modification or adaptation.

* **Exporter compatibility**: VMP supports various exporters provided by the open source community to quickly collect the metrics of conventional applications.


<span id="vgxqiJEK"></span>
## Multi\-cloud observability

VMP can monitor cross\-cloud resources in a centralized manner and is compatible with the Prometheus/Grafana ecosystem. It offers capabilities including data collection, intelligent alerting, and elastic scaling. VMP mainly offers the following capabilities:


* VMP allows you to deploy collection agents in different cloud environments to collect various metrics of targets such as nodes and containers in a centralized manner.

* VMP collects and stores the observability data of multi\-cloud clusters in the same workspace, which facilitates the query of multi\-cluster data.

* VMP supports the SDKs and exporters of the Prometheus community, making it easy to integrate with the open source ecosystem for observability.
