---
title: "Log field description"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Log_field_description"
---

AgentKit\-specific logs are stored in the `apmplus-server-log` log topic under the `apmplus-server` project. Descriptions of the corresponding log fields are in the table below.


|Field name |Sample value |Description |
|---|---|---|
|attribute |`{"exception.message":"helloworld","exception.type":"*errors.fundamental","foo":"bar","span_id":"698e4273e1a06c01"}` |Additional attributes of the log, in JSON format. |
|file_line |`uptracezap_demo.go:10` |The line number in the source file that emitted the log entry. |
|file_name |`uptracezap_demo.go` |The name of the source file that emitted the log entry. |
|hostname |`test-log-demo-778b86****-jm8t5` |The hostname of the container or virtual machine that generated the log. |
|log_level |`INFO` |The log level. Valid values:<br><br><br>* **DEBUG**: Debugging logs<br><br>* **INFO**: Informational logs<br><br>* **WARN**: Warning logs<br><br>* **ERROR**: Error logs<br><br>*  **???** : Default value. `???` appears when the log level is not set. |
|message |`this is uptrace zap error log demo` |The raw log text emitted by the application. |
|resource |`{"host.arch":"arm64","host.type":"vm_demo","service.version":"1.0.0"}` |Resource attributes associated with the log, in JSON format. This may include, but is not limited to, fields such as container_id, instance_id, host.arch, and service.version. |
|service |`test-log-demo` |The service name. |
|source |`otl-collector` |The collection source, which indicates different collection methods. |
|trace_id |`3e0022a380c4bc0c10feb18da17a****` |The trace ID (TraceId), used to locate a unique request trace. |


&nbsp;

<span id="t2H8cKkg"></span>
##
