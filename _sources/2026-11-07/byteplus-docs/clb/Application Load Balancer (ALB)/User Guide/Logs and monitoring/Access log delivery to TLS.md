---
title: "Access log delivery to TLS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Sending-access-logs-to-TLS"
---

ALB supports the access log delivery to TLS feature. Compared to delivering logs to TOS, delivering access logs to TLS offers higher real\-time performance. It eliminates the need for you to decompress log packages and allows you to directly view and analyze log entries. This topic describes how to enable the Access Log Delivery to TLS function in the ALB console to view or analyze the access logs of ALB instances.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

By integrating with BytePlus Torch Log Service (TLS), ALB can deliver access logs to TLS. You can perform real\-time search and analysis of access logs in the ALB console. ALB can conduct SQL analysis and calculations based on the log search results and present the analysis outcomes in the form of charts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS is a one\-stop service provided by BytePlus for log\-type data. It offers log collection, massive storage, search and analysis, monitoring and alerting, and data visualization. It is suitable for scenarios such as application operation and maintenance, service monitoring, and compliance with security standards, comprehensively enhancing R&D and operational efficiency. ALB, combined with TLS, supports using keywords to search logs, enabling quick pinpointing of abnormal events. It also supports using SQL for real\-time statistics and analysis of logs, facilitating rapid access to key data.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have activated the TLS and created a log project and a log topic.

<span id=".5byA5ZCv6K6_6Zeu5pel5b-X5oqV6YCSdGxz"></span>
## Enable access log delivery to TLS


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **Instance**.

3. Click the target ALB instance name.

4. On the **Access log analysis** tab, click **Configure access log delivery to TLS**.

5. On the **Configure access log delivery tab**, enable the **Access log delivery to TLS** feature.

6. Select the **Log project** and **Log topic** from the dropdown list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ALB does not charge for log delivery; you only need to pay for TLS usage.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When enabling the health check log delivery/access log analysis feature for the first time, you need to authorize the TLS service for your service role <a href="https://console.byteplus.com/iam/identitymanage/role/ServiceRoleForALB">ServiceRoleForALB</a> to perform subsequent delivery operations.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deleting the service role will cause cross\-service authorization to fail, preventing log delivery for all instances with access logs enabled. Please proceed with caution.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no log project or log topic is available for selection, you can create them first and then make your choice.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Logs from one instance can only be delivered to one specified log topic, but a single log topic can receive logs from different instances.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to deliver access logs and health check logs to different log projects or log topics for easier management and to avoid inconsistencies in searchable fields.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log data may fail to be delivered if the data volume exceeds the write limit of the log topic. It is recommended to choose an appropriate log topic based on your business traffic volume. You can manually set the number of shards for a log topic or enable automatic sharding in the TLS console.    </div>
   

7. Click **Confirm** to complete the action.


<span id=".5YWz6Zet6K6_6Zeu5pel5b-X5oqV6YCSdGxz"></span>
## Disable access log delivery to TLS


* The Access Log Delivery to TLS feature can be stopped anytime. In the **Access log analysis** tab, you can click **Configure** and disable **Access Log**.

* After stopping Access Log Delivery to TLS, you will not be able to view the current log analysis page in the ALB console.

* Logs already delivered will continue to be retained in TLS. The retention period depends on the TLS configuration for the log topic. You can go to the TLS console to view historical log data.

* When re\-enabling log delivery to TLS, you must reselect the log project and log topic.


<span id=".6K6_6Zeu5pel5b-X5YiG5p6Q"></span>
## Access log analysis


* You can perform real\-time search and analysis of access logs in the ALB console. ALB can conduct SQL analysis and calculations based on the log search results and present the analysis outcomes in the form of charts.

