---
title: "CloudWeGo service tracing"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/CloudWeGo_service_distributed_tracing"
---

Server\-side Monitoring has been adapted to multiple CloudWeGo frameworks, enabling tracing for CloudWeGo\-related services. Currently switched to the Demo region, you can view CloudWeGo\-related demo applications to understand the overall functional modules of APMPIus.

<span id="V67XziMS"></span>
## Background

CloudWeGo is positioned as a set of middleware for rapidly building enterprise\-level cloud\-native microservice architectures. Its common features are high performance, high scalability, and high reliability, focusing on microservice communication and governance. To date, the CloudWeGo GitHub organization has multiple repositories, including several key sub\-projects such as **Kitex, Hertz, Netpoll, Volo**, and multiple small but elegant sub\-projects such as **Thriftgo, Frugal, Fastpb, Pilota, Motore, cwgo, Dynamicgo, Shmipc, sonic\-rs**, and two projects, **Sonic and Monoio**.


* **Kitex**: A Golang microservice RPC framework featuring **high performance** and **high scalability**. It supports multiple message protocols (Thrift/Protobuf/gRPC), multiple message types (PingPong/Oneway/Streaming), service governance, code generation, and a complete open\-source community ecosystem.

* **Hertz**: A Golang microservice HTTP framework featuring **high performance and high scalability**. It supports multiple protocols (HTTP 1.1/HTTP 2/HTTP 3/Websocket), on\-demand switching of network layers (Netpoll/go net), rich Web middleware capabilities, comprehensive service governance, code generation, and a complete open\-source community ecosystem.


<span id="OoB3SEqY"></span>
## Prerequisites

CloudWeGo\-related services have already been integrated, for example, [Kitex](https://docs.byteplus.com/en/docs/apmplus/Integrate_Kitex) and [Hertz](https://docs.byteplus.com/en/docs/apmplus/Integrate_Hertz).

<span id="dCJb9Ycu"></span>
## Procedure


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Switch the project to **All resources of the account**, and the region to the **demo** region.

3. In all services, select the ** cloudwego.demonote** service to view service details, including service overview, service topology, process analysis, interface monitoring, upstream/downstream calls, log analysis, and runtime monitoring.

4. Click **Trace analysis** in the left navigation pane, filter by the cloudwego.demonote service, and then filter target traces by span attribute. Typically, you can filter target trace details by attribute such as request ID or user ID.

5. After locating the target trace, click the TraceID to go to the "Single trace details" page and view detailed information about the current trace. The list will display all span information related to the current trace. You can check whether a span comes from Kitex or Hertz by viewing the Tags information in the Attribute tab.

    &nbsp;

6. Switch to the Metrics tab to view host details, process details, and container details within the time range associated with the target trace. You can analyze the trends of these metrics to determine whether any system metrics are relevant to latency.

7. Click **Service topology** in the left navigation pane, and search for the topology of the cloudwego.demonote service by keyword.
