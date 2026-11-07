---
title: "Code examples"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/code-example-go"
---

This topic provides code examples for the Redis Go SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Downloading and installing SDK](https://docs.byteplus.com/en/docs/redis/download-install-go-sdk)

2. [Initializing client](https://docs.byteplus.com/en/docs/redis/client-initialization-go)


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Configure request timeout

When using the Go SDK to call Redis interfaces, there is no default timeout.

When you initialize the client, you can specify the request timeout by using `WithHTTPClient(&http.Client{Timeout: <Timeout> * time.Second})`. If the request is not completed within this time, it is terminated and a timeout error is reported.

For example, you can use the following code to set the client's request timeout to 10 seconds.

```go
config = byteplus.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
   WithRegion(region).WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id=".5Yib5bu6LXJlZGlzLeWunuS-iw=="></span>
## Creating Redis instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/createdbinstance">CreateDBInstance</a>.</div>



<Tabs>
<Tab zoneid="lk7Ra1wNLk" title="Example 1">
<TabTitle>Example 1</TabTitle>

Use the following example code to create a Redis instance with sharding cluster enabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e. 8192 MiB).

* Number of shards: 2.

* Number of nodes in each shard: 3.

* In the China (Beijing) region, multi\-availability zone deployment is used, in which the primary node is deployed in the availability zone A, and both secondary nodes are deployed in the availability zone B.

* Associate with two allowlists: `acl-cq014ioqkm9zt5j****` and `acl-cq015pp15v8buvl****`.

* Associate with two tags: `department:game` and `owner:Alice`.

* Billing type: Subscription, expected to be used for 3 months, and auto\-renewal is disabled.


```Go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/redis"
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
      client *redis.REDIS
      resp   *redis.CreateDBInstanceOutput
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

   client = redis.New(sess)

   // Set the configuration information needed for creating an instance
   regionId := "cn-beijing"
   multiAZ := "enabled"
   aza := "cn-beijing-a"
   azb := "cn-beijing-b"
   azc := "cn-beijing-c"
   instanceName := "go_sdk_shardedcluster_test"
   shardedCluster := int32(1)
   password := "Pwd@12****"
   nodeNumber := int32(2)
   shardNumber := int32(2)
   shardCapacity := int64(8192)
   engineVersion := "5.0"
   vpcId := "vpc-1g15eukkrvojk8ibuxxg3****"
   subnetId := "subnet-2fe941zmjud4w5oxruvfw****"
   allowListId1 := "acl-cq0118bj1dah84v****"
   allowListId2 := "acl-cq011jlt9rkap8n****"
   key1 := "department"
   value1 := "game"
   key2 := "owner"
   value2 := "Alice"
   chargeType := "PrePaid"
   purchaseMonths := int32(3)
   autoRenew := false
   
   // Call the CreateDBInstance API to create an instance
   resp, err = client.CreateDBInstance(&redis.CreateDBInstanceInput{
       RegionId:       &regionId,
       MultiAZ:  &multiAZ,
       ConfigureNodes: []*redis.ConfigureNodeForCreateDBInstanceInput{
               {
                       AZ: &aza,
                    },
                    {
                            AZ: &azb,
                        },
                        {
                                AZ: &azc,
                        },
                },
                InstanceName:   &instanceName,
                ShardedCluster: &shardedCluster,
                Password:       &password,
                NodeNumber:     &nodeNumber,
                ShardNumber:    &shardNumber,
                ShardCapacity:  &shardCapacity,
                EngineVersion:  &engineVersion,
                VpcId:          &vpcId,
                SubnetId:       &subnetId,
                AllowListIds: []*string{
                &allowListId1,
        &allowListId2,
        },
        Tags: []*redis.TagForCreateDBInstanceInput{
                {
                        Key:   &key1,
                            Value: &value1,
                        },
                        {
                                Key:   &key2,
                                Value: &value2,
                        },
                },
                ChargeType:     &chargeType,
                PurchaseMonths: &purchaseMonths,
                AutoRenew:      &autoRenew,
        })

   if err != nil {
      fmt.Printf("Error when calling REDISApi->CreateDBInstance, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```





</Tab>
<Tab zoneid="pZBCq7e5v0" title="Example 2">
<TabTitle>Example 2</TabTitle>

Use the following example code to create a Redis instance with sharding cluster disabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e. 8192 MiB).

* Number of nodes: 2.

* Use single\-availability\-zone deployment in the China (Beijing) region, and all nodes are deployed in availability zone A.


```Go
package main

import (
   "fmt"
   "os"

   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/redis"
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
      client *redis.REDIS
      resp   *redis.CreateDBInstanceOutput
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

   client = redis.New(sess)

   // Set the configuration information needed for creating an instance
   
   regionId := "cn-beijing"
   multiAZ := "disabled"
   aza := "cn-beijing-a"
   instanceName := "go_sdk_test"
   shardedCluster := int32(0) 
   password := "Pwd@12****"
   nodeNumber := int32(2)
   shardCapacity := int64(8192)
   engineVersion := "5.0"
   vpcId := "vpc-1g15eukkrvojk8ibuxxg3****"
   subnetId := "subnet-2fe941zmjud4w5oxruvfw****"

   // Call the CreateDBInstance API to create an instance
   resp, err = client.CreateDBInstance(&redis.CreateDBInstanceInput{
      RegionId:       &regionId,
      MultiAZ:  &multiAZ,
      ConfigureNodes: []*redis.ConfigureNodeForCreateDBInstanceInput{
          {
                  AZ: &aza,
              },
          },
      InstanceName:   &instanceName,
      ShardedCluster: &shardedCluster,
      Password:       &password,
      NodeNumber:     &nodeNumber,
      ShardCapacity:  &shardCapacity,
      EngineVersion:  &engineVersion,
      VpcId:          &vpcId,
      SubnetId:       &subnetId,
   })

   if err != nil {
      fmt.Printf("Error when calling REDISApi->CreateDBInstance, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```





</Tab>
</Tabs>


<span id=".5p-l6K-iLXJlZGlzLeWunuS-i-S_oeaBrw=="></span>
## Querying Redis instance information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/describedbinstancedetail">DescribeDBInstanceDetail</a>.</div>


```Go
package main

import (
   "fmt"
   "os"

   
   "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/redis"
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
      client *redis.REDIS
      resp   *redis.DescribeDBInstanceDetailOutput
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
   client = redis.New(sess)

   // Specify the instance ID need to view
   instanceId := "redis-cn048413rhre*****"

  // Call the DescribeDBInstanceDetail API to view the information about the instance
   resp, err = client.DescribeDBInstanceDetail(&redis.DescribeDBInstanceDetailInput{
      InstanceId: &instanceId,
   })

   if err != nil {
      fmt.Printf("Error when calling REDISApi->DescribeDBInstanceDetail, err: %v\n", err)
      os.Exit(1)
   }

   fmt.Println(resp)
}
```
