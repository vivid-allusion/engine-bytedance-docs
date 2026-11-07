---
title: "Code examples"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Code_examples_go"
---

This article introduces code examples of NDB for MySQL Go SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The [Downloading and installing SDK](https://www.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_go) has been completed.

* The [Initializing client](https://www.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_go) has been completed.


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Request timed out time settings

There is no timeout setting by default when calling the interface with the Go SDK. When initializing the client, you can use `WithHTTPClient(&http.Client{Timeout: <Timeout> * time.Second})` to specify the client's request timeout. If the request is not completed within this time, the request will be terminated immediately and a timeout error will be reported. For example, you can set the client's request timed out to 10 seconds with the following code.

```go
config = byteplus.NewConfig().
   WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
   WithRegion(region).
   WithEndpoint("service host").
   WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu6LXZlZGItbXlzcWwt5a6e5L6L"></span>
## Creating an instance

For a detailed description of the parameters in the following example, see [CreateDBInstance](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance#请求参数).

```go
func StringPtr(s string) *string {
    return &s
}

func Int32Ptr(i int32) *int32 {
    return &i
}

func CreateDBInstance() {
    InitClient()

    var (
       resp *CreateDBInstanceOutput
       err  error
    )

    resp, err = VeDBMClient.CreateDBInstance(&CreateDBInstanceInput{
       ChargeType:           StringPtr("PostPaid"),
       DBEngineVersion:      StringPtr("MySQL_8_0"),
       DBTimeZone:           StringPtr("UTC +08:00"),
       InstanceName:         StringPtr("your instance name"),
       LowerCaseTableNames:  StringPtr("0"),
       NodeNumber:           Int32Ptr(2),
       NodeSpec:             StringPtr("vedb.mysql.x4.large"),
       ProjectName:          nil,
       SubnetId:             StringPtr("your subnet id"),
       SuperAccountName:     StringPtr("your super account name"),
       SuperAccountPassword: StringPtr("your super account password"),
       Tags:                 nil,
       VpcId:                StringPtr("your vpc id"),
       ZoneIds:              StringPtr("cn-beijing-b"),
    })

    if nil != err {
       t.Errorf("%s", err.Error())
    }

    var respStr []byte
    respStr, err = json.MarshalIndent(resp, "", "\t")
    fmt.Printf("%s", string(respStr))
}
```


<span id=".5p-l6K-iLXZlZGItbXlzcWwt5a6e5L6L5L-h5oGv"></span>
## Query instance information

```go
func DescribeDBInstanceDetail() {
    InitClient()

    var (
       resp *DescribeDBInstanceDetailOutput
       err  error
    )

    resp, err = VeDBMClient.DescribeDBInstanceDetail(&DescribeDBInstanceDetailInput{
       InstanceId: StringPtr("your instance id"),
    })

    if nil != err {
       t.Errorf("%s", err.Error())
    }

    var respStr []byte
    respStr, err = json.MarshalIndent(resp, "", "\t")
    fmt.Printf("%s", string(respStr))
}
```
