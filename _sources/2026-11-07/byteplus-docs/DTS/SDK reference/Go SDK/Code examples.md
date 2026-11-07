---
title: "Code examples"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Code_examples"
---

This topic provides code examples of the DTS Go SDK for your reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data transmission task described in this topic can include migration task, synchronization task, and data subscription task.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Download and install the SDK.](https://docs.byteplus.com/en/docs/DTS/Downloading_and_installing_the_SDK)

2. [Initialization client.](https://docs.byteplus.com/en/docs/DTS/Initializing_client)


<span id=".6K6-572u6K-35rGC6LaF5pe25pe26Ze0"></span>
## Set the request timeout period

When you use the Go SDK to call the DTS interface, there is no timeout period set by default.  When initializing the client, you can specify the request timed out time of the client by `WithHTTPClient (& http. Client {Timeout: ${Timeout} * time. Second})`. If the request is not completed within this time, the request will be terminated with a timeout error. For example, you can use the following code to set the client's request timeout to 10 seconds.

```go
config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
   WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu65pWw5o2u6K6i6ZiF5Lu75Yqh"></span>
## Create a data subscription task

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()

    // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    instance.SetCredential(base.Credentials{
       AccessKeyID:     os.Getenv("AK"),
       SecretAccessKey: os.Getenv("SK"),
    })

    times := int32(1)
    // 付费方式
    chargeType := dts_v20221001.CreateTransmissionTaskBodyChargeConfigChargeType("PostPaid")
    chargeConfig := &dts_v20221001.CreateTransmissionTaskBodyChargeConfig{
       ChargeType: &chargeType,
       Times:      &times,
    }

    // 订阅中间件
    endpointType := dts_v20221001.CreateTransmissionTaskBodyDestConfigEndpointType("Builtin_Kafka")

    // 中间件配置
    builtinKafkaSettings := &dts_v20221001.CreateTransmissionTaskBodyDestConfigBuiltinKafkaSettings{}
    destConfig := &dts_v20221001.CreateTransmissionTaskBodyDestConfig{
       EndpointType:         &endpointType,
       BuiltinKafkaSettings: builtinKafkaSettings,
    }

    // 项目名称
    projectName := "default"
    solutionType := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsSolutionType("MySQL2Kafka")

    // 最大重试时间
    maxRetrySeconds := int32(7200)
    errorBehaviorSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsErrorBehaviorSettings{
       MaxRetrySeconds: &maxRetrySeconds,
    }

    // 订阅类型-全量订阅的配置
    enableFull := false
    fullTransmissionSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsFullTransmissionSettings{
       EnableFull: &enableFull,
    }

    enableIncr := true

    //订阅类型-增量订阅的配置
    statments_1 := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsIncrTransmissionSettingsStatementsItem("StmtDMLUpdate")
    statements := []*dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsIncrTransmissionSettingsStatementsItem{&statments_1}
    incrTransmissionSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsIncrTransmissionSettings{
       EnableIncr: &enableIncr,
       Statements: statements,
    }

    // 订阅类型-结构订阅的配置
    enableMeta := false
    metaTransmissionSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsMetaTransmissionSettings{
       EnableMeta: &enableMeta,
    }

    // 订阅起始点
    mySQLPosition := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsMySQLPosition{}

    destObjName_1 := "d1"

    mappingList_1_destObjName_1 := "*"

    setObjectTransType := true
    meta := dts_v20221001.ObjectMapping20221001ObjectMappingSettingObjectTransTypesItem("Meta")
    incr := dts_v20221001.ObjectMapping20221001ObjectMappingSettingObjectTransTypesItem("Incr")
    objectTransTypes := []*dts_v20221001.ObjectMapping20221001ObjectMappingSettingObjectTransTypesItem{&meta, &incr}
    mappingList_1_objectMappingSetting_1 := dts_v20221001.ObjectMapping20221001ObjectMappingSetting{
       SetObjectTransType: &setObjectTransType,
       ObjectTransTypes:   objectTransTypes,
    }

    objectType := dts_v20221001.ObjectMapping20221001ObjectType("Table")
    srcObjName := "*"
    mappingList_1 := dts_v20221001.ObjectMapping20221001{
       DestObjName:          &mappingList_1_destObjName_1,
       ObjectMappingSetting: &mappingList_1_objectMappingSetting_1,
       ObjectType:           &objectType,
       SrcObjName:           &srcObjName,
    }
    mappingList := []*dts_v20221001.ObjectMapping20221001{
       &mappingList_1,
    }

    meta_sub := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsPropertiesItemsItem("Meta")
    incr_sub := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsPropertiesItemsItem("Incr")
    objectTransTypes_sub := []*dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsPropertiesItemsItem{&meta_sub, &incr_sub}

    setObjectTransType_sub := true
    objectMappingSetting := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsItemObjectMappingSetting{
       ObjectTransTypes:   objectTransTypes_sub,
       SetObjectTransType: &setObjectTransType_sub,
    }

    objectType_sub := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsItemObjectType("Database")

    srcObjName_sub := "d1"

    objectMappings_1 := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsItem{
       DestObjName:          &destObjName_1,
       MappingList:          mappingList,
       ObjectMappingSetting: &objectMappingSetting,
       ObjectType:           &objectType_sub,
       SrcObjName:           &srcObjName_sub,
    }

    // 订阅对象
    objectMappings := []*dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsObjectMappingsItem{
       &objectMappings_1,
    }

    // 订阅格式
    protocol := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsSubscriptionSettingsProtocol("Volc")
    // 私有网络
    vpcId := "vpcId"
    // 子网
    vpcSubnetId := "vpcSubnetId"
    // 订阅配置
    subscriptionSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettingsSubscriptionSettings{
       Protocol:    &protocol,
       VPCID:       &vpcId,
       VPCSubnetID: &vpcSubnetId,
    }

    // mysql2kafka 配置
    mySQL2KafkaSettings := dts_v20221001.CreateTransmissionTaskBodySolutionSettingsMySQL2KafkaSettings{
       ErrorBehaviorSettings:    &errorBehaviorSettings,
       FullTransmissionSettings: &fullTransmissionSettings,
       IncrTransmissionSettings: &incrTransmissionSettings,
       MetaTransmissionSettings: &metaTransmissionSettings,
       MySQLPosition:            &mySQLPosition,
       ObjectMappings:           objectMappings,
       SubscriptionSettings:     &subscriptionSettings,
    }

    // 订阅对象配置
    solutionSettings := &dts_v20221001.CreateTransmissionTaskBodySolutionSettings{
       SolutionType:        &solutionType,
       MySQL2KafkaSettings: &mySQL2KafkaSettings,
    }

    srcEndpointType := dts_v20221001.CreateTransmissionTaskBodySrcConfigEndpointType("Volc_MySQL")

    // 源端实例 id
    dbInstanceId := "dbInstanceId"
    // 数据库账号
    password := "password"
    // 账号密码
    userName := "userName"

    region := "cn-beijing"
    // 源端 region 配置
    regionSettings := dts_v20221001.CreateTransmissionTaskBodySrcConfigVolcMySQLSettingsRegionSettings{
       Region: &region,
    }

    // 源端 mysql 配置
    volcMySQLSettings := dts_v20221001.CreateTransmissionTaskBodySrcConfigVolcMySQLSettings{
       DBInstanceID:   &dbInstanceId,
       Password:       &password,
       Username:       &userName,
       RegionSettings: &regionSettings,
    }

    // 源端配置
    srcConfig := dts_v20221001.CreateTransmissionTaskBodySrcConfig{
       EndpointType:      &srcEndpointType,
       VolcMySQLSettings: &volcMySQLSettings,
    }

    // 标签
    tags := []*dts_v20221001.CreateTransmissionTaskBodyTagsItem{}
    // 任务名称
    taskName := "taskName"
    // 任务类型
    taskType := dts_v20221001.CreateTransmissionTaskBodyTaskType("DataSubscription")
    // 规格
    trafficSpec := dts_v20221001.CreateTransmissionTaskBodyTrafficSpec("Standard")
    param := &dts_v20221001.CreateTransmissionTaskBody{
       ChargeConfig:     chargeConfig,
       DestConfig:       destConfig,
       ProjectName:      &projectName,
       SolutionSettings: solutionSettings,
       SrcConfig:        &srcConfig,
       Tags:             tags,
       TaskName:         &taskName,
       TaskType:         &taskType,
       TrafficSpec:      &trafficSpec,
    }

    resp, err := instance.CreateTransmissionTask(context.Background(), param)

    if err != nil {
       fmt.Printf("error %v", err)
    } else {
       fmt.Printf("success %v", resp)
    }
}
```


<span id=".5p-l6K-i5pWw5o2u5Lyg6L6T5Lu75Yqh5L-h5oGv"></span>
## **Query data transmission task information**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.DescribeTransmissionTaskInfoBody{TaskID: &taskID}

    resp, err := instance.DescribeTransmissionTaskInfo(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5om56YeP5p-l6K-i5pWw5o2u5Lyg6L6T5Lu75Yqh5L-h5oGv"></span>
## Batch **query data transmission task information**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    taskType := "DataSubscription"
    param := &dts_v20221001.DescribeTransmissionTasksBody{TaskType:(*dts_v20221001.DescribeTransmissionTasksBodyTaskType)(&taskType)}

    resp, err := instance.DescribeTransmissionTasks(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5pqC5YGc5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Pause data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.SuspendTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.SuspendTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5om56YeP5pqC5YGc5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## Batch **pause data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    ID1 := ""
    ID2 := ""

    taskIDs := []*string{&ID1, &ID2}
    param := &dts_v20221001.SuspendTransmissionTasksBody{TaskIDs: taskIDs}

    resp, err := instance.SuspendTransmissionTasks(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5ZCv5Yqo5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Start data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.StartTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.StartTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5om56YeP5ZCv5Yqo5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## Batch **start data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    ID1 := "ID1"
    ID2 := "ID2"

    taskIDs := []*string{&ID_1, &ID_2}
    param := &dts_v20221001.StartTransmissionTasksBody{TaskIDs: taskIDs}

    resp, err := instance.StartTransmissionTasks(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".6YeN6K-V5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Retry data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.RetryTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.RetryTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5om56YeP6YeN6K-V5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## Batch **retry data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    ID1 := ""
    ID2 := ""
    taskIDs := []*string{&ID1, &ID2}
    param := &dts_v20221001.RetryTransmissionTasksBody{TaskIDs: taskIDs}

    resp, err := instance.RetryTransmissionTasks(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5oGi5aSN5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Recover data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.ResumeTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.ResumeTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".57uI5q2i5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Terminate data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.StopTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.StopTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5Yig6Zmk5pWw5o2u5Lyg6L6T5Lu75Yqh"></span>
## **Delete data transmission task**

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20221001"
)

func main() {

    instance := dts_v20221001.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    // 任务 ID
    taskID := "taskID"
    param := &dts_v20221001.DeleteTransmissionTaskBody{TaskID: &taskID}

    resp, err := instance.DeleteTransmissionTask(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5Yib5bu66aKE5qOA5p-l5Lu75Yqh"></span>
## Create pre\-check task

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20180101"
)

func main() {

    instance := dts_v20180101.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    param := &dts_v20180101.PreCheckAsyncBody{
        TaskID: "TaskID",
    }

    resp, err := instance.PreCheckAsync(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```


<span id=".5p-l6K-i6aKE5qOA5p-l57uT5p6c"></span>
## Query pre\-check results

```go
package main

import (
    "context"
    "fmt"
    "os"
    "github.com/volcengine/volc-sdk-golang/base"
    "github.com/volcengine/volc-sdk-golang/service/dts/v20180101"
)

func main() {

    instance := dts_v20180101.NewInstance()
    
     // 强烈建议不要把 AccessKey ID 和 AccessKey Secret 保存到工程代码里，否则可能导致 AccessKey 泄露，威胁您账号下所有资源的安全。
    // 本示例通过从环境变量中读取 AccessKey ID 和 AccessKey Secret，来实现 API 访问的身份验证。运行代码示例前，请配置环境变量 ACCESS_KEY_ID 和 ACCESS KEY_SECRET
    
    instance.SetCredential(base.Credentials{
        AccessKeyID:     os.Getenv("AK"),
        SecretAccessKey: os.Getenv("SK"),
    })
    
    param := &dts_v20180101.GetAsyncPreCheckResultBody{
        // 预检查的 ID
        ID: "ID",
    }

    resp, err := instance.GetAsyncPreCheckResult(context.Background(), param)
    
    if err != nil {
        fmt.Printf("error %v", err)
    } else {
        fmt.Printf("success %v", string(resp))
    }
}
```
