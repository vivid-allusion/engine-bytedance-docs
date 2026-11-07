---
title: "Code examples"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/code_examples"
---

This topic provides code examples for the Redis Java SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Downloading and installing SDK](https://docs.byteplus.com/en/docs/redis/downloading_and_installing_an_SDK)

2. [Initializing client](https://docs.byteplus.com/en/docs/redis/initializing_a_client)


<span id=".6K6-572u6K-35rGC6LaF5pe25pe26Ze0"></span>
## Configure request timeout

When using the Java SDK to call Redis interfaces, there is no default timeout.

When initializing the client, you can specify its request timeout using `setConnectTimeout(${timeout})` (default unit: milliseconds). If the request is not completed within this time, it will terminate and report a timeout error.

For example, you can set the client's request timeout to 5000 milliseconds using the following code.

```Java
public static ApiClient apiClient = new ApiClient()
        .setCredentials(Credentials.getCredentials(ak,sk))
        .setRegion(region)
        .setConnectTimeout(5000);
```


<span id=".5Yib5bu6LXJlZGlzLeWunuS-iw=="></span>
## Creating Redis instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/createdbinstance">CreateDBInstance</a>.</div>



<Tabs>
<Tab zoneid="b8FPABxebv" title="Example 1">
<TabTitle>Example 1</TabTitle>

Use the following example code to create a Redis instance with sharding cluster enabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e., 8192 MiB).

* Number of shards: 2.

* Number of nodes in each shard: 3.

* Use multi\-availability\-zone deployment in the China (Beijing) region, where the primary node is deployed in availability zone A, and the two secondary nodes are both in availability zone B.

* Associate with two allowlists: `acl-cq014ioqkm9zt5j****` and `acl-cq015pp15v8buvl****`.

* Associate with two tags: `department:game` and `owner:Alice`.

* Billing type: Subscription, expected to be used for 3 months, and auto\-renewal is disabled.


```Java
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.sign.Credentials;

import com.byteplus.redis.RedisApi;
import com.byteplus.redis.model.*;

import java.util.Arrays;

public class TestRedis {
    public static void main(String[] args) throws Exception {
        // Set AKSK authentication information and Region
        // Note the safety of the example code. Code leakage may lead to AKSK leakage, which poses a great security risk.
        String ak = "Your AK";
        String sk = "Your SK";
        String region = "Your Region";

        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);
        RedisApi redisApi = new RedisApi(apiClient);
        
        // Create an interface input parameter
        CreateDBInstanceRequest request = new CreateDBInstanceRequest();
        // Set the interface input parameter according to the parameter description of the CreateDBInstance interface
        request.regionId("cn-beijing")
                .multiAZ("enabled")
            .configureNodes(Arrays.asList(new ConfigureNodeForCreateDBInstanceInput().AZ("cn-beijing-a"), new ConfigureNodeForCreateDBInstanceInput().AZ("cn-beijing-b"), new ConfigureNodeForCreateDBInstanceInput().AZ("cn-beijing-c")))
            .instanceName("java_sdk_shardedcluster_test")
            .shardedCluster(1)
            .password("Pwd@12****")
            .nodeNumber(3)
            .shardNumber(2)
            .shardCapacity(8192L)
            .engineVersion("5.0")
            .vpcId("vpc-30uf6q5ku7vgg7r2qr12n****")
            .subnetId("subnet-2gcljx616l5hc50ztyyzz****")
            .allowListIds(Arrays.asList("acl-cq0118bj1dah84v****", "acl-cq011jlt9rkap8n****"))
            .tags(Arrays.asList(new TagForCreateDBInstanceInput().key("department").value("game"), new TagForCreateDBInstanceInput().key("owner").value("Alice")))
            .chargeType("PrePaid")
            .purchaseMonths(3)
            .autoRenew(false);
   
       // Call the interface to create a Redis instance
        try {
            // Copy the code to run the example. Please print the API return value by yourself.
            CreateDBInstanceResponse response = redisApi.createDBInstance(request);
            System.out.println(response);
        } catch (ApiException e) {
            // Copy the code to run the example. Please print the API error information by yourself.
            System.out.println(e.getResponseBody());
        }
    }
 }
```





</Tab>
<Tab zoneid="ON7GbzIjuj" title="Example 2">
<TabTitle>Example 2</TabTitle>

Use the following example code to create a Redis instance with sharding cluster disabled, configured as follows:


* Database version number: 5.0.

* Available memory: 8 GiB (i.e., 8192 MiB).

* Number of nodes: 2.

* Use single\-availability\-zone deployment in the China (Beijing) region, and all nodes are deployed in availability zone A.


```java
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.sign.Credentials;

import com.byteplus.redis.RedisApi;
import com.byteplus.redis.model.*;

import java.util.Arrays;

public class TestRedis {
    public static void main(String[] args) throws Exception {
        // Set AKSK authentication information and Region
        // Note the safety of the example code. Code leakage may lead to AKSK leakage, which poses a great security risk.
        String ak = "Your AK";
        String sk = "Your SK";
        String region = "Your Region";

        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);
        RedisApi redisApi = new RedisApi(apiClient);
        
        // Create an interface input parameter
        CreateDBInstanceRequest request = new CreateDBInstanceRequest();   
        
        // Set the interface input parameter according to the parameter description of the CreateDBInstance interface
        request.regionId("cn-beijing")
                .multiAZ("disabled")
                .configureNodes(Arrays.asList(new ConfigureNodeForCreateDBInstanceInput().AZ("cn-beijing-a")))
            .instanceName("java_sdk_test")
            .shardedCluster(0)
            .password("Pwd@12****")
            .nodeNumber(2)
            .shardCapacity(8192L)
            .engineVersion("5.0")
            .vpcId("vpc-30uf6q5ku7vgg7r2qr12n****")
            .subnetId("subnet-2gcljx616l5hc50ztyyzz****")
            .allowListIds(Arrays.asList("acl-cq0118bj1dah84v****", "acl-cq011jlt9rkap8n****"))
            .tags(Arrays.asList(new TagForCreateDBInstanceInput().key("department").value("game"), new TagForCreateDBInstanceInput().key("owner").value("Alice")));
            
        // Call the interface to create a Redis instance
        try {
            // Copy the code to run the example. Please print the API return value by yourself.
            CreateDBInstanceResponse response = redisApi.createDBInstance(request);
            System.out.println(response);
        } catch (ApiException e) {
            // Copy the code to run the example. Please print the API return value by yourself.
            System.out.println(e.getResponseBody());
        }
    }
 }
```





</Tab>
</Tabs>


<span id=".5p-l6K-iLXJlZGlzLeWunuS-i-S_oeaBrw=="></span>
## Querying Redis instance information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to <a href="https://docs.byteplus.com/en/docs/redis/describedbinstancedetail">DescribeDBInstanceDetail</a>.</div>


```Java
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.sign.Credentials;

import com.byteplus.redis.RedisApi;
import com.byteplus.redis.model.*;

import java.util.Arrays;

public class TestRedis {
    public static void main(String[] args) throws Exception {
        // Set AKSK authentication information and Region
        // Note the safety of the example code. Code leakage may lead to AKSK leakage, which poses a great security risk.
        String ak = "Your AK";
        String sk = "Your SK";
        String region = "Your Region";

        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);
        RedisApi redisApi = new RedisApi(apiClient);
        
        // Create an interface input parameter
        DescribeDBInstanceDetailRequest request = new DescribeDBInstanceDetailRequest();   
        
        // Set the interface input parameter according to the parameter description of the DescribeDBInstanceDetail interface
        request.instanceId("redis-cn0212gzmh2xs****")
        
        // Call the interface to query the detailed information of the specified Redis instance
        try {
            // Copy the code to run the example. Please print the API error information by yourself.
            DescribeDBInstanceDetailResponse response = redisApi.describeDBInstanceDetail(request);
            System.out.println(response);
        } catch (ApiException e) {
            // Copy the code to run the example. Please print the API error information by yourself.
            System.out.println(e.getResponseBody());
        }
    }
 }
```
