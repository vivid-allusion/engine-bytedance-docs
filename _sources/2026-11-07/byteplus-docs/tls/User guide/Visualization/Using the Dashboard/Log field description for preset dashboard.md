---
title: "Log field description for preset dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Description_of_preset_template_dashboard_log_fields"
---

TLS supports creating dashboard based on preset templates like JuiceFS, VPC, CDN, ALB, APIG, VKE , and CLB.

Before you create a dashboard using a preset template, the system validates the selected log topic fields based on the specified template and automatically matches the corresponding **index fields** by name. If a field is missing, the field type differs, or statistics are not enabled, you need to manually select fields from the log topic to replace those specified in the preset template. You can also refer to [Configure index](https://docs.byteplus.com/docs/tls/Configure-indexes-2) to add or modify fields.

This topic introduces the preset log topic fields in the preset dashboard template. For instructions on how to create dashboards, see [Create a blank dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard).

<span id="85c0955e"></span>
## JuiceFS preset dashboard fields


|Field name |Field type |Description |
|---|---|---|
|uid |long |User ID. |
|gid |long |Group ID. |
|pid |long |Process ID. |
|op |text |Type of operation. |
|delay |double |Operation delay. |
|inode |long |Index node number of the file. |
|length |long |Written data length. |
|offset |long |Write offset. |
|filename |text |Filename to search for. |
|filehandle |long |File handle. |
|status |text |Operation status. |
|mode |text |File permissions and type information. |
|parent_inode |long |Parent directory inode number for query operations. |
|others |text |Other information. |
|time |text |Log timestamp. |
|unknown |text |Unknown field. |


<span id="9a90cebb"></span>
## VPC preset dashboard fields


|Field name |Field type |Description |
|---|---|---|
|srcaddr |text |Source address of the traffic. |
|dstaddr |text |Destination address of the traffic. |
|srcport |text |Source port of the traffic. |
|dstport |text |Destination port of the traffic |
|protocol |long |IANA protocol number of the traffic |
|packets |long |The count of packets transmitted. |
|bytes |long |The count of bytes transmitted. |
|action |text |Operation associated with traffic. |
|logstatus |text |Log recording status for flow logs. |


<span id="ddeb7893"></span>
## CDN preset dashboard fields


|Field name |Field type |Description |
|---|---|---|
|domain |text |The domain name in the request URL, i.e., the acceleration domain name. |
|ds_http_status |long |CDN response status code. |
|ds_http_uri_path |text |The path in the request URL, starting with a slash (/). |
|client_ip_province |text |The Chinese provincial administrative region to which the client IP address belongs. |
|client_ip_isp |text |The Chinese network operator to which the client IP address belongs. |
|client_ip |text |The client IP address that sends the request. |
|ds_http_referer |text |Value of the Referer header in the request. If the request does not include this header, the parameter value is `–`. |


<span id="88c50b93"></span>
## ALB preset dashboard fields

<span id="88c50b93"></span>
### ALB second\-level metric monitoring


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |ALB instance ID.<br><br>This field is included in the log file name. Therefore, log file content will not display this field. |
|request_time |text |The duration for an ALB instance to respond to a client request, i.e., the request processing time.<br><br>The total time consumed from the moment the ALB instance receives the first byte of the client request to the moment the ALB instance sends the last byte to the client, measured in seconds.<br><br>The entire process involves the following: a client sends a request to the ALB instance; the ALB instance forwards the request to the backend server; the backend server returns the response data to the ALB instance; and the ALB instance forwards the data to the client. |
|upstream_response_time |text |The duration for the backend server to respond to client requests.<br><br>The time from when the ALB instance begins connecting to the backend server until the backend server response is complete, measured in seconds. |
|request_length |text |Byte size of the request. |
|bytes_sent |text |The size of the response message from the ALB instance to the client request, i.e., the number of bytes of data sent by the ALB instance to the client. |
|status |text |The response status code of the ALB instance, i.e., the status code returned by the ALB instance to the client. |
|upstream_status |text |Status code returned by the backend server to the ALB instance. |
|__time__ |long |Log timestamp. |


<span id="adf7246b"></span>
### ALB access overview


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |ALB instance ID.<br><br>This field is included in the log file name. Therefore, log file content will not display this field. |
|remote_addr |text |IP address of the client request. |
|http_user_agent |text |User\-Agent field in the request header. |
|http_host |text |Host field in the request header. |
|__time__ |long |Log timestamp. |


<span id="3bb7267e"></span>
### ALB monitoring center


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |ALB instance ID.<br><br>This field is included in the log file name. Therefore, log file content will not display this field. |
|status |text |The response status code of the ALB instance, i.e., the status code returned by the ALB instance to the client. |
|upstream_response_time |text |The duration for the backend server to respond to client requests.<br><br>The time from when the ALB instance begins connecting to the backend server until the backend server response is complete, measured in seconds. |
|request_length |text |Byte size of the request. |
|bytes_sent |text |The size of the response message from the ALB instance to the client request, i.e., the number of bytes of data sent by the ALB instance to the client. |
|request_time |text |The duration for an ALB instance to respond to a client request, i.e., the request processing time.<br><br>The total time consumed from the moment the ALB instance receives the first byte of the client request to the moment the ALB instance sends the last byte to the client, measured in seconds.<br><br>The entire process involves the following: a client sends a request to the ALB instance; the ALB instance forwards the request to the backend server; the backend server returns the response data to the ALB instance; and the ALB instance forwards the data to the client. |
|remote_addr |text |IP address of the client request. |
|http_host |text |Host field in the request header. |
|request |text |Request sent by the client. |
|__time__ |long |Log timestamp. |


<span id="639ee40d"></span>
## APIG preset dashboard fields


|Field name |Field type |Description |
|---|---|---|
|gateway_id |text |The user's gateway instance. |
|downstream_remote_address |text |Client address connected to the gateway. |
|duration |long |Total request duration, measured in ms. |
|response_code |long |HTTP response status code. |


<span id="a3e207e8"></span>
## VKE Pod preset dashboard fields


|Field name |Field type |Description |
|---|---|---|
|involvedObject_kind |text |Kubernetes resource type for the corresponding event. |
|type |text |Event level. |
|source_component |text |Event source. |
|reason |text |Event type. |
|source_host |text |Source Host. |
|message |text |Details. |
|metadata_name |text |Pod name. |
|metadata_namespace |text |Kubernetes namespace. |
|__time__ |long |Log timestamp. |


<span id="9ab25bc9"></span>
## CLB Preset dashboard fields

<span id="7b757f99"></span>
### CLB monitoring center


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |CLB instance ID.<br><br>This field is included in the log file name. Therefore, log file content will not display this field. |
|status |long |The response status code from the CLB instance, i.e., the status code that CLB instance returns to the client. |
|upstream_response_time |double |The duration for the backend server to respond to client requests.<br><br>The time from when the CLB instance begins connecting to the backend server until the backend server response is complete, measured in seconds. |
|request_length |long |Byte size of the request. |
|bytes_sent |long |The size of the response message from the CLB instance to the client request, i.e., the number of bytes of data sent by the CLB instance to the client. |
|request_time |double |The duration of a CLB instance responding to client requests. |
|remote_addr |text |IP address of the client request. |
|http_host |text |Host field in the request header. |
|request |text |Request sent by the client. |
|__time__ |long |Log timestamp. |


<span id="98bc31a1"></span>
### CLB access overview


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |CLB instance ID. This field is included in the log file name. Therefore, log file content will not display this field. |
|remote_addr |text |IP address of the client request. |
|http_user_agent |text |User\-Agent field in the request header. |
|http_host |text |Host field in the request header. |
|__time__ |long |Log timestamp. |


<span id="dbe157f0"></span>
### CLB second\-level metric monitoring


|Field name |Field type |Description |
|---|---|---|
|loadbalancer_id |text |CLB instance ID.<br><br>This field is included in the log file name. Therefore, log file content will not display this field. |
|request_time |double |The duration of a CLB instance responding to client requests. |
|upstream_response_time |double |The duration for the backend server to respond to client requests.<br><br>The time from when the CLB instance begins connecting to the backend server until the backend server response is complete, measured in seconds. |
|request_length |long |Byte size of the request. |
|bytes_sent |long |The size of the response message from the CLB instance to the client request, i.e., the number of bytes of data sent by the CLB instance to the client. |
|status |long |The response status code from the CLB instance, i.e., the status code that CLB instance returns to the client. |
|upstream_status |long |The status code returned by the backend server to the CLB instance. |
|__time__ |long |Log timestamp. |


<span id="5920fabe"></span>
## Nginx preset dashboard fields

<span id="efc18f13"></span>
### Nginx access dashboard


|Field name |Field type |Description |
|---|---|---|
|http_user_agent |text |User\-Agent field value in the request header.<br><br>Contains identification information such as the client’s browser type, operating system, and version. |
|remote_addr |text |Client IP address.<br><br>For proxied requests, this may be the proxy server IP address. |
|status |long |HTTP response status code.<br><br>For example, 200: a successful request; 404: resource not found; 500: a server error. |
|url |text |URL path of the request.<br><br>This path is usually related to request_uri, and may not include query parameters, depending on log configuration. The path is used to simplify identification of the requested resource path. |
|host |text |Value of the Host field in the request header.<br><br>It is used to identify target hostname or domain name of the client request. |


<span id="ae0e056b"></span>
### Nginx monitoring dashboard


|Field name |Field type |Description |
|---|---|---|
|proxy_upstream_name |text |Upstream name in the Nginx configuration when acting as a reverse proxy.<br><br>Identifies the backend service cluster to which the current request is forwarded. |
|status |long |HTTP response status code.<br><br>For example, 200: a successful request; 404: resource not found; 500: a server error. |
|body_bytes_sent |long |Number of bytes sent in the response body to the client (excluding response headers). |
|remote_addr |text |Client IP address.<br><br>For proxied requests, this may be the proxy server IP address.. |
|request_length |long |Total length of the client request, including headers and body.<br><br>Unit: bytes. |
|url |text |URL path of the request.<br><br>This path is usually related to request_uri, and may not include query parameters, depending on log configuration. The path is used to simplify identification of the requested resource path. |
|request_method |text |The HTTP request method.<br><br>Such as GET, POST, PUT, DELETE, HEAD, and more. |
|request_time |long |Total time spent by Nginx to process a request.<br><br>The time from receiving the request to sending the response, measured in seconds. |


<span id="26ee83f0"></span>
## VeADK preset dashboard fields

<span id="8fcb29b3"></span>
### VeADK observability


|Field name |Field type |Description |
|---|---|---|
|Attributes.app.name |text |Application name. |
|Attributes.agent.name |text |Intelligent agent name. |
|Attributes.user.id |text |User ID. |
|Attributes.session.id |text |Session ID. |
|Attributes.gen_ai.tool.input |text |Tool invocation input. |
|Attributes.gen_ai.tool.output |text |Tool invocation output. |
|Attributes.gen_ai.tool.name |text |Name of the tool being called. |
|Attributes.gen_ai.usage.input_tokens |long |Total count of tokens in all contexts. |
|Attributes.gen_ai.usage.output_tokens |long |Count of tokens generated by the model. |
|Attributes.gen_ai.usage.total_tokens |long |Count of tokens for prompt and completion |
|Attributes.gen_ai.usage.cache_create_input_tokens |long |Number of input tokens newly cached in this request. |
|Attributes.gen_ai.usage.cache_read_input_tokens |long |Number of input tokens read directly from the cache in this request. |
|StatusCode |text |The status code that represents the state of a span.<br><br>It is usually used to indicate the outcome of an operation, such as success or error. |
|Duration |long |The duration of a span, i.e., the time elapsed from start to end. |
|End |long |The timestamp when the span ends. |
|Kind |text |Type or category of span. It is used to differentiate various operation types. |
|Name |text |Name of the span. |
|ParentSpanID |text |Unique identifier for the parent span.<br><br>It is used to establish hierarchy among spans, indicating which span initiated the current one. If it is a root span, this field may be empty. |
|ServiceName |text |Name of the service that generated the span.<br><br>It is used to identify which service performed this operation, facilitating locating services in distributed systems. |
|SpanID |text |Unique identifier for the span. |
|Start |long |The timestamp at the start of the span. It records the specific time point when the operation began. |
|StatusDescription |text |Text description of the status code. It further explain the specific outcome of the operation. |
|TraceID |text |Unique identifier for the entire distributed trace.<br><br>A trace contains multiple related spans. All spans belonging to the same trace share the same TraceID. |
|TraceState |text |It is used to transfer vendor\-specific information in distributed tracing.<br><br>A set of key\-value pairs that carries custom trace information across services. |


<span id="ae6466d9"></span>
## WAF preset dashboard fields

<span id="2be8b2a4"></span>
### WAF overview


|Field name |Field type |Description |
|---|---|---|
|ActionType |text |WAF execution action. |
|Status |long |HTTP status code that WAF returns to client requests. |
|MatchedHost |text |WAF access domain name. |
|HitInfo |text |Secondary rule type after matching a protection policy type. |
|UserAgent |text |The User\-Agent field in the client request header contains information such as the client browser identifier and operating system identifier. |
|Host |text |The Host field in the client request header, i.e., the actual domain accessed by the client. |
|Plugin |text |Protection rule type. |
|ClientIP |text |Client IP. |
|PolicyID |text |Rule IP. |
|AttackType |text |Attack type. |
|VerificationStatus |text |Action that is taken when verification succeeds. |
|APIStatus |text |API status. |