* For detailed information on the functionalities of different modules in log analysis, search syntax, configuration instructions, etc., see [Search and analysis](https://docs.byteplus.com/en/docs/tls/Query-and-analysis-2) in the TLS documentation.


<span id=".5a2X5q616K-05piO"></span>
## Field description

The table below lists the fields that can be included in ALB access logs. Except for the alb_headers field, other fields are included in the access logs by default. The alb_headers field is only included in the access logs after being specifically configured. For detailed information, please see the field descriptions in the table below.


|Field |Explanation |Example |
|---|---|---|
|loadbalancer_id |Indicates the ALB instance ID. This field is included in the log file name. It is not present within the log file content. |\- |
|protocol_type |Indicates the protocol type used by the client request. |[https] |
|remote_addr |Indicates the IP address of the client request. |[180.xx.xx.180] |
|remote_port |Indicates the port number used by the client request. |[49540] |
|request |Indicates the request sent by the client. |[GET /v1/_proxy/disease/getContentByType/44672585629444/5 HTTP/1.1] |
|http_user_agent |Indicates the User\-Agent field from the request headers. |[Mozilla/5.0 (Linux; Android 10; ; wv) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/... Mobile Safari/. VivoBrowser/...] |
|http_host |Indicates the Host field in the request header. |[m.baikemy.com] |
|http_referer |Indicates the source address of the request. |[https://www.zhihu.com/] |
|http_x_forwarded_for |Indicates the content of the X\-Forwarded\-For request header. The first address in the X\-Forwarded\-For field is the client's real IP. The specific format is as follows: `X-Forwarded-For: client-real-IP, proxy-server-1-IP, proxy-server-2-IP, ...` |[192.168.11.1] |
|request_length |Indicates the size of the request in bytes. |[19] |
|ssl_protocol |Indicates the SSL cipher suite used for the request. This field is not included for HTTP requests. |[TLSv1.2] |
|ssl_cipher |Indicates the SSL cipher suite used by the request. This field is not included for HTTP requests. |[ECDHE\-RSA\-AES256\-GCM\-SHA384] |
|request_id |Indicates the request ID. |[rewewert234w\*\*\*\*\*\*] |
|connection |Indicates the TCP connection ID between the request and the ALB instance. |[casd1345zxcasd\*\*\*\*\*\*] |
|connection_requests |Indicates the number of completed requests processed on the TCP connection between the client and the ALB instance. |[5] |
|vip |Indicates the private IP address of the ALB instance. |[192.168.33.134] |
|eip |Indicates the EIP address of the ALB instance. This field is not included if the ALB instance is a private instance. |[172.16.3.61] |
|listener_id |Indicates the ID of the listener that served the request. |[lsn\-3tl161ztae4l928\*\*\*\*\*\*] |
|vport |Indicates the port on which the listener is listening. |[443] |
|tcpinfo_rtt |Indicates the Round\-Trip Time (RTT) during the TCP connection establishment between the client and the ALB instance, in microsecond. |[1210] |
|status |Indicates the response status code from the ALB instance, i.e., the status code returned by ALB to the client. |[200] |
|bytes_sent |Indicates the size of the response message from the ALB instance to the client, i.e., the number of bytes of data sent by ALB to the client. |[1069] |
|request_time |Indicates the duration of the ALB instance's response to the client request, i.e., the request processing time. This is the time elapsed from the ALB instance receiving the first byte from the client until it sends the last byte to the client. Unit: seconds. The whole process includes the client request transmission, ALB forwarding to the backend server, backend server response, and ALB forwarding the response to the client. |[0.252] |
|server_name |Indicates the domain name configured in the matched forwarding rule. The domain name configured in the forwarding rule. This can be a wildcard domain. |[\*.baikemy.com] |
|servergroup_id |Indicates the ID of the backend server group. |[rsp\-3tl161zn6y4e8i\*\*\*\*\*\*] |
|upstream_addr |Indicates the IP address and port number of the backend server processing the request.<br><br>If the request encounters an error, this field will record NGINX's upstream ID. |[192.168.1.198:3000] |
|upstream_connect_time |Indicates the time taken for the ALB instance to establish a TCP connection with the backend server. This refers to the time consumed from when ALB starts connecting to the backend server until it begins sending the HTTP request, in seconds. |[0.231] |
|upstream_header_time |Indicates the time taken for the ALB instance to receive the response headers from the backend server. This is the time from when the ALB instance starts connecting to the backend server until it finishes receiving the backend server's response headers. Unit: seconds. |[0.020] |
|upstream_response_time |Indicates the time taken by the ALB instance to process the client request. This is the time from when the ALB instance starts connecting to the backend server until the backend server's response ends. Unit: seconds. |[0.566] |
|upstream_status |Indicates the status code returned by the backend server to the ALB instance. |[200] |
|alb_headers |Indicates custom request headers. In log records, custom headers have a length limit of 1KB.<br><br>Note:<br><br><br>* To use this field, please contact your account manager to apply.<br><br>* After enabling **Access log delivery to TLS**, you also need to perform the following operations for this field:<br><br>   a. Enable the **Custom header for access log recording** feature on the listener's details page.<br><br>   b. Add this field to the log index. You can configure this field either on the **Access log analysis** tab of the instance details page in the ALB console or on the **Query and analysis** page for the specified log topic in the TLS console. For detailed operations, see [Configuring index](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2). |{Accept:\*/\*}, |
|servicegroup_name |Indicates the name of the server group. |[sg\-x] |


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
