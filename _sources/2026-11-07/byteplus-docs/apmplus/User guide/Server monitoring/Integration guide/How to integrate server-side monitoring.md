---
title: "How to integrate server-side monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_server-side_monitoring"
---

Server\-side monitoring uses a non\-intrusive instrumentation approach, so you only need to perform simple configuration to enable server\-side monitoring. How to integrate server\-side monitoring

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Register a  account and complete real\-name authentication. If you have not completed these steps, please register an account and complete identity verification first. 

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation Procedure

You can refer to the following steps to integrate server\-side monitoring.


1. Log in to the [Application Performance Management Plus](https://console.byteplus.com/observe/apmplus-server) console homepage.

2. In the menu bar on the left, click **server\-side monitoring.** 

3. Click the **Enter service list** in the upper left corner to enter the service list page.

4. On the **Service List** page, click the **Create Service** button to enter the service access page.

5. On the **Service Access** page, select the application type you want to integrate.

   Integration is now supported for applications written in Java, Go, Python, Nodejs, or other languages. Please refer to the integration process and important notes for applications in various languages:


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When integrating the application, you must provide the correct service name value; it cannot be left empty. Otherwise, the reported access data will be discarded immediately.</div>



* [Integrate Java applications](https://docs.byteplus.com/en/docs/apmplus/Java_application_integration)

* [Go application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Go_applications)

* [Integrate Python applications](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications)

* [Integrate a Node.js application](https://docs.byteplus.com/en/docs/apmplus/Integrate_a_Nodejs_application)

* [Integrate applications in other languages](https://docs.byteplus.com/en/docs/apmplus/Integration_of_applications_in_other_languages)

   The monitoring systems supported for each language are as follows.



|**Monitoring system** |**Supported application language types** |**DescriptionS** |
|---|---|---|
|APMPlus |Java、Go |The APMPlus proprietary monitoring component is a data collection tool independently developed by APMPlus. It is responsible for the collection of monitoring data from applications and infrastructure, and then reports the relevant data to the APMPlus server side for visualization, query, and analysis.<br><br>Currently, only Java and Go applications are supported.<br><br>For details, refer to [APMPlus self-developed Monitoring component description](https://docs.byteplus.com/en/docs/apmplus/Description_of_the_APMPlus_self-developed_monitoring_system). |
|OpenTelemetry |Java, Go, Node.js, Python, and others |OpenTelemetry is an observability project under CNCF that aims to provide standardized solutions for the observability domain. It addresses the standardization of data models, collection, processing, and export of observability data, and offers vendor\-neutral services.<br><br>If your application has already integrated the OpenTelemetry SDK, the APMPlus server side can receive data reported by OpenTelemetry. After integrating APMPlus, you will gain multiple monitoring capabilities, including RED metric generation, multidimensional trace search, single trace search, and topology generation.<br><br>For details, refer to [OpenTelemetry](https://opentelemetry.io/docs/). |
|Prometheus |Java, Go, and others |APM OpenTelemetry Collector is a data collector developed by APMPlus based on OpenTelemetry Collector. It complies with the Apache 2.0 license and supports the collection of OpenTelemetry monitoring data, as well as Prometheus metrics and K8s resource metrics. You can use Prometheus to meet the requirements for custom metrics. For systems that have already integrated Prometheus, custom application metric data can be reported to APMPlus for metric storage, querying, and display. Dashboard and alert features are also supported.<br><br>For details, refer to [Prometheus](https://prometheus.io/docs/introduction/overview/). |
|Jaeger |Java, Go, and others |Jaeger is an open\-source distributed tracing system developed by Uber. For existing operating systems that have already integrated Jaeger, Jaeger trace data can be reported to APMPlus to achieve comprehensive full trace monitoring capability. After integrating APMPlus, you will gain monitoring capabilities such as RED method metric generation, multidimensional trace search, single trace search, and topology generation.<br><br>For details, refer to [Jaeger](https://www.jaegertracing.io/docs/1.40/). |
|Zipkin |Java, Go, and others |Zipkin is an open\-source distributed tracing system developed by Twitter. Zipkin can help you collect trace data. For systems that have already integrated Zipkin, existing trace data can be reported to APMPlus to enable comprehensive end\-to\-end trace monitoring capabilities. After integrating APMPlus, you will gain the ability to generate RED method metrics, perform multi\-dimensional trace search, conduct single trace search, generate topologies, and access many other monitoring capabilities.<br><br>For details, refer to [Zipkin](https://zipkin.io/) **。**  |
|SkyWalking |Java, Go, and others |Skywalking is an application performance monitoring tool for distributed systems, featuring distributed tracing, performance metric analysis, service dependency analysis, and more.<br><br>For details, refer to [Skywalking](https://skywalking.apache.org/docs/). |
