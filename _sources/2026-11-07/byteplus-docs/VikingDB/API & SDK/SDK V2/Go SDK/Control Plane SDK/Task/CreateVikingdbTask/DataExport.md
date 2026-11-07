---
title: "DataExport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DataExport"
---

<span id="overview"></span>
# Overview

Batch export data from Collection based on specific conditions.

Before using, please authorize VikingDB for cross\-service access to TOS [Authorize Now](https://console.volcengine.com/iam/service/attach_role/?ServiceName=ml_platform)

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `CreateVikingdbTask(input)` method to initiate a task creation request. The input parameter type is `vikingdb.CreateVikingdbTaskInput`, which contains the complete configuration information required for task creation.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |string |No |Project name |
|CollectionName | |string |One of two required |Collection name |
|ResourceId | |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|TaskType | |string |Yes |data_export |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |FileType |string |Yes |File type, json or parquet, required |
| |FilterConds |[]interface{} |No |Filter conditions. Reference: https://www.volcengine.com/docs/84313/1791133<br><br><br>* If FilterConds is not filled, it is irrelevant to ExportAll, and all data is exported by default.<br><br>* If FilterConds is filled:<br><br>* If ExportAll is not specified or ExportAll=false, data that meets the conditions is exported by default.<br><br>* If ExportAll=true is specified, all data is forcibly exported, and FilterConds does not take effect at this time. |
| |TosPath |string |Yes |TOS path, format: {bucket name}/{path}, note that this is not a domain name. Required |
| |ExportAll |bool |No |Whether to export all data, FilterConds does not take effect at this time. Default is false |
| |OutputFields |string |No |Configure the list of exported fields. All fields are exported by default. |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Type |Description |
|---|---|---|
|TaskId |string |Task ID |
|Message |string |Operation result information |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )

    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    // Create export task
    input := &vikingdb.CreateVikingdbTaskInput{
       TaskType: volcengine.String(vikingdb.EnumOfTaskTypeForCreateVikingdbTaskInputDataExport),
       TaskConfig: &vikingdb.TaskConfigForCreateVikingdbTaskInput{
          ExportAll: volcengine.Bool(true),
          FileType:  volcengine.String(vikingdb.EnumOfFileTypeForCreateVikingdbTaskInputJson),
          TosPath:   volcengine.String("your-tos-bucket-name/path/"),
       },
       CollectionName: volcengine.String("Your-Collection-Name"),
       ProjectName:    volcengine.String("default"),
    }

    resp, err := svc.CreateVikingdbTask(input)
    if err != nil {
       panic(err)
    }

    fmt.Println(*resp.TaskId)
}
```


<span id="post-processing"></span>
## Post\-processing

<span id="_1-download-file-from-tos"></span>
### 1. Download file from TOS

```Go
package main

import (
    "context"
    "fmt"
    "os"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
    var (
       endpoint  = "https://tos-cn-beijing.volces.com"
       region    = "ap-southeast-1"
       accessKey = os.Getenv("TOS_ACCESS_KEY")
       secretKey = os.Getenv("TOS_SECRET_KEY")
       bucket    = "liningrui-test"
       objectKey = "path/0.parquet"
       localPath = "data.parquet"
    )

    // Initialize TOS client
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    if err != nil {
       fmt.Printf("Init client failed, err: %v\n", err)
       return
    }

    // Download object
    _, err = client.GetObjectToFile(context.Background(), &tos.GetObjectToFileInput{
       GetObjectV2Input: tos.GetObjectV2Input{
          Bucket: bucket,
          Key:    objectKey,
       },
       FilePath: localPath,
    })
    if err != nil {
       fmt.Printf("Get object failed, err: %v\n", err)
       return
    }

    fmt.Printf("Download success, object %s saved to %s\n", objectKey, localPath)
}
```


<span id="_2-parse-parquet-type-data"></span>
### 2. Parse parquet type data

```Go
package main

import (
    "fmt"
    "log"

    "github.com/xitongsys/parquet-go-source/local"
    "github.com/xitongsys/parquet-go/reader"
)

// DemoStruct defines the schema of the parquet file
// You should modify this struct according to your parquet file schema
type DemoStruct struct {
    Name string `parquet:"name=name, type=BYTE_ARRAY, convertedtype=UTF8"`
    Id   int64  `parquet:"name=id, type=INT64"`
}

func main() {
    filePath := "data.parquet" // Replace with your parquet file path

    // 1. Open local file
    fr, err := local.NewLocalFileReader(filePath)
    if err != nil {
       log.Printf("Can't open file: %v", err)
       return
    }
    defer fr.Close()

    // 2. Create parquet reader
    // The second argument is an instance of the struct that matches the parquet schema
    pr, err := reader.NewParquetReader(fr, new(DemoStruct), 4)
    if err != nil {
       log.Printf("Can't create parquet reader: %v", err)
       return
    }
    defer pr.ReadStop()

    // 3. Get total number of rows
    num := int(pr.GetNumRows())
    fmt.Printf("Total rows: %d\n", num)

    // 4. Read and print rows
    // We read in batches for efficiency
    batchSize := 10
    for i := 0; i < num; i += batchSize {
       readNum := batchSize
       if i+batchSize > num {
          readNum = num - i
       }

       data := make([]DemoStruct, readNum)
       if err = pr.Read(&data); err != nil {
          log.Printf("Read error: %v", err)
          break
       }

       for _, item := range data {
          fmt.Printf("Row: %+v\n", item)
       }
    }
}
```
