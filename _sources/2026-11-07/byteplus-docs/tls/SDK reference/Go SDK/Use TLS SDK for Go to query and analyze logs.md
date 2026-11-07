---
title: "Use TLS SDK for Go to query and analyze logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_tls_for_go_to_query_and_analyze_logs"
---

Torch Log Service (TLS) allows you to use an SDK to query log data collected to the server. This topic offers sample code that demonstrates how to use TLS SDK for Go to query and analyze logs.

<span id="e8e08536"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

* Collect log data and configure indexes. To configure indexes in the console, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes). Alternatively, use [CreateIndex](https://docs.byteplus.com/docs/tls/api-createindex) API to configure indexes. To get the sample code, refer to [Use TLS SDK for Go to create basic resources](https://docs.byteplus.com/docs/tls/use_tls_for_go_to_create_basic_resources).


<span id="0493c7f0"></span>
## Consuming logs

<span id="9b8e7863"></span>
### Scenario description

You can use the SDK to call the SearchLogs API action to query and analyze log data. For information on the limits of the query and analysis feature, refer to [Query and analysis limits](/docs/tls/Limits#Query and analysis limits). For information on the syntax of query and analysis statements, refer to [Log query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) and [Analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview). The following sample code returns all log data as an example to demonstrate how to use the SDK to query and analyze log data.

<span id="4e26199c"></span>
### Sample code

```Go
package tls

import (
    "fmt"
    "github.com/volcengine/volc-sdk-golang/service/tls"
)

func main() {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    client := tls.NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"),
        os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))

    // Query and analyze log data.
    // Specify parameters such as TopicId, Query, StartTime, EndTime, and Limit as needed.
    resp, err := client.SearchLogsV2(&tls.SearchLogsRequest{
       TopicID:   "TopicId",
       Query:     "*",
       StartTime: 1346457600000,
       EndTime:   1630454400000,
       Limit:     20,
    })
    if err != nil {
       // Handle an error.
       fmt.Println(err.Error())
    }

    // Print some basic information in the return value of the SearchLogs API action.
    // Handle other information in the return value as needed.
    fmt.Println(resp.Status)
    fmt.Println(resp.HitCount)
    fmt.Println(resp.Count)
    fmt.Println(resp.Analysis)
}
```


<span id="7309d891"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |Description |
   |---|---|
   |[SearchLogs](https://docs.byteplus.com/en/docs/tls/api-searchlogs) |Call the SearchLogs interface to query logs. |
   

* To get the complete sample code of TLS queries and analysis, refer to [TLS Go SDK Demo on GitHub](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_log.go).
