---
title: "Access log overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Access-log-overview"
---

## Introduction​

CLB supports delivering access log data of layer 7 (HTTP/HTTPS) listeners to object storage TOS and log service TLS, facilitating user access behavior analysis or troubleshooting.

## Basic information

### Capabilities

**Deliver to log service TLS**

CLB delivers access logs to TLS. The related basic information is as follows:

|Concept |Explanation |
|---|---|
|Index |After enabling the **access Log delivery TLS ** feature, the default configuration uses the [log fields](https://docs.byteplus.com/en/docs/clb/Access-log-overview#MLdBptPB) mentioned below to configure key\-value indices for the log topic.<br><br>> **tip**<br><br><br>> The default configuration key value index will override the original index configuration of the log topic, please operate with caution. To modify index, see [Viewing and modifying index](https://docs.byteplus.com/en/docs/clb/Access-Log-Delivery-to-TLS#KVGZMp9V).<br> |
|Search query |A search and analysis statement consists of a search statement and an SQL analysis statement, separated by a pipe symbol (\|). This syntax indicates that data statistics and analysis are performed on the results that match the search conditions.  |
|Log project |The fundamental resource management unit in the Torch Log Service (TLS), used for log resource isolation and Identity and Access Management (IAM). |
|Log topic |The basic unit for log management (such as log collection, storage, query, and analysis) in TLS. |

**Deliver to object storage TOS**

CLB delivers generated log files to TOS for storage. Basic information of the generated log files is as follows:

|Concept |Explanation |
|---|---|
|Generation cycle |5 minutes. |
|file size |The file size is determined by the number of visits. |
|Data compression |Yes, the system compresses log files before uploading by default. |
|Save path |A CLB instance automatically creates the path /CLBAccessLogs/*YYYY*/*MM*/*DD* at the root directory of the bucket to store log files. |
|File name |The log file archive naming rule is: *loadbalancerid\-time_vip{_eip}* .log.gz.<br><br><br>* loadbalancerid represents the ID of the CLB instance;<br><br>* time indicates the start time of CLB access logs in the current log file;<br><br>* vip refers to the private IP address of the CLB instance;<br><br>* eip refers to the public IP address associated with the CLB instance. If it is a private instance without an associated public IP, the log file name does not include _eip.<br><br><br>> **tip**<br><br><br>> If you manually upload a file with the same name to the log storage path, it will overwrite the original automatically uploaded log file.<br> |
|Storage period |Determined by the bucket configuration in the Storage service. |
|File content |The [log fields](https://docs.byteplus.com/en/docs/clb/Access-log-overview#MLdBptPB) in the table below are listed in the order they appear in the log files from top to bottom. Log files do not display field names, only field values. Fields not involved in certain log files are represented by [\-]. |

### Log fields

|**Field** |**Explanation** |**Example** |
|---|---|---|
|loadbalancer_id |CLB Instance ID. This field is included in the log file name but is not present within the log file content. |\- |
|protocol_type |Protocol type of the client request. |[https] |
|time_iso8601 |The time and time zone when the access response is completed, using the standard ISO format. The suffix +08:00 indicates that the time zone is UTC plus 8 hours, which is Beijing Time. |[2021\-08\-10T17:39:29+08:00] |
|remote_addr |Client IP address. |[180.XX.XX.180] |
|remote_port |Client port number. |[49540] |
|eip |Public IP address bound to the CLB instance. This field applies only to Internet\-facing instances and does not apply to private instances. |[172.XX.XX.61] |
|request<br><br> |Request line. |[GET /v1/_proxy/disease/getContentByType/44672585629444/5 HTTP/1.1] |
|http_user_agent |User_agent field of the HTTP protocol header. |[Mozilla/5.0 (Linux; Android 10;  *; wv) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/... Mobile Safari/.*  VivoBrowser/ *.* . *.* ] |
|http_host |Requested domain name. |[www.volcengine.com] |
|http_referer |HTTP request source. |[https://www.volcengine.com] |
|request_length |Number of request bytes received from the client. |[19] |
|ssl_protocol |SSL protocol version. This field applies to HTTPS protocol listeners; other protocol listeners do not involve this field. |[TLSv1.2] |
|ssl_cipher |SSL cipher suite. This field applies to HTTPS protocol listeners; other protocol listeners do not involve this field. |[ECDHE\-RSA\-AES256\-GCM\-SHA384] |
|request_id |Request ID. |[5a7c044358167c90a69f280ddd70\*\*\*\*] |
|connection |Connection ID. |[18757\*\*\*\*] |
|connection_requests |Number of successfully connected requests. |[5] |
|vip |The private IP address of the CLB instance. |[192.XX.XX.134] |
|listener_id |Listener ID. |[lsn\-1g1hsc8ftjb408ibuxwr8\*\*\*\*] |
|vport |Listener port number. |[443] |
|tcpinfo_rtt |Round\-trip time of the TCP connection between CLB and the client, in milliseconds. |[0.121] |
|status |CLB instance response status code, the code returned by CLB to the client. |[200] |
|bytes_sent |CLB response byte count, which is the number of bytes CLB sends to the client. |[1069] |
|request_time |CLB response time, which is the total time from receiving the first byte of the client request to sending the last byte back to the client, including the client request to CLB, CLB forwarding the request to the backend server, backend server responding to CLB, and CLB forwarding data to the client, measured in seconds. |[0.252] |
|server_name |Matched forwarding rule domain, which is the server name matched by the rule and can be a wildcard domain. |[\*.baikemy.com] |
|servergroup_id |Backend server group ID. |[rsp\-2fel2y2rplp8g5oxruwa2\*\*\*\*] |
|upstream_addr |IP address and port number of the backend server handling the request.<br><br>If the request is abnormal, this field records nginx's upstreamID. |[192.168.1.198:3000] |
|upstream_connect_time |Time for CLB to establish a TCP connection with the backend server, measured from starting the connection to starting to send the HTTP request, in seconds. |[0.231] |
|upstream_header_time |CLB measures the time spent receiving HTTP headers from the backend server, from the moment the connection to the backend server starts until the HTTP response headers are fully received. The unit is seconds. |[0.020] |
|upstream_response_time |Backend server response time, the total time spent on the backend request, from starting the connection to the backend server until receiving the complete response from the backend server, measured in seconds. |[0.566] |
|upstream_status |Backend server response status code, the status code returned to CLB by the backend server. |[200] |

## Billing description

Regarding access log billing, CLB currently does not charge; the billing is handled by Torch Log Service (TLS) or Torch Object Storage (TOS).

If access logs are delivered to Torch Log Service (TLS), charges follow the Torch Log Service (TLS) billing standards.

If access logs are delivered to Torch Object Storage (TOS), charges follow the Torch Object Storage (TOS) billing standards.
