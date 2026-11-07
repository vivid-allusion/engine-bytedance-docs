---
title: "Metric references"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Metric_references"
---

Full\-stack observability supports the collection of various network\-layer and application\-layer metrics. This topic describes supported metrics.

<span id="89jw4lNd"></span>
## Background

After you turn on full\-stack observability and configure metric collection, the system collects the corresponding eBPF metrics based on your configuration. For information about configuring metric collection, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Metrics collected by full\-stack observability are stored in VMP workspaces for metric queries, dashboard creation, and alerting. All these metrics are <strong>non\-basic metrics (that is, chargeable metrics)</strong>. Configure metric collection based on your actual needs. For VMP billing details, see <a href="https://docs.byteplus.com/en/docs/vmp/billing-overview">Billing overview</a>.</div>


<span id="qcg1Gbbu"></span>
## Metrics

<span id="emVbHDaS"></span>
### Topology metrics

The **cluster topology** feature in full\-stack observability depends on the following metric, which is enabled by default and cannot be disabled. For details, see [Cluster topology](https://docs.byteplus.com/en/docs/vke/Cluster-topology).


|Metric description |Metric name |Unit |Metric type |Metric source |
|---|---|---|---|---|
|Network topology |ms_network_topology |\- |gauge |eBPF |


<span id="PdbDwc3t"></span>
### Network metrics

Network metrics include TCP and UDP metrics. You can enable or disable the corresponding metrics as needed. The following table describes these metrics.


|Metric description |Metric name |Unit |Metric type |Metric source |
|---|---|---|---|---|
|Number of TCP connections initiated |ms_tcp_conn_open_total |Count |counter |eBPF |
|Number of TCP connections established |ms_tcp_conn_total |Count |counter |eBPF |
|TCP connection duration |ms_tcp_conn_duration |Milliseconds |histogram |eBPF |
|Number of TCP connections closed due to errors |ms_tcp_conn_error_closed_total |Count |counter |eBPF |
|Inbound TCP traffic |ms_tcp_recv_bytes_total |Bytes |counter |eBPF |
|Outbound TCP traffic |ms_tcp_sent_bytes_total |Bytes |counter |eBPF |
|Number of inbound TCP packets |ms_tcp_recv_packets_total |Count |counter |eBPF |
|Number of outbound TCP packets |ms_tcp_sent_packets_total |Count |counter |eBPF |
|Number of lost TCP packets |ms_tcp_packets_loss_total |Count |counter |eBPF |
|TCP retransmission count |ms_tcp_retrans_total |Count |counter |eBPF |
|Inbound UDP traffic |ms_udp_recv_bytes_total |Bytes |counter |eBPF |
|Outbound UDP traffic |ms_udp_sent_bytes_total |Bytes |counter |eBPF |
|Inbound UDP datagrams |ms_udp_recv_datagrams_total |Count |counter |eBPF |
|Outbound UDP datagrams |ms_udp_sent_datagrams_total |Count |counter |eBPF |
|Number of UDP datagrams that failed to be received. |ms_udp_recv_datagrams_error_total |Count |counter |eBPF |
|Number of UDP datagrams that failed to be sent. |ms_udp_sent_datagrams_error_total |Count |counter |eBPF |


<span id="K3Cyv5rl"></span>
### Application metrics

Application metrics include metrics related to application\-layer protocols, such as HTTP and DNS. You can enable or disable the corresponding metrics as needed. The following table describes these metrics.


|Metric description |Metric name |Unit |Metric type |Metric source |
|---|---|---|---|---|
|Application\-layer API request count |ms_requests_total |Count |counter |eBPF |
|Application\-layer API request latency |ms_request_duration |Milliseconds |histogram |eBPF |
|Number of MQ requests (including Redis Pub/Sub) |ms_messaging_io_total |Count |counter |eBPF |
|MQ request duration (including Redis Pub/Sub) |ms_messaging_io_duration |Milliseconds |histogram |eBPF |
|Number of application\-layer gRPC Streaming messages sent and received |ms_streaming_message_total |Count |counter |eBPF |
|Application layer GRPC Streaming sent/received message size |ms_streaming_message_size |Bytes |counter |eBPF |
|Total number of application\-layer protocol records successfully parsed and processed |ms_agent_records_process_total |Count |counter |eBPF |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Application metrics do not fully match the configurations in the console. The application layer protocol of the metric is displayed only via the <code>traffic_protocol</code> label. For a description of the metric label, see the section below.</div>


* <div data-tips="true" data-tips-type="default">You can deselect unnecessary application layer protocols in the console to reduce the number of collected metrics.</div>



<span id="RM1SfWrQ"></span>
## Metric labels

Various labels are added to full\-stack observability metrics to indicate the dimensions of traffic. For example, the `source_pod` label indicates the source Pod for the metric in the request. The following table describes metric labels.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The labels supported by different metrics vary slightly.</div>



|Label name |Label description |
|---|---|
|source_workload |Source workload. |
|source_workload_kind |The kind of the source workload. |
|source_workload_namespace |The namespace of the source workload. |
|source_pod |The source pod. This label appears only in client\-side metrics. |
|source_node |The node where the request source is located. |
|dest_workload |The destination workload. |
|dest_workload_kind |The kind of the destination workload. |
|dest_workload_namespace |The namespace of the destination workload. |
|dest_service |The Kubernetes Service corresponding to the destination of the request. This label appears only when the request destination is a Service. |
|dest_service_namespace |The namespace of the destination Service. This label appears only when the request destination is a Service. |
|dest_pod |The destination pod. This label appears only in server\-side metrics. |
|dest_node |The node where the request destination is located. |
|dest_cluster |The ID of the cluster where the request destination is located. |
|traffic_protocol |Traffic protocol, for example, http or dns. |
|traffic_direction |Traffic direction:<br><br><br>* **ingress**: Inbound.<br><br>* **egress**: Outbound. |
|traffic_role |Traffic role. Possible values:<br><br><br>* **client**: Client<br><br>* **server**: Server |
|traffic_status_code |HTTP status code. For example, HTTP status codes 2xx, 4xx, and 5xx. |
|traffic_status |Traffic status. Possible values:<br><br><br>* **ok**: Success.<br><br>* **error**: Fail.<br><br>* **unknown**: Unknown. |
|operation |The API name. This label appears only in API metrics. |
|dns_domain |DNS domain. This label appears only in API metrics. |
|dns_domain_type |The DNS type, for example, CNAME, A, AAAA, or TXT. This label appears only in API metrics. |
|is_slow |Whether the traffic is from a slow call. Valid values:<br><br><br>* **true**: Slow call.<br><br>* **false**: Non\-slow call. |


&nbsp;

&nbsp;

&nbsp;

&nbsp;
