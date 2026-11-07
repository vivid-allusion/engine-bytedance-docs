---
title: "Access log delivery to TOS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Sending-access-logs-to-TOS"
---

Application Load Balancer (ALB) supports the access log delivery to TOS feature. This topic describes how to enable the Access Log Delivery to TOS function in the ALB console to obtain access logs for ALB instances.

> **tip**

> The ALB access log delivery to TOS feature is currently in beta stage. If you need a trial, please contact your account manager.

## Feature overview

* ALB can periodically deliver an instance's access logs to a specified BytePlus Torch Object Storage (TOS) bucket. You can use these logs for troubleshooting, analyzing user profiles, and then implementing precise operational activities.

* ALB packages access logs every 5 minutes and compresses the log package before delivery. The delivery directory structure is /ALBAccessLogs/*YYYY*/*MM*/*DD*. If the directory does not exist, it will be created automatically. The retention period for log files is determined by the bucket's configuration. For log field explanations, see [Field description](https://docs.byteplus.com/docs/clb/Sending-access-logs-to-TOS#.5a2X5q616K-05piO).

   > **tip**

   > BytePlus  Torch Object Storage (TOS) is a massive, secure, low\-cost, easy\-to\-use, highly reliable, and highly available distributed cloud storage service provided by the BytePlus . After ALB enables access log delivery to TOS, it regularly processes log data and packages it for delivery to the TOS bucket for storage. This suits scenarios requiring long\-term storage of massive data, offering low storage costs and high cost performance.

## Prerequisites

You have activated TOS service and created a TOS bucket to receive access logs from ALB instances. For more information, see [Creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

## Enable access log delivery to TOS

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Instance**.

4. Click the name of the target ALB instance.

5. Click **Edit configuration** next to **Access log delivery to TOS**.

6. Enable access log and select a bucket from the dropdown list.

   > **warning**

   * > When enabling the Access Log feature for the first time, the system will automatically create the role [ServiceRoleForALB](https://console.byteplus.com/iam/identitymanage/role/ServiceRoleForALB) for you to obtain authorization to deliver logs to the specified bucket.

   * > Deleting the role will cause cross\-service authorization to fail, preventing log delivery for all instances with access logs enabled. Please proceed with caution.

7. Click **Save** to complete the action.

## Disable access log delivery to TOS

* The Access Log Delivery to TOS feature can be stopped at any time. You can click **Edit configuration** next to **Access log delivery to TOS** and disable **Access Log**.

* After stopping Access Log Delivery to TOS, logs already delivered will continue to be retained in TOS. The retention period depends on the TOS storage type.

* When re\-enabling Access Log Delivery to TOS, you need to reselect the storage bucket. When repeatedly enabling/stopping delivery on the same day and the delivery target is the same bucket, the storage directory is created only once.

## Field description

|Field |Explanation |Example |
|---|---|---|
|loadbalancer_id |Indicates the ALB instance ID. This field is included in the log file name. It is not present within the log file content. |\-\- |
|protocol_type |Indicates the protocol type used by the client request. |[https] |
|time_iso8601 |Indicates the completion time and timezone of the request's response. Timestamp in standard ISO format. The trailing +08:00 indicates the time zone is UTC+8, i.e., Beijing Time. |[2021\-08\-10T17:39:29+08:00] |
|remote_addr |Indicates the IP address of the client request. |[180.184.65.180] |
|remote_port |Indicates the port number used by the client request. |[49540] |
|request |Indicates the request sent by the client. |[GET /v1/_proxy/disease/getContentByType/44672585629444/5 HTTP/1.1] |
|http_user_agent |Indicates the User\-Agent field from the request headers. |[Mozilla/5.0 (Linux; Android 10; ; wv) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/... Mobile Safari/. VivoBrowser/...] |
|http_host |Indicates the Host field in the request header. |[m.baikemy.com] |
|http_referer |Indicates the source address of the request. |[https://www.zhihu.com/] |
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
|servicegroup_name |Indicates the name of the server group. |[sg\-x] |
