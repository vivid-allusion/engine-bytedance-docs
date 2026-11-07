---
title: "Code examples"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/code-example-go"
---

This topic provides sample code for the MongoDB Go SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


1. [Downloading and installing](https://docs.byteplus.com/en/docs/mongodb/download-install-go-sdk)

2. [Initializing the client](https://docs.byteplus.com/en/docs/mongodb/client-initialization-go)


<span id=".6K6-572u6K-35rGC6LaF5pe25pe26Ze0"></span>
## Configure request timeout

When using the Go SDK to call MongoDB interfaces, there is no default timeout.

You can specify the established timeout for client requests through `WithHTTPClient(&http.Client{Timeout: ${timeout} * time.Second})` when initializing the client. If the request is not completed within this time, it will be terminated with a timeout error reported.

For example, you can use the following code to set the client's request timeout to 10 seconds.

```go
config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
   WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu6LW1vbmdvZGIt5a6e5L6L"></span>
### Creating a MongoDB instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/createdbinstance">CreateDBInstance</a>.</div>



<Tabs>
<Tab zoneid="SCyAWFKsay" title="Example 1">
<TabTitle>Example 1</TabTitle>

Create a sharding cluster instance with the sample code below and configure it as follows:


* The availability zone where the instance is located: China (Beijing) \- availability zone A.

* Storage capacity: 100 GiB.

* Node specifications:

   * Include 2 Mongos nodes, each with 2 cores 4 GiB.

   * Include 2 shards (each includes 3 nodes by default), and the specifications of the nodes in each shard is 2 cores 4 GiB.


```go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/mongodb"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
)
func main() {
   var (
      ak     string
      sk     string
      region string
      config *byteplus.Config
      sess   *session.Session
      client *mongodb.MONGODB
      resp   *mongodb.CreateDBInstanceOutput
      err    error
   )

   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
      WithRegion(region)

   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }

   client = mongodb.New(sess)

   // Set the configuration information needed for creating an instance
   zoneId := "cn-beijing-a"
   nodeSpec := "mongo.shard.2c4g"
   storageSpaceGb := 100
   vpcId := "vpc-13f24t16guqdc3n6nu4k5****"
   subnetId := "subnet-rr96lovl7f28v0x58tv****"
   instanceName := "go_sdk_test_shard"
   mongosNodeSpec := "mongo.mongos.2c4g"
   instanceType := "ShardedCluster"
   shardNumber := 2
   mongosNodeNumber := 2
      

   // Call the CreateDBInstance API to create an instance
   resp, err = client.CreateDBInstance(&mongodb.CreateDBInstanceInput{
      ZoneId:             &zoneId,
      NodeSpec:           &nodeSpec,
      StorageSpaceGB:     &storageSpaceGb,
      VpcId:              &vpcId,      
      SubnetId:           &subnetId,
      InstanceName:       &instanceName,
      MongosNodeSpec:     &mongosNodeSpec,
      InstanceType:       &instanceType,
      shardNumber:        &shardNumber,
      MongosNodeNumber:   &mongosNodeNumber,
   })

   if err != nil {
      fmt.Printf("Error when calling MONGODBApi->CreateDBInstance, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```



</Tab>
<Tab zoneid="D1eRhLm0ZF" title="Example 2">
<TabTitle>Example 2</TabTitle>

Create a replica set instance (containing three nodes by default) with the configuration code below and configure it as follows:


* The availability zone where the instance is located: China (Beijing) \- availability zone A.

* Storage capacity: 100 GiB.

* Node specification: 2 cores 4 GiB.


```go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/mongodb"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
)
func main() {
   var (
      ak     string
      sk     string
      region string
      config *byteplus.Config
      sess   *session.Session
      client *mongodb.MONGODB
      resp   *mongodb.CreateDBInstanceOutput
      err    error
   )

   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
      WithRegion(region)

   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }

   client = mongodb.New(sess)

   // Set the configuration information needed for creating an instance
   vpcId := "vpc-13f24t16guqdc3n6nu4k5****"
   zoneId := "cn-beijing-a"
   nodeSpec := "mongo.2c4g"
   storageSpaceGb := 100
   subnetId := "subnet-rr96lovl7f28v0x58tv****"
   instanceName := "go_sdk_test_replica"

   // Call the CreateDBInstance API to create an instance
   resp, err = client.CreateDBInstance(&mongodb.CreateDBInstanceInput{
       VpcId:              &vpcId,
       ZoneIds:            &zoneIds,
       NodeSpec:           &nodeSpec,
       StorageSpaceGB:     &storageSpaceGb,
       SubnetId:           &subnetId,
       InstanceName:       &instanceName,
   })

   if err != nil {
      fmt.Printf("Error when calling MONGODBApi->CreateDBInstance, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```



</Tab>
</Tabs>


<span id=".5p-l6K-iLW1vbmdvZGIt5a6e5L6L5L-h5oGv"></span>
### Querying MongoDB instances

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of parameters used in the following SDK requests, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail">DescribeDBInstanceDetail</a>.</div>


```go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/mongodb"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
)

func main() {
   var (
      ak     string
      sk     string
      region string
      config *byteplus.Config
      sess   *session.Session
      client *mongodb.MONGODB
      resp   *mongodb.DescribeDBInstanceDetailOutput
      err    error
   )

   ak = "Your AK"
   sk = "Your SK"
   region = "Your Region"
   config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
      WithRegion(region)

   sess, err = session.NewSession(config)
   if err != nil {
      fmt.Printf("Failed to create session, err: %v\n", err)
      os.Exit(1)
   }

   client = mongodb.New(sess)

   // Specify the instance ID need to view
   instanceId := "mongo-replica-e649ae42****"

   // Call the DescribeDBInstanceDetail API to view the information about the instance
   resp, err = client.DescribeDBInstanceDetail(&mongodb.DescribeDBInstanceDetailInput{
      InstanceId: &instanceId,
   })

   if err != nil {
      fmt.Printf("Error when calling MONGODBApi->DescribeDBInstanceDetail, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```
