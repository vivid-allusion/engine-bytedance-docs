---
title: "Glossary"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Basic-concepts"
---

This topic describes the common glossary of Vital Managed Service for Prometheus (VMP). This helps you quickly understand service knowledge and concepts when you read related documentation.


|Glossary |Description |
|---|---|
|exporter |An exporter serves as an agent that collects monitoring data and provides data based on the Prometheus specification. The Prometheus community provides a wide variety of exporters, which can be used to monitor various targets such as infrastructure, middleware, and network. You can also define custom exporters. For more details, refer to the [official documentation of Prometheus](https://prometheus.io/docs/instrumenting/exporters/). |
|target |The data collection target of the Prometheus collector, which exposes the metric information of its own operational or business status. The targets include the CPU, memory, storage, and elastic network interfaces (ENIs) of hosts. |
|job |The configuration set for a group of targets. |
|PromQL |Prometheus Query Language (PromQL) is a unique Domain Specific Language (DSL) of Prometheus for data query. PromQL features rich expressiveness and many built\-in functions, which can be used in daily data visualization and rule alerting. |
|Grafana |Grafana is an open source metric analysis platform with various dashboards and charts. It provides various methods for you to efficiently create, share, and view data. Grafana provides comprehensive support for Prometheus. |
|CRD/CR |Custom Resource Definitions (CRDs) serve as the API definitions of custom resources in Kubernetes. Custom Resources (CRs) refer to specific custom resource objects. |
|workspace |The VMP workspace is an abstract integration of data and collection rules, which provides you with physically or logically isolated Prometheus capabilities. You can create different workspaces in VMP, where data in different workspaces is isolated from each other. |
|monitoring instance |The logical unit used for data collection and data storage analysis during VMP monitoring. Each monitoring logical unit exposes monitoring sample data via HTTP. For example, node\-exporter that is running on a host can be called a monitoring instance. |
|metrics |Metrics refer to the labelled data exposed by the monitoring target. Metrics reflect the operational or business status of the target. The metrics include CPU utilization, memory utilization, network traffic, total HTTP requests, and other metrics. Metrics mainly consist of metric names and labels.<br><br><br>* The metric name is used to describe the meaning of the metric. For example, http_request_total indicates the total number of HTTP requests.<br><br>* The label mainly reflects the dimensional characteristics of metrics and is used for filtering, aggregating, or pruning metrics. Labels consist of label names and label values, which form multiple dimensions of metrics. For example, the http_request_total monitoring metric can be split by dimension such as status="404" or status="200" and method="get" or method="post". |
|service discovery |Service discovery is a major feature of Prometheus. Prometheus pulls the metrics of monitoring targets. Therefore, you can configure native Prometheus service discovery, ServiceMonitor, PodMonitor, or Probe to discover different collection targets. |
