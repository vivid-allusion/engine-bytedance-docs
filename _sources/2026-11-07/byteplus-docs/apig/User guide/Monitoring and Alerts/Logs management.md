---
title: "Logs management"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Logs_management"
---

The API gateway based on [Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS) provides persistent storage for user access logs, facilitating business observation of client, gateway, and backend service actions, and meeting troubleshooting and auditing requirements. This article introduces how to deliver and query gateway logs, as well as the fields delivered by the logs.

<span id=".5byA5ZCv5pel5b-X5oqV6YCS"></span>
## Enable log delivery

The API gateway supports delivering logs to Torch Log Service to achieve persistent storage.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">APIG instances created before December 15, 2023, 00:00:00 do not support self\-service log delivery activation. If you need to deliver logs, please <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx">Submit a ticket</a> to apply.</div>


<span id="EBC0XxrW"></span>
### Prerequisites


* Torch Log Service has been activated. Using the Torch Log Service will incur charges. 

* Log projects have been created.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The API Gateway supports automatic creation of log topics, or you can use your own log topics.</div>


<span id="Aj4FQ0wg"></span>
### Configuration when creating an APIG instance

When creating an instance, in the **Observability** area, **check Use Torch Log Service** to deliver the access log of the gateway to TLS. Specific actions refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance) .

<span id="HMG2gRSL"></span>
### Configuration for existing APIG instances


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig), select the target region from the top navigation bar.

2. In the left **navigation bar**, click on the target instance name and enter the Overview page.

3. Switch to the Log tab, click **to choose**, and select the desired log project and log topic.



|Parameter |Description |
|---|---|
|log project |A log project is a basic resource management unit in the log service, used for log resource isolation and access control among multiple users or multiple projects/products. Please select the target log project. |
|log topic |The log topic is the basic unit for Logs management in Torch Log Service, each log topic is used to carry different types or classifications of logs within the same application.<br><br><br>* **Default configuration**: By selecting the default configuration, a topic named `APIG id-accessLog` will be automatically generated under the current project.<br><br>* **Use existing topic**: Choose to use an already created topic. |



4. Click **confirm** to complete the log delivery configuration.


<span id=".57yW6L6R5pel5b-X6YWN572u"></span>
## Edit log configuration

By editing the log configuration, you can turn off log delivery, or switch to a different log project and log topic.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please be cautious when switching the log project and log topic for delivery! After switching, you will not be able to query the historical logs delivered to the original project and topic on the APIG side.</div>



1. On the Log tab of the current gateway, click the edit icon of the log configuration.

2. In the pop\-up dialog, modify the turn\-on status, log project, and log topic as needed.

3. Click **confirm** to complete modifications.


<span id=".5p-l6K-i5pel5b-X"></span>
## Search logs

On the Log tab of the current APIG instance, select the target time range, click **search**, and query the log results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The log search box is set to automatically carry the APIG id, making it easier for you to view the access logs of the target instance.</div>


<span id=".5pel5b-X5oqV6YCS5a2X5q616K-05piO"></span>
## Description of log fields

Description of fields involved in APIG log delivery is as follows:


|Field name. |field type |Field description |
|---|---|---|
|__time__ |long |Time when the log was generated. |
|gateway_id |string |APIG instance ID. |
|authority |string |Host Header in the request message. |
|bytes_received |long |Size of the request's Body (excluding Header). |
|bytes_sent |long |Size of the response body (excluding Header). |
|downstream_local_address |string |Gateway Pod address. |
|downstream_remote_address |string |Address of the client connected to the APIG instance. |
|duration |long |Request total duration. The unit is milliseconds. |
|method |string |HTTP method. |
|path |string |Path in the HTTP request. |
|protocol |string |The HTTP protocol version. |
|request_id |string |The gateway generates an ID for each request and places it in the x\-request\-id in the Header for backend tracing and troubleshooting. |
|requested_server_name |string |Server Name used during the SSL connection. |
|response_code |long |HTTP response status code. |
|response_flags |string |Reason for the response failure. |
|route_name |string |Route Name. |
|start_time |string |Request start time. Format: UTC. |
|trace_id |string |Trace ID。 |
|upstream_cluster |string |Upstream cluster. |
|upstream_host |string |Upstream IP. |
|upstream_local_address |string |Local address connecting upstream. |
|upstream_service_time |long |The time taken by the upstream service to process the request (in milliseconds), including the network time taken by the gateway to access the upstream service and the processing time taken by the upstream service itself. |
|upstream_transport_failure_reason |string |Reason for the failure of the upstream link. |
|user_agent |string |UserAgent in the HTTP Header. |
|x_forwarded_for |string |The x\-forwarded\-for in the HTTP header is typically used to represent the real IP of the HTTP request origin. |
