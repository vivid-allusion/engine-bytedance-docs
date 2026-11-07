---
title: "Use TLS SDK for Go to import Kafka data"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use-tls-sdk-for-go-to-import-kafka-data"
---

Torch Log Service (TLS) supports importing Kafka data by using SDK. This topic demonstrates through sample code how to import data from Kafka to TLS using the Go SDK.

<span id="d8afc8a3"></span>
## Before you begin


* Install TLS SDK for Go. For more information, refer to [Install TLS SDK for Go](https://docs.byteplus.com/docs/tls/install_tls_for_go).

* Run the following command to install the proto dependency:

   ```Shell
   go get -u github.com/gogo/protobuf/proto
   ```
   

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="33b25f6b"></span>
## Configuration description

This topic demonstrates how to create a Kafka data import task in a specific project using the GO SDK through sample code. For relevant feature introductions, precautions and fee descriptions, please refer to [Import data from Kafka](https://docs.byteplus.com/docs/tls/import_data_from_kafka).

<span id="6a6127ff"></span>
## Sample code

```Plain
package demo

import (
    "github.com/volcengine/volc-sdk-golang/service/tls"
    "os"
)

func CreateImportKafkaTaskDemo() (*tls.CreateImportTaskResponse, error) {
    // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
    // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
    client := tls.NewClient(os.Getenv("VOLCENGINE_ENDPOINT"), os.Getenv("VOLCENGINE_ACCESS_KEY_ID"), os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET"), os.Getenv("VOLCENGINE_TOKEN"), os.Getenv("VOLCENGINE_REGION"))
    // Create a data import task.
    createImportTaskResp, err := client.CreateImportTask(&tls.CreateImportTaskRequest{
       TopicID:     "fa**",
       TaskName:    "task-name-1",
       SourceType:  "kafka",
       Description: "this is a task",
       ImportSourceInfo: &tls.ImportSourceInfo{
          KafkaSourceInfo: &tls.KafkaSourceInfo{
             Host:              "kafka-cnngc7an0qpv****.kafka.ibytepluses.com:9092",
             Group:             "mygroup",
             Topic:             "test",
             Encode:            "UTF-8",
             Password:          "",
             Protocol:          "",
             Username:          "",
             Mechanism:         "",
             InstanceID:        "",
             IsNeedAuth:        "false",
             InitialOffset:     0,
             TimeSourceDefault: 0,
          },
       },
       TargetInfo: &tls.TargetInfo{
          Region:  "cn-shanghai",
          LogType: "json_log",
          ExtractRule: &tls.ImportExtractRule{
             TimeZone:         "GMT",
             SkipLineCount:    0,
             TimeExtractRegex: "",
             ExtractRule: &tls.ExtractRule{
                Quote: "\"",
             },
          },
       },
    })

    if err != nil {
       return nil, err
    }

    return createImportTaskResp, nil
}
```


<span id="99aa9f1e"></span>
## Related documents


* After you use the SDK to send an API request, the server returns a response. If the response contains a non\-200 status code, the API call fails. To view the error code and error message, refer to API reference.

* The following table describes the API actions involved in the preceding sample code. To view the details of each API action, refer to API reference.

   
   |API |explain |
   |---|---|
   |[CreateImportTask](https://docs.byteplus.com/en/docs/tls/CreateImportTask) |Create a data import task. |
   |[DeleteImportTask](https://docs.byteplus.com/en/docs/tls/DeleteImportTask) |Delete the specified data import task. |
   |[ModifyImportTask](https://docs.byteplus.com/en/docs/tls/ModifyImportTask) |Modify the specified data import task. |
   |[DescribeImportTask](https://docs.byteplus.com/en/docs/tls/DescribeImportTask) |View information about a specific data import task. |
   |[DescribeImportTasks](https://docs.byteplus.com/en/docs/tls/DescribeImportTasks) |View the list of data import tasks. |
