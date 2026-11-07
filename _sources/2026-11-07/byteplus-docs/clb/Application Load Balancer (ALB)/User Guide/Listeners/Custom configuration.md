---
title: "Custom configuration"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Custom-configurations"
---

Application Load Balancer (ALB) provides custom configuration functionality at the listener level. Through the console, you can create and manage standard NGINX configuration policies. You can associate a configuration policy with a listener on its details page with one click, enabling personalized configurations to meet business needs without submitting a ticket.

## Create a custom configuration policy

### Procedure

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select Customization.

4. Click **Create custom configuration policy**.

5. See [Field description](https://docs.byteplus.com/docs/clb/Custom-configurations#.5a2X5q616Kej6YeK) and configure the policy according to your actual requirements.

6. Click **Save** to complete the action.

### Field description

|Field ||Required |Description |
|---|---|---|---|
|Name ||Yes |Assign a name to the created custom configuration policy for easier future management. The specific rules are as follows:<br><br><br>* Cannot start with `http://` or `https://`.<br><br>* Must start with a letter or Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, periods`.`, underscores`_`, and hyphens`-`.<br><br>* Length: 1 to 128 characters. |
|Description ||No |Description for the created custom configuration policy. The specific rules are as follows:<br><br><br>* Cannot start with `http://` or `https://`.<br><br>* Must start with a letter or Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, English comma`,`, period`.`, underscore`_`, space, equals sign`=`, hyphen`-`, full\-width comma`，`, and full\-width period`。`.<br><br>* If left blank, it defaults to an empty string.<br><br>* Length must be within 255 characters. |
|TLS protocol |Version (ssl_protocols) |No |After selecting the TLS protocol, TLSv1, TLSv1.1, and TLSv1.2 are chosen by default. ALB supports TLSv1.3. If you need a trial, please Submit ticket to apply. The specific rules are as follows:<br><br><br>* Supports single or multiple selection. When selecting multiple versions, they must be selected consecutively.<br><br>* Duplicate protocol configurations are not supported.<br><br>* After enabling TLSv1.3, ALB will automatically add the default TLSv1.3 cipher suites to your selected set. Modifying the TLSv1.3 cipher suites is currently not supported. |
||Cipher suite (ssl_ciphers) |No |Each protocol version supports different cipher suites. If left blank, the default cipher suite will be used. For details, see [Protocols and cipher suites](https://docs.byteplus.com/docs/clb/Custom-configurations#240172ba). |
|Keep\-alive time for persistent connections (keepalive_timeout) ||No |The keep\-alive time for persistent connections between the client and ALB. Default is 75 seconds, with a configurable range of 0\-900 seconds. |
|Connection timeout (proxy_connect_timeout) ||No |The connection establishment timeout between ALB and backend servers should be greater than the health check timeout. Default: 4s; Range: 4\-120s. |
|Maximum size of the client request body (client_max_body_size) ||No |The maximum size of client_body_timeout that can be accepted. Default is 60M, configurable in the range of 1\-30720M. |
|Request body cache ||Yes |This feature is enabled by default.<br><br><br>* On (Enables buffering of the client request body): ALB caches the request and forwards it to the backend server in chunks only after it has been fully received.<br><br>* Off (Disables buffering): ALB forwards the request to the backend server immediately upon receipt, which may impose some performance pressure on the backend server. |
|Custom response header (add_header) ||No |Add the specified fields to the response header. A maximum of 10 custom response headers can be configured.<br><br>One response header name can correspond to multiple values. For example, you can configure the response header name as Strict\-Transport\-Security and its value as "max\-age=63072000; includeSubdomains; preload".<br><br>The specific rules are as follows:<br><br><br>* Custom header name<br><br>   * Can contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>   * Length must be between 1 and 256 characters.<br><br>* Custom header value<br><br>   * Can contain English letters, numbers, spaces, and the following special characters: _ \- \* , / \ : @ = .( ) ;。<br><br>   * If the header value contains special characters other than numbers and letters, enclose the entire value in double ("") or single ('') quotes, such as `"POST, OPTIONS"`.<br><br>   * Length must be between 1 and 256 characters.<br><br>   * Must not contain "\r" or "\n".<br><br>* Always<br><br>   * Always is an optional configuration.<br><br>   * Always off: Custom response headers are added to the response only for status codes 200, 201, 204, 206, 301, 302, 303, 304, 307, 308. (primarily 2xx and 3xx)<br><br>   * Always on: Custom response headers are added to the response for all status codes (2xx, 3xx, 4xx, 5xx).<br><br><br>> **warning**<br><br><br>> If your service involves cross\-origin (CORS) scenarios, configure as follows based on your needs:<br><br><br><br>* > Allow cross\-origin requests using different methods<br><br><br>   * > Custom header name: `Access-Control-Allow-Methods`<br><br><br>   * > Custom header value: `"POST, OPTIONS"`<br><br><br>   * > Enable always if you need cross\-origin response headers to be available even for 4xx or 5xx status codes.<br><br><br>* > Specifies which domain names are allowed to access the ALB<br><br><br>   * > Custom header name: `Access-Control-Allow-Origin`<br><br><br>   * > Custom header value: A specific domain name. Using `*` allows requests from any origin to access the ALB.<br><br><br>   * > Enable always if you need cross\-origin response headers to be available even for 4xx or 5xx status codes.<br> |
|Add and overwrite response headers (more_set_headers) || |Adds the specified field(s) to the response headers and overwrites any existing values for fields with the same name. The specific rules are as follows<br><br><br>* header key<br><br>   * Can contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>   * Length must be between 1 and 256 characters.<br><br>* value<br><br>   * Allowed characters: letters, numbers, "_", "\-", "\*", ",", "/", ":", "@", "=", ".", "(", ")", ";", and spaces<br><br>   * Length: 1\-256 characters<br><br>   * Cannot contain "\r" or "\n"<br><br>* A maximum of 10 custom response headers can be configured. |
|Custom request header (more_set_input_headers) ||No |> **warning**<br><br><br>> Configuring custom request headers is an allowlist\-only feature. To use it, please contact your account manager.<br><br><br>Add specified fields to the request header. The specific rules are as follows:<br><br><br>* header key<br><br>   * A string composed of underscores (_), hyphens (\-), letters, and numbers.<br><br>   * Length must not exceed 128 characters.<br><br>   * Cannot start with a hyphen (\-).<br><br>   * Duplicate values are not allowed.<br><br>   * Header keys are case\-insensitive, and neither uppercase nor lowercase: x\-real\-ip, x\-forwarded\-for, x\-forwarded\-proto, x\-alb\-waf\-requestid, x\-alb\-waf\-real\-port, upgrade, connection, x\-vport, x\-vip, x\-clb\-cluster, x\-toutiao\-lb\-ip, x\-vni, content\-length, transfer\-encoding, keep\-alive, host, cookie, authority are supported.<br><br>* value<br><br>   * Must be either a variable or another string.<br><br>   * A string composed of letters, numbers, underscores (_), hyphens (\-), asterisks (\*), commas (,), forward slashes (/), at signs (@), equals signs (=), periods (.), parentheses, spaces, and single quotes. Must not contain semicolons (;).<br><br>   * Quotation marks (") can only appear at the beginning and end of the value.<br><br>   * No leading or trailing spaces are allowed.<br><br>   * Length must not exceed 128 characters.<br><br>   * When the value is a variable, the following are supported: $remote_addr, $proxy_add_x_forwarded_for, $remote_port, $scheme, $vport, $load_balancer_id, $remote_vni, $endpoint_id.<br><br>* A maximum of 10 custom response headers can be configured. |
|The timeout for reading a backend response (proxy_read_timeout) ||No |* Defines the timeout for ALB to read a response from a backend server.<br><br>* This timeout applies only between two consecutive read operations, not to the entire response transmission.<br><br>* If the backend server does not transmit any data within this period, the connection will be closed.<br><br>* Range: 30\-3600s. Default: 60s. |
|Timeout for forwarding requests to the backend (proxy_send_timeout) ||No |* Defines the timeout for establishing a connection with a backend server.<br><br>* This timeout applies only between two consecutive write operations, not to the entire request transmission process.<br><br>* If the backend server does not receive any data within this period, the connection will be closed.<br><br>* Range: 30\-3600s. Default: 60s. |
|Timeout for reading the client request header (client_header_timeout) ||No |* Defines the timeout for reading the client request header.<br><br>* If the client does not transmit the entire header within this period, an HTTP 408 error (Request Timeout) will be returned to the client.<br><br>* Range: 30\-120s. Default: 60s. |
|Timeout for reading the client request body (client_body_timeout) ||No |* Defines the timeout for reading the client_body_timeout.<br><br>* This timeout applies only to the interval between two consecutive read operations, not to the entire request transmission.<br><br>* If the client sends no data within this period, an HTTP 408 error (Request Timeout) is returned to the client.<br><br>* Range: 30\-120s. Default: 60s. |
|The timeout for reading a backend response (send_timeout) ||No |* Defines the timeout for sending a response to the client.<br><br>* This timeout applies only between two consecutive write operations, not to the entire response transmission process.<br><br>* If the client does not receive any content within this time, the connection will be closed.<br><br>* Range: 1\-3600s. Default: 60s. |
|Client certificate verification depth (ssl_verify_depth) ||No |* Defines the verification depth for the client certificate chain.<br><br>* Range: 3\-10. Default: 3. |
|SSL session expiration time<br><br>(ssl_session_timeout) ||No |* Defines the custom duration for which a client stores a Session Ticket. The client will delete the Ticket after it expires.<br><br>* Range: 1\-60 minutes. Default value: 10 minutes. |
|Backend response buffer size<br><br>(proxy_buffer_size) ||No |* Sets the buffer size for receiving backend responses.<br><br>* Range: 4\-32k. Default: 4k. |
|Client side request large header buffer<br><br>(large_client_header_buffers) ||No |* Set the maximum number and size of buffers used for reading large client request headers.<br><br>* The request line must not exceed the size of one buffer, otherwise a 414 error is returned to the client.<br><br>* A request header field must not exceed the size of one buffer, otherwise a 400 error is returned to the client.<br><br>* Maximum range: 4\-8. Default: 4.<br><br>* Size range: 8k\-32k. Default: 8k. |
|Response detection ||No |Whether the response information you configure needs to be checked. Default is off. |
|Pass\-through backend response header ||No |Forces the selected backend response headers to be passed through without being overwritten by ALB's own headers with the same name. |
|Ignore client exceptions ||Yes |Determines whether the connection between ALB and the backend server is terminated when the client actively interrupts the connection with ALB without waiting for a response. Disabled by default. |
|Additional HTTP header fields ||No |Add specified fields to the request header.<br><br><br>* X\-Forwarded\-Clientcert\-subjectdn: Used to retrieve the subject information of the client certificate accessing ALB.<br><br>* X\-Forwarded\-Clientcert\-clientverify: Used to obtain the verification result of the client certificate accessing the ALB. |
|Forward Host request header ||No |Whether to pass the client request's Host header through to the backend server. |
|Data compression |Data compression |No |Enable data compression.<br><br>> **tip**<br><br><br>> Data compression feature is currently in the invite\-only beta stage. For trial requests, please contact your account manager.<br> |
||Custom compression type |No |Select a compression type.<br><br><br>* By default, all types under **Common text formats (recommended: select all)**  and **XML and feed formats (select as needed)**  are selected.<br><br>* **Common text formats (recommended: select all)** <br><br>   * text/plain: plain text content, such as logs and .txt files.<br><br>   * text/css: Cascading Style Sheets, such as .css files.<br><br>   * text/javascript: JavaScript script (old standard).<br><br>   * application/javascript: JavaScript script (standard).<br><br>   * application/x\-javascript: JavaScript script (non\-standard).<br><br>   * application/json: JSON\-format data, such as API responses; most commonly used.<br><br>* **XML and feed formats (select as needed)** <br><br>   * text/xml: XML text (old standard).<br><br>   * application/xml: XML data (standard).<br><br>   * application/rss+xml: RSS feed, based on XML format.<br><br>   * application/atom+xml: Atom feed, based on XML format.<br><br>* **Binary and other formats (select with caution)** <br><br>   * application/x\-protobuf: Google Protobuf binary serialized data; select when using Protobuf for transmission.<br><br>   * application/octet\-stream: Binary stream of unknown format. Select this option only when the upstream incorrectly marks text content as this type. It is not recommended for images, ZIP, or other already\-compressed files, as compression will be ineffective and waste performance. |
||Custom compression threshold |No |Configure the compression threshold. Enable compression only when the response body size ≥ threshold (in bytes). Responses smaller than this threshold are not compressed and are returned as\-is.<br><br><br>* Value range: 200\-1024.<br><br>* Default: 200. |
||Custom compression level |No |Configure the compression level. The higher the level, the higher the compression ratio, but the greater the CPU usage and the longer the time.<br><br><br>* Value range: 1\-6.<br><br>* Default value: 5. |
|Max client request headers ||No |Configure the maximum number of request headers allowed per HTTP request.<br><br><br>* Range: 1000–25000.<br><br>* Default: 1000.<br><br><br>> **tip**<br><br><br>> This feature is currently in the invite\-only Beta stage. For trial requests, please contact your account manager.<br> |
|Long connection request max count ||No |Configure the maximum number of requests that a single HTTP/1.1 persistent connection can handle. After this limit is reached, the server will proactively close the connection.<br><br><br>* Value range: 100\-1000.<br><br>* Default value: 100.<br><br><br>> **tip**<br><br><br>> This feature is currently in the invite\-only Beta stage. For trial requests, please contact your account manager.<br> |
|HTTP/2 connection request max count ||No |Configure the maximum number of requests allowed per HTTP/2 connection. After the limit is reached, the server sends a GOAWAY frame to notify the client and closes the current connection.<br><br><br>* Value range: 300\-3000.<br><br>* Default value: 300.<br><br><br>> **tip**<br><br><br>> This feature is currently in the invite\-only Beta stage. For trial requests, please contact your account manager.<br> |
|Project ||No |Select a project for the custom configuration policy. [Project](https://docs.byteplus.com/docs/6649/189152) is a resource management method provided by BytePlus. Using projects, you can group and manage your cloud resources.<br><br>If no project is selected, the personalized configuration policy will be added to the **default** project by default. |
|Tag ||No |Set tags for custom configuration policy. [Tags](https://docs.byteplus.com/docs/6649/189377) are used to label resources, enabling you to categorize and aggregate resources for management. A tag consists of a tag key and a tag value.<br><br>You can directly select existing tags or enter a tag key and tag value. After entering a tag key or tag value, you need to click on it to confirm.<br><br>When setting tags, please note the following:<br><br><br>* The tag key and tag value can only contain Chinese characters, uppercase and lowercase English letters, numbers, spaces, and the special characters _.:/=+\-@.<br><br>* The tag key cannot start with `volc:` or `sys:`, nor any case variations of `volc:` and `sys:`.<br><br>* Tag keys and values are case\-sensitive.<br><br>* The tag key cannot be empty, while the tag value can be empty.<br><br>* A single custom configuration policy can be bound to a maximum of 50 tags. You can add up to 20 tags at a time.<br><br>* When multiple tags are bound to a single custom configuration policy, the tag keys must be unique.<br><br><br>For more information on how to use tags to manage ALB resources, see [Managing ALB resources with tags](https://docs.byteplus.com/docs/clb/Using-tags-to-manage-ALB-resources). |

> **tip**

* > ALB supports gzip compression by default. No manual activation is required.

   * > If a client request includes the header `Accept-Encoding: gzip`, ALB will perform gzip compression on the backend response content. If the request does not contain `Accept-Encoding: gzip`, ALB will not compress the response.

   * > Supported compressed content types: `text/plain`, `text/css`, `text/xml`, `application/xml`, `text/javascript`, `application/x-javascript`, `application/json`, `application/javascript`, `application/x-protobuf`, `application/octet-stream; ssmix=a`.

* > Scenarios where ALB compression does not take effect.

   * > If the response returned by the backend server is already compressed, ALB will not perform secondary compression.

   * > ALB only compresses response content when its size exceeds 200B. The compression feature will not take effect for response content of 200B or less.

   * > ALB does not currently support brotli compression. If a client request includes `Accept-Encoding: br`, ALB will not compress the backend response content.

* > Compression alters the MD5 hash of the content. If the backend server has an MD5 verification mechanism configured and the client needs to verify the MD5 value of the original response, ensure that the client request header does not contain `Accept-Encoding: gzip` to avoid MD5 verification failure.

### **Protocol and cipher suites**

|Selected protocol |Cipher suite |
|---|---|
|TLSv1 |ECDHE\-ECDSA\-AES128\-SHA<br><br>ECDHE\-ECDSA\-AES256\-SHA<br><br>ECDHE\-RSA\-AES128\-SHA<br><br>ECDHE\-RSA\-AES256\-SHA<br><br>AES128\-SHA<br><br>AES256\-SHA<br><br>DES\-CBC3\-SHA |
|TLSv1.1 ||
|TLSv1.2 |ECDHE\-ECDSA\-AES128\-SHA<br><br>ECDHE\-ECDSA\-AES256\-SHA<br><br>ECDHE\-RSA\-AES128\-SHA<br><br>ECDHE\-RSA\-AES256\-SHA<br><br>AES128\-SHA<br><br>AES256\-SHA<br><br>DES\-CBC3\-SHA<br><br>ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>ECDHE\-ECDSA\-AES128\-SHA256<br><br>ECDHE\-ECDSA\-AES256\-SHA384<br><br>ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>ECDHE\-RSA\-AES128\-SHA256<br><br>ECDHE\-RSA\-AES256\-SHA384<br><br>ECDHE\-RSA\-CHACHA20\-POLY1305<br><br>ECDHE\-ECDSA\-CHACHA20\-POLY1305<br><br>AES128\-GCM\-SHA256<br><br>AES256\-GCM\-SHA384<br><br>AES128\-SHA256<br><br>AES256\-SHA256 |
|TLS1.3 |TLS_AES_128_CCM_SHA256<br><br>TLS_AES_128_CCM_8_SHA256<br><br>TLS_AES_128_GCM_SHA256<br><br>TLS_AES_256_GCM_SHA384<br><br>TLS_CHACHA20_POLY1305_SHA256 |
|Leave blank |Default cipher suites: ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5 |

## Associate a custom policy

After creating a custom policy, you must associate it with a specific listener and enable the feature so that the listener adheres to the configuration policy.

### Procedure

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. Click the target listener name.

5. In the Custom configuration module, then click **Edit** icon to the right of **Custom configuration**.

6. Enable the custom configuration status, select **Custom configuration policy**, then click **Save** to complete the action.

> **tip**

* > The TLS version and cipher suite configurations within the custom settings only take effect for HTTPS listeners.

* > If a listener's custom configuration is disabled, you must re\-select the custom configuration policy when re\-enabling it.

* > A maximum of 200 policy groups can be created per region, and each policy group can be associated with up to 50 listeners.
