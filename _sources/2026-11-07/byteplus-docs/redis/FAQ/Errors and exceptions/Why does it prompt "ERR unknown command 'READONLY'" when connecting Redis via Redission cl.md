---
title: "Why does it prompt \"ERR unknown command 'READONLY'\" when connecting Redis via Redission client?"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/clusterallfailederror-failed-to-refresh-slots-cache"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem phenomenon

When connecting to the Cache for Redis through the Redission client, this error message `ERR unknown command 'READONLY'` appears. You can view the error message in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8786995a218349f17875a4ba8007fa40.png) </span>

<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible cause

For the Redission client in Cluster mode, the default value of `ReadMode` is `SLAVE`. The Redission client sends the `READONLY` command to the Redis database by default. However, Cache for Redis does not support the `READONLY` command currently. When connecting to a Redis instance through the Redission client in Cluster mode, this error `ERR unknown command 'READONLY'` may appear. For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).

<span id=".5aSE55CG5pa55rOV"></span>
## Solution

You can refer to any of the following methods to avoid the above errors.

<span id=".5pa55rOV5LiA77yI5o6o6I2Q77yJ77ya5bCGLXJlZGlzc2lvbi3lrqLmiLfnq6_orr7nva7kuLotc2luZ2xlLeaooeW8jw=="></span>
### Method 1 (recommended): Set Single mode for the Redission client

The Redission client in Single mode does not use Cluster\-related commands (including the `READONLY` command) to avoid errors such as `ERR unknown command 'READONLY'`.

Refer to the code below to set Single mode for the Redission client.

```Java
Config config = new Config();
// Use Single mode
config.useSingleServer()
        // Access address of Redis instance
        .setAddress("redis://redis-shzlxvk38vs2j****.redis.volces.com:6379")
        // In the example of this article, the default account is used to connect to the Redis database. You only need to set the database login password
        .setPassword("YourPassword");
RedissonClient redisson = Redisson.create(config);
```


<span id=".5pa55rOV5LqM77ya5bCGLWNsdXN0ZXIt5qih5byP55qELXJlYWRtb2RlLeiuvue9ruS4ui1tYXN0ZXI="></span>
### Method 2: Set `ReadMode` of Cluster mode to `MASTER`

If you need to use the Cluster mode of the Redission client as required by business, you can set `ReadMode` to `MASTER` (read data from the primary node only). After setting, the Redission client will not send the `READONLY` command to a Redis database to avoid `ERR unknown command 'READONLY'`.

Refer to the code below to set the `ReadMode` of the Redission client in Cluster mode to `MASTER`.

```Java
Config config = new Config();
// Use Cluster mode
config.useClusterServers()
        // Set ReadMode to MASTER
        .setReadMode(ReadMode.MASTER)
        // Access address of Redis instance
        .addNodeAddress("redis://redis-shzlxvk38vs2j****.redis.volces.com:6379")
        // In the example of this article, the default account is used to connect to the Redis database. You only need to set the database login password
        .setPassword("YourPassword");
RedissonClient redisson = Redisson.create(config);
```
