---
title: "Code examples"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Go_SDK_code_example"
---

The code examples for the RDS for SQL Server Go SDK in this topic are for reference only.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have downloaded and installed the SDK. For more information, see [Download and installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_installation).

* You have initialized the client. For more information, see [Client initialization](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Go_SDK_Initialize_the_client).


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## **Set a request timeout**

By default, there is no timeout limit when you use the SDK to call SQL Server APIs. When you initialize the client, you can use `WithHTTPClient(&http.Client{Timeout: <超时时间> * time.Second})` to specify the request timeout. If a request does not complete within the specified period, it terminates and a timeout error is reported. For example, you can use the following code to set the client's request timeout to 10 seconds.

```go
config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu6LXNxbC1zZXJ2ZXIt5a6e5L6L"></span>
## **Create an SQL Server instance**

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance).

```Go
package  main
import (
   "fmt"
   "os"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/rdsmssql"
)

var (
   Config *byteplus.Config
   Sess   *session.Session
   Client *rdsmssql.RDSMSSQ
)
func main() {
    ak = "Your AK"
    sk = "Your SK"
    region = "Your Region"
    config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region)
    sess, err = session.NewSession(config)
    if err != nil {
       fmt.Printf("Failed to create session, err: %v\n", err)
       os.Exit(1)
    }
    Client = rdsmssql.New(sess)

    resp, err := Client.CreateDBInstance(&CreateDBInstanceInput{
       DBEngineVersion:      byteplus.String("SQLServer_2019_Std"),
       InstanceType:         byteplus.String("HA"),
       ZoneId:               byteplus.String("cn-beijing-a"),
       NodeSpec:             byteplus.String("rds.mssql.3il.s2.medium.s2"),
       StorageSpace:         byteplus.Int32(30),
       VpcId:                byteplus.String("vpc-*"),
       SubnetId:             byteplus.String("subnet-*"),
       SuperAccountPassword: byteplus.String("Test@123456"),
       DBTimeZone:           byteplus.String("China Standard Time"),
       ServerCollation:      byteplus.String("Chinese_PRC_CI_AS"),
       ChargeInfo: &ChargeInfoForCreateDBInstanceInput{
       ChargeType: byteplus.String("PostPaid"),
       AutoRenew:  byteplus.Bool(false),
       },
    })

    if err != nil {
        panic(err)
    }

    fmt.Println(resp)
}
```


<span id=".5p-l6K-iLXNxbC1zZXJ2ZXIt5a6e5L6L5L-h5oGv"></span>
## **Query SQL Server instance information**

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances)

```go
package  main
import (
   "fmt"
   "os"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/rdsmssql"
)

var (
   Config *byteplus.Config
   Sess   *session.Session
   Client rdsmssql.RDSMSSQL
)
func main() {
    ak = "Your AK"
    sk = "Your SK"
    region = "Your Region"
    config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region)
    sess, err = session.NewSession(config)
    if err != nil {
       fmt.Printf("Failed to create session, err: %v\n", err)
       os.Exit(1)
    }
    Client = rdsmssql.New(sess)
    
    resp, err := Client.DescribeDBInstances(&DescribeDBInstancesInput{})

    if err != nil {
       panic(err)
    }

    fmt.Println(resp)
}
```
