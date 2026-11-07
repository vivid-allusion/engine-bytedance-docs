---
title: "Using Go SDK"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/use_go_sdk"
---

This topic describes the download, installation, and client initialization related information of the Go SDK for RDS for PostgreSQL.

<span id=".5LiL6L295LiO5a6J6KOF"></span>
## Download and install

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Go 1.5 or above is required, and Go 1.12 or above is recommended.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can check the current Go version information by executing the <code>go version</code> command.</div>


<span id=".U0RLIOS4i-i9veWcsOWdgA=="></span>
### SDK download URL

The source code address of the Go SDK for RDS for PostgreSQL, see [SDK list](https://docs.byteplus.com/en/docs/RDS_for_PG/sdk_overview).

<span id=".5a6J6KOFIFNESw=="></span>
### **Install SDK**

Execute the following command under the target Go project to install the Go SDK.

```go
go get github.com/volcengine/volcengine-go-sdk/volcengine/credentials
go get github.com/volcengine/volcengine-go-sdk/volcengine/volcengineutil
```


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initialize client

The RDS for PostgreSQL Go SDK supports initializing clients through Session. The PostgreSQL client created through Session implements reuse of HTTP/HTTPS resources (connections or requests) at the underlying level. When multiple clients need to be initialized for operations, creating them via Session can improve client performance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. For specific operations, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* The supported Regions and corresponding Hosts of RDS for PostgreSQL have been obtained. Please refer to [service address](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A).

* The RDS for PostgreSQL Go SDK has been downloaded and installed. For specific steps, see [Download and Install](https://docs.byteplus.com/en/docs/RDS_for_PG/use_go_sdk#.5LiL6L295LiO5a6J6KOF).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
### Initialize client

Initialize the client with the following code.

```go
package rdspostgresql
import (
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
    "github.com/volcengine/volcengine-go-sdk/service/rdspostgresql"
)
var (
    Config *volcengine.Config
    Sess   *session.Session
    Client *rdspostgresql.RDSPOSTGRESQL
)
const (
    AK       = "Your AK"
    SK       = "Your SK"
    REGION   = "Your Region"
    ENDPOINT = "Your Host"
)
func InitConfig() {
    Config = volcengine.NewConfig().
       WithCredentials(credentials.NewStaticCredentials(AK, SK, "")).
       WithRegion(REGION).WithEndpoint(ENDPOINT)
    Sess, _ = session.NewSession(Config)
    Client = rdspostgresql.New(Sess)
}
```


<span id=".5Luj56CB56S65L6L"></span>
## Sample

<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
### Request timed out time settings

When using the Go SDK to call the PostgreSQL interface, there is no timeout set by default. You can specify the client's request timeout when initializing the client by using `WithHTTPClient(&http.Client{Timeout: <timeout> * time.Second})`. If the request is not completed within this time, it will be immediately terminated and report a timeout error. For example, you can set the client's request timeout to 10 seconds with the following code.

```go
config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu6IFBvc3RncmVTUUwg5a6e5L6L"></span>
### Creating PostgreSQL instance

For the definitions, value ranges, and other information of the parameters used in the following SDK code, please refer to [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance).

```go
package rdspostgresql
import (
    "fmt"
    "github.com/volcengine/volcengine-go-sdk/service/rdspostgresql"
    "testing"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
)
func TestRDSPostgreSQL_CreateDBInstanceCommon(t *testing.T) {
    InitConfig()
    resp, err := Client.CreateDBInstance(&rdspostgresql.CreateDBInstanceInput{
       DBEngineVersion: volcengine.String("PostgreSQL_12"),
       NodeInfo: []*rdspostgresql.NodeInfoForCreateDBInstanceInput{
          {
             NodeOperateType: volcengine.String("Create"),
             NodeSpec:        volcengine.String("rds.postgres.1c2g"),
             NodeType:        volcengine.String("Primary"),
             ZoneId:          volcengine.String("cn-beijing-c"),
          },
          {
             NodeOperateType: volcengine.String("Create"),
             NodeSpec:        volcengine.String("rds.postgres.1c2g"),
             NodeType:        volcengine.String("Secondary"),
             ZoneId:          volcengine.String("cn-beijing-c"),
          },
          {
             NodeOperateType: volcengine.String("Create"),
             NodeSpec:        volcengine.String("rds.postgres.1c2g"),
             NodeType:        volcengine.String("ReadOnly"),
             ZoneId:          volcengine.String("cn-beijing-c"),
          },
       },
       StorageSpace: volcengine.Int32(30),
       StorageType:  volcengine.String("LocalSSD"),
       VpcId:        volcengine.String("vpc-2bzo8w6m87v282dx0eemg****"),
       SubnetId:     volcengine.String("subnet-2d6b6byrhtts058ozfenq****"),
       ChargeInfo: &rdspostgresql.ChargeInfoForCreateDBInstanceInput{
          ChargeType: volcengine.String("PrePaid"),
          AutoRenew:  volcengine.Bool(false),
          PeriodUnit: volcengine.String("Month"),
          Period:     volcengine.Int32(2),
          Number:     volcengine.Int32(1),
       },
       InstanceName: volcengine.String("pg-test-sdk-go"),
       ProjectName:  volcengine.String("default"),
       Tags: []*rdspostgresql.TagForCreateDBInstanceInput{
          {
             Key:   volcengine.String("test1"),
             Value: volcengine.String("test1"),
          },
          {
             Key:   volcengine.String("test2"),
             Value: volcengine.String("test2"),
          },
       },
    })
    if err != nil {
       panic(err)
    }
    fmt.Println(resp)
}
```


The parameters in this example are described in the following table.


|Configuration item |Note |Value |
|---|---|---|
|DBEngineVersion |Compatible version. |PostgreSQL_12 |
|NodeInfo |Instance specification configuration. |[<br><br>{<br><br>"NodeType": "Primary",<br><br>"ZoneId": "cn\-beijing\-c",<br><br>"NodeSpec": "rds.postgres.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijing\-c",<br><br>"NodeSpec": "rds.postgres.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"ZoneId": "cn\-beijing\-c",<br><br>"NodeSpec": "rds.postgres.1c2g"<br><br>}<br><br>] |
|StorageType |Storage type. |LocalSSD |
|StorageSpace |Instance storage space. |30 |
|VpcId |A proprietary network (VPC) ID. |vpc\-2bzo8w6m87v282dx0eemg\*\*\*\* |
|SubnetId |Subnet ID. |subnet\-2d6b6byrhtts058ozfenq\*\*\*\* |
|InstanceName |Storage type. |pg\-test\-sdk\-go |
|ProjectName |Affiliated project of the instance. |default |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PrePaid",<br><br>"AutoRenew": false,<br><br>"PeriodUnit": "Month",<br><br>"Period":2,<br><br>"Number":1<br><br>} |
|InstanceTags |Instance tag. |[{<br><br>"Key": "test1",<br><br>"Value":"test1"<br><br>},{<br><br>"Key": "test2",<br><br>"Value":"test2"<br><br>}] |
|Number |Instance purchase quantity. |1 |


<span id=".5p-l6K-iIFBvc3RncmVTUUwg5a6e5L6L5L-h5oGv"></span>
### Query PostgreSQL instance information

For information about the definition, range, and other parameters used in the following SDK requests, see [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail).

```go
package rdspostgresql
import (
    "fmt"
    "github.com/volcengine/volcengine-go-sdk/service/rdspostgresql"
    "testing"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
)
func TestRDSPostgreSQL_DescribeDBInstanceDetailCommon(t *testing.T) {
    InitConfig()
    resp, err := Client.DescribeDBInstanceDetail(&rdspostgresql.DescribeDBInstanceDetailInput{
       InstanceId: volcengine.String("postgres-3acf1726****"),
    })
    if err != nil {
       panic(err)
    }
    fmt.Println(resp)
}
```
