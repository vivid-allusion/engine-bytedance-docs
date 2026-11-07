---
title: "Description of the APMPlus self-developed monitoring system"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Description_of_the_APMPlus_self-developed_monitoring_system"
---

The APMPlus proprietary monitoring system is an independently developed data collection tool for the Application Performance Management Plus full\-trace version. It is responsible for collecting monitoring data from applications and infrastructure, and then reporting the relevant data to the APMPlus server side for visualization and analysis.

<span id=".57O757uf5qGG5p6257uT5p6E"></span>
## Operating system architecture

 overall, server\-side monitoring adopts a three\-layer architecture.


* **Application probe**: The integrated Trace, Log, and Metrics SDKs communicate with the local agent via IPC (Inter Process Communication, that is, Inter\-process communication).

* **Agent**: Responsible for the collection of host machine data and container data on the host machine, receiving monitoring data sent by applications, caching the data, and forwarding it to the data center after compression and encryption. Also responsible for periodically synchronizing the dynamic configuration from the data center to the application.

* **Data center**: Responsible for receiving data, cleaning and storing it, ultimately presenting it to users, and providing analysis and alert features.


<span id=".SmF2YeW6lOeUqOWKn-iDvQ=="></span>
## Java application features

Java applications integrate with the server side using a non\-intrusive instrumentation solution. The following introduces the features supported after Java applications are integrated with the server side.

<span id="Trace"></span>
### Trace

After the Java application connects to the server side, JavaAgent can automatically collect trace information and generate metric data.

