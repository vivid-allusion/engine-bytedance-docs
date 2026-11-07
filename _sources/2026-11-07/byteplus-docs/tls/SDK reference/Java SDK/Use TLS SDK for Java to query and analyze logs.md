---
title: "Use TLS SDK for Java to query and analyze logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_to_query_and_analyze_logs"
---

Torch Log Service (TLS) allows you to use an SDK to query log data collected to the server. This topic offers sample code that demonstrates how to use TLS SDK for Java to query and analyze logs.

<span id="9bcdb574"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

* Collect log data and configure indexes. To configure indexes in the console, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes). Alternatively, use CreateIndex to configure indexes. To get the sample code, refer to [Use TLS SDK for Java to create basic resources](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_to_create_basic_resources).


<span id="fc7bf10b"></span>
## Consuming logs

<span id="8816cb1c"></span>
### Scenario description

You can use the SDK to call the SearchLogs API action to query and analyze log data. For information on the limits of the query and analysis feature, refer to [Query and analysis limits](/docs/tls/Limits#Query and analysis limits). For information on the syntax of query and analysis statements, refer to [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [Analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview). The following sample code returns all log data as an example to demonstrate how to use the SDK to query and analyze log data.

<span id="946c11e8"></span>
### Sample code

```Java
package com.volcengine.example.tls.demo;

import com.volcengine.model.tls.*;
import com.volcengine.model.tls.exception.LogException;
import com.volcengine.model.tls.request.*;
import com.volcengine.model.tls.response.*;
import com.volcengine.service.tls.TLSLogClient;

import java.util.ArrayList;
import java.util.List;


public class Demo {
    public static void main(String[] args) throws LogException {
        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks. 
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
        ClientConfig clientConfig = new ClientConfig(System.getenv("VOLCENGINE_ENDPOINT"), System.getenv("VOLCENGINE_REGION"),
            System.getenv("VOLCENGINE_ACCESS_KEY_ID"), System.getenv("VOLCENGINE_ACCESS_KEY_SECRET"), System.getenv("VOLCENGINE_TOKEN"));
        TLSLogClient client = ClientBuilder.newClient(clientConfig);

        // Query and analyze log data.
        // Specify parameters such as TopicId, Query, StartTime, EndTime, and Limit as needed.        
        SearchLogsRequest searchLogsRequest = new SearchLogsRequest();
        searchLogsRequest.setTopicId("your-topic-id");
        searchLogsRequest.setQuery("*");
        searchLogsRequest.setStartTime(1346457600);
        searchLogsRequest.setEndTime(1630454400);
        searchLogsRequest.setLimit(20);
        SearchLogsResponseV2 searchLogsResponse = client.searchLogsV2(searchLogsRequest);

        // Print some basic information in the return value of the SearchLogs API action.
        // Handle other information in the return value as needed.
        System.out.println(searchLogsResponse.getResultStatus());
        System.out.println(searchLogsResponse.getHitCount());
        System.out.println(searchLogsResponse.getCount());
        System.out.println(searchLogsResponse.isAnalysis());
    }
}
```


<span id="1933c34b"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |Description |
   |---|---|
   |[SearchLogs](https://docs.byteplus.com/en/docs/tls/api-searchlogs) |Queries logs. |
   

* To get the complete sample code of TLS queries and analysis, refer to [TLS Java SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/LogsDemo.java).
