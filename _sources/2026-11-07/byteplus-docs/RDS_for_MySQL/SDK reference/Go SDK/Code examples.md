---
title: "Code examples"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/code_examples_3"
---

This topic provides sample code for the MySQL Go SDK for your reference.

<span id="prerequisites"></span>
## **Prerequisites**


* of the SDK has been completed.

* [Client initialization](https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_3) has been completed.


<span id="set-the-established-timeout-for-requests"></span>
## Set the established timeout for requests

There is no established timeout by default when calling the MySQL API with the Go SDK. When initializing the client, you can specify the client request timeout by `WithHTTPClient(&http.Client{Timeout: <timeout> * time.Second})`. If a request is not completed within this time, it will be terminated with an error reported. For example, you can set the request established timeout of the client to 10 seconds with the following code.

```go
config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id="create-a-mysql-instance"></span>
## Create a MySQL instance

For the definitions, value ranges, and other information of parameters used in the following SDK code, refer to [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1).

```go
package  main
import  (
   "fmt"
   "os"
   "github.com/volcengine/volcengine-go-sdk/service/rdsmysqlv2"
   "github.com/volcengine/volcengine-go-sdk/volcengine"
   "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
   "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)
func main()  {
   var  (
            ak          string
            sk          string
            region  string
            config *volcengine.Config
            sess   *session.Session
            client *rdsmysqlv2.RDSMYSQLV2
            resp   *rdsmysqlv2.CreateDBInstanceOutput
            err        error
      )
      ak =  "Your AK"
      sk =  "Your SK"
      region =  "Your Region"
      config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk,  "")).WithRegion(region)
      sess, err = session.NewSession(config)
   if  err !=  nil  {
            fmt.Printf("Failed to create session, err: %v\n", err)
            os.Exit(1)
      }
      client = rdsmysqlv2.New(sess)
      newStr :=  func(s  string)  *string  {
      return  &s
      }
      newInt :=  func(i  int32)  *int32  {
      return  &i
      }
      resp, err = client.CreateDBInstance(&rdsmysqlv2.CreateDBInstanceInput{
            DBEngineVersion: newStr("MySQL_Community_5_7"),
            StorageType:     newStr("LocalSSD"),
            VpcId:           newStr("vpc-*"),
            SubnetId:        newStr("subnet-*"),
            StorageSpace:    newInt(20),
            NodeInfo: []*rdsmysqlv2.NodeInfoForCreateDBInstanceInput{
                  {
                        NodeType: newStr("Primary"),
                        ZoneId:   newStr("cn-beijinga"),
                        NodeSpec: newStr("rds.mysql.1c2g"),
                  },
                  {
                        NodeType: newStr("Secondary"),
                        ZoneId:   newStr("cn-beijinga"),
                        NodeSpec: newStr("rds.mysql.1c2g"),
                  },
            },
            ChargeInfo: &rdsmysqlv2.ChargeInfoForCreateDBInstanceInput{
                  ChargeType: newStr("PostPaid"),
            },
      })
   if  err !=  nil  {
            fmt.Printf("Error when calling RDSMYSQLApi->CreateDBInstance, err: %v\n", err)
            os.Exit(1)
      }
      fmt.Println(resp)
}
```


The parameters in this example are described in the following table.


|**Configuration Item** |**Description** |**Value** |
|---|---|---|
|DBEngineVersion |Instance name. |Your Instance Name |
|NodeInfo |Instance specification configuration. |[<br><br>{<br><br>"NodeType": "Primary",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"ZoneId": "cn\-beijinga",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>}<br><br>] |
|StorageType |Instance storage type. |LocalSSD |
|StorageSpace |Instance storage space. |100 |
|VpcId |The Virtual Private Cloud (VPC) ID. |vpc\-\*\*\*\* |
|SubnetId |Subnet ID. |Subnet123456 |
|InstanceName |Instance name. |Your Instance Name |
|SuperAccountName |Privileged account name. |Test1 |
|SuperAccountPassword |Password of privileged account. |Test@123456 |
|LowerCaseTableNames |Whether the table name is case\-sensitive. |1 |
|DBTimeZone |Time zone. |UTC +08:00 |
|DBParamGroupId |Parameter template ID. |ParamGroup123456 |
|ProjectName |Project of the instance. |Test |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PostPaid"<br><br>} |
|InstanceTags |Instance tag. |{<br><br>"Key": ""aa,<br><br>"Value":"aa"<br><br>} |
|Number |Number of purchased instances. |1 |


<span id="query-mysql-instance-information"></span>
## Query MySQL instance information

For the definitions, value ranges, and other information of parameters used in the following SDK requests, refer to [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail).

```go
package main

import  (
   "fmt"
   "os"
   "github.com/volcengine/volcengine-go-sdk/service/rdsmysqlv2"
   "github.com/volcengine/volcengine-go-sdk/volcengine"
   "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
   "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
   var (
      ak     string
      sk     string
      region string
      config *volcengine.Config
      sess   *session.Session
      client *rdsmysqlv2.RDSMYSQLV2
      resp   *rdsmysqlv2.DescribeDBInstanceDetailOutput
      err    error
   )

   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).WithRegion(region)
   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }
   client = rdsmysqlv2.New(sess)

   newStr := func(s string) *string {
      return &s
   }
   resp, err = client.DescribeDBInstanceDetail(&rdsmysqlv2.DescribeDBInstanceDetailInput{
      InstanceId: newStr("Your InstanceId"),
   })
   if err != nil {
      fmt.Printf("Error when calling RDSMYSQLApi->DescribeDBInstanceDetail, err: %v\n", err)
      os.Exit(1)
   }
   fmt.Println(resp)
}
```


&nbsp;