For the currently supported frameworks, refer to [Supported Frameworks List](https://docs.byteplus.com/en/docs/apmplus/Description_of_the_APMPlus_self-developed_monitoring_system#.5pSv5oyB55qE5qGG5p625YiX6KGo). After integration, Metrics will be automatically generated as follows:


|**Metrics** |**DescriptionS** |**Tags** |
|---|---|---|
|apminsight.service.trace.called.throughput |Number of calls |service: Name of called service<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: Process ID |
|apminsight.service.trace.called.latency.us. |Invocation duration |service: Name of the called service<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: Process ID |
|apminsight.service.trace.call.throughput |Number of calls to other services |service: Service name<br><br>resource: interface name<br><br>status: return code<br><br>instance_id: Process ID<br><br>call_service: Service name to call<br><br>call_resource: Interface name to call<br><br>db.slow_query: Is it a slow SQL query |
|apminsight.service.trace.call.latency.us. |Duration of calling other services |service: Name of the called service<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: Process ID<br><br>call_service: Service name to call<br><br>call_resource: Called interface name<br><br>db.slow_query: Is it a slow SQL query |
|apminsight.service.performance.cpu.core |Service CPU usage |service: Service name |
|apminsight.service.performance.cpu_limit.core |Service CPU limits |service: Service name |
|apminsight.service.performance.rss.mb |Service memory usage |service: Service name |
|apminsight.service.performance.memory_limit.mb |Service memory limit |service: Service name |


<span id="Log"></span>
### Log

After a Java application connects to the server side, it can support invocation chain search and log search features. Currently, integration has been implemented for the following frameworks:


* Logback

* log4j2


<span id="Metrics"></span>
### Metrics

After a Java application connects to the server side, the Metrics feature becomes available. For details, refer to [apminsight-server-sdk-java](https://github.com/volcengine/apminsight-server-sdk-java).

<span id=".SlZN55uR5o6n"></span>
### JVM monitoring

After a Java application connects to the server side, JVM\-related monitoring is supported, mainly including the following metrics:


|**Type** |**Metrics** |**DescriptionS** |**Unit** |
|---|---|---|---|
|Heap memory |jvm.init_heap |The initial heap memory of the JVM |Byte |
||jvm.used_heap |Used heap memory |Byte |
||jvm.max_heap |Maximum heap memory for JVM |Byte |
||jvm.committed_heap |JVM committed heap memory |Byte |
|Non\-heap memory |jvm.init_noheap |JVM initial non\-heap memory |Byte |
||jvm.used_noheap |JVM non\-heap memory in use |Byte |
||jvm.max_noheap |Maximum JVM non\-heap memory |Byte |
||jvm.committed_noheap |JVM submitted non\-heap memory |Byte |
|Memory pool \- NewGen |vm.init_newgen |JVM memory pool \- initial NewGen |Byte |
||jvm.max_newgen |JVM memory pool \- maximum NewGen |Byte |
||jvm.used_newgen |JVM memory pool – used NewGen memory |Byte |
||jvm.committed_newgen |JVM memory pool \- committed NewGen |Byte |
|Memory pool \- OldGen |jvm.init_oldgen |JVM memory pool \- initial OldGen |Byte |
||jvm.max_oldgen |Maximum JVM OldGen memory pool |Byte |
||jvm.used_oldgen |OldGen used |Byte |
||jvm.committed_oldgen |JVM memory pool \- committed OldGen |Byte |
|The memory pool CodeCache |jvm.init_code_cache |JVM memory pool \- initial CodeCache |Byte |
||jvm.max_code_cache |JVM memory pool: maximum CodeCache |Byte |
||jvm.used_code_cache |JVM memory pool \- CodeCache used |Byte |
||jvm.committed_code_cache |JVM memory pool \- submitted CodeCache |Byte |
|Memory pool \- survivor |jvm.init_survivor |JVM memory pool \- initial Survivor |Byte |
||jvm.max_survivor |JVM memory pool: maximum Survivor space |Byte |
||jvm.used_survivor |JVM memory pool \- Survivor used |Byte |
||jvm.committed_survivor |JVM memory pool \- committed Survivor |Byte |
|Memory pool–MetaSpace |jvm.init_meta_space |JVM memory pool \- initial MetaSpace |Byte |
||jvm.max_meta_space |JVM Memory pool \- Maximum MetaSpace |Byte |
||jvm.used_meta_space |JVM memory pool – MetaSpace used |Byte |
||vm.committed_meta_space |JVM memory pool \- committed MetaSpace |Byte |
|Memory pool\-PermGen |jvm.init_perm_gen |JVM memory pool \- initial PermGen size |Byte |
||jvm.max_perm_gen |JVM memory pool\-Maximum PermGen |Byte |
||jvm.used_perm_gen |JVM memory pool \- used PermGen |Byte |
||jvm.committed_perm_gen |JVM memory pool \- committed PermGen |Byte |
|Class loading |jvm.loaded_class_count |The number of classes currently loaded by the JVM |count |
||jvm.total_unloaded_class_count |Total number of unloaded classes in the JVM |count |
||vm.total_loaded_class_count |The total number of loaded classes in the JVM |count |
|Order |jvm.live_count |The number of live JVM threads |count |
||jvm.daemon_count |Number of JVM daemon threads |count |
||jvm.peak_count |JVM maximum thread count |count |
||jvm.runnable_state_thread_count |JVM runnable thread count |count |
||jvm.blocked_state_thread_count |Number of blocked threads in the JVM |count |
||vm.waiting_state_thread_count |JVM waiting thread count |count |
||vm.timed_waiting_state_thread_count |JVM timed waiting thread count |count |
|GC count |jvm.gc_count_old |JVM GC count \- OldGen |count |
||jvm.gc_count_new |JVM GC count – new generation |count |
|GC time |jvm.gc_time_old |JVM GC time \- OldGen |ms |
||jvm.gc_time_new |JVM GC time \- NewGen |ms |


<span id=".6Ieq5a6a5LmJ5o-S5qGp"></span>
### **Custom instrumentation**

After a Java application is integrated with the server side, custom code instrumentation for monitoring is supported. Configure the class names and method names for global and service dimensions on the platform to complete instrumentation of the relevant methods. The instrumentation results will be reported and queried together with the trace.

<span id=".5pSv5oyB55qE5qGG5p625YiX6KGo"></span>
### **Supported frameworks**


|**Framework/component** |**Maven** |**Version** |
|---|---|---|
|tomcat |org.apache.tomcat.embed:tomcat\-embed\-core |7.x~8.x |
|mysql |mysql:mysql\-connector\-java |5.x~8.x |
|oracle |com.oracle:ojdbc14 |Versions 10.x and above |
|redis |redis.clients:jedis |Version 2.x and above |
||io.lettuce:lettuce\-core |Version 5.x and above |
|Memcached |net.spy:spymemcached |Version 2.x or later |
||com.googlecode.xmemcached:xmemcached |Version 2.x and later |
|MongoDB |org.mongodb:mongo\-java\-driver |2.x~3.x |
||org.mongodb:mongodb\-driver\-sync |Version 4.x or later |
|Kafka |org.apache.kafka:kafka\-clients |Versions 0.11.0.0 and above |
|RocketMQ |com.alibaba.rocketmq:rocketmq\-client |Versions 3.x and above |
||org.apache.rocketmq:rocketmq\-client |Version 4.x or later |
|RabbitMQ |com.rabbitmq:amqp\-client |Version 5.x and above |
|logback |ch.qos.logback:logback\-classic |Version 1.x or later |
|log4j |org.apache.logging.log4j:log4j\-core |Version 2.x or later |
|HttpClient |com.squareup.okhttp:okhttp |version 2.x or later |
||com.squareup.okhttp3:okhttp |3.x~4.x |
||commons\-httpclient:commons\-httpclient |Versions 3.x and above |
||org.apache.httpcomponents:httpclient |Version 4.x and above |
||org.apache.httpcomponents.client5:httpclient5 |Version 5.x or later |
||org.apache.httpcomponents:httpasyncclient |Version 4.x or later |
||org.asynchttpclient:async\-http\-client |Versions 2.x and above |
||io.github.openfeign:feign\-core |9.x |
||org.springframework.cloud:spring\-cloud\-starter\-feign |1.x~2.x |
|Rest tempalte |org.springframework:spring\-web |Version 4.x or later |
|Spring |org.springframework:spring\-webmvc |3.x~5.x |
||org.springframework:spring\-context |3.x~5.x |


<span id=".R2_lupTnlKjlip_og70="></span>
## Go application features

The Go application integrates with the server side using an intrusive instrumentation approach. The following introduces the features supported after the Go application is integrated with the server side.

<span id="pHe20zEZ"></span>
### Trace

When integrating Go applications with the server side, a non\-intrusive instrumentation solution cannot be used; integration can only be achieved through frameworks. Currently, integration has been implemented for the following frameworks:


* gin\-gonic/gin

* gorm.io/gorm.v1

* net/http


For details on how to integrate, refer to the [trace feature description](https://github.com/volcengine/apminsight-server-sdk-go/tree/master/trace). After integration, the following Metrics will be automatically generated:


|**Metrics** |**DescriptionS** |**Tags** |
|---|---|---|
|apminsight.service.trace.called.throughput |Number of calls |Called service name<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: Process ID |
|apminsight.service.trace.called.latency.us. |Invocation duration |service: Name of the called service<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: Process ID |
|apminsight.service.trace.call.throughput |Number of calls to other services |service: Service name<br><br>resource: interface name<br><br>status: return code<br><br>instance_id: process<br><br>IDcall_service: Service name to call<br><br>Name of the called interface<br><br>db.slow_query: Is it slow<br><br>SQL |
|apminsight.service.trace.call.latency.us. |Time to call other services |service: Name of the service being called<br><br>resource: Name of the called interface<br><br>status: return code<br><br>instance_id: process<br><br>IDall_service: Service name to call<br><br>call_resource: Name of the called interface<br><br>db.slow_query: Is it a slow SQL query |
|apminsight.service.performance.cpu.core |Services CPU usage |service: Service name |
|apminsight.service.performance.cpu_limit.core |Service CPU limits |service: Service name |
|apminsight.service.performance.rss.mb |Service memory usage |service: Service name |
|apminsight.service.performance.memory_limit.mb |Service memory limits |service：Service name |


<span id="Um2aUNIn"></span>
### Log

After Go applications are integrated with the server side and adapted to the Trace and Log frameworks, features such as call chain search and log search can be implemented. Currently, integration has been performed for the following frameworks:


* sirupsen/logrus


For specific integration methods, refer to [Log feature description](https://github.com/volcengine/apminsight-server-sdk-go/tree/master/trace/contrib/sirupsen). The following Metrics will be automatically generated after integration:


|**Metrics** |**DescriptionS** |**Tags** |
|---|---|---|
|apminsight.service.log.throughput |Service log entries |service: Service name<br><br>log_level: Log level |


<span id="8wT6eNRh"></span>
### Metrics

Go SDK provides the following interfaces

```go
// Used for scenarios such as measuring QPS and similar metrics
func EmitCounter(name string, value float64, tags map[string]string) error {
}
// Used for scenarios such as measuring elapsed time, where analysis of mean and quantile is required
func EmitTimer(name string, value float64, tags map[string]string) error {
}
// Used for absolute value measurement scenarios
func EmitGauge(name string, value float64, tags map[string]string) error {
}
```


Refer to [metrics feature description](https://github.com/volcengine/apminsight-server-sdk-go/tree/master/metrics) for specific integration methods.

<span id="RiE0pnQL"></span>
### **Supported frameworks list**


|**Framework** |**Version** |
|---|---|
|gin\-gonic/gin |1.x |
|gorm.io/gorm.v1 |1.x |
|net/http |\- |
|sirupsen/logrus |1.x |
