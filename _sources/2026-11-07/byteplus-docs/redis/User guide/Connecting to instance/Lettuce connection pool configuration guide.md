---
title: "Lettuce connection pool configuration guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Lettuce_connection_pool_configuration_guide"
---

This topic introduces the underlying connection pool configuration in Spring Data Redis + Lettuce synchronous call scenarios and explains the differences when directly using the Lettuce API.

## Default connection reuse method

For example, with **Spring Data Redis + Lettuce**, regular non\-blocking, non\-transactional operations share underlying connections by default. Lettuce supports reusing multiple concurrent requests on the same connection, so burst traffic may concentrate on shared connections.

In a cloud Redis architecture that uses **cloud load balancer + multiple proxy nodes**, requests on the same connection are continuously forwarded to the same proxy node. Under this forwarding mechanism, if the business primarily sends a large number of requests through a few shared long connections, traffic may concentrate on a few proxy nodes, leading to **uneven load distribution among proxy nodes**: some nodes experience CPU, network, or request processing pressure, and even increased queuing and tail latency, while other nodes still have idle resources. Therefore, even when the overall average load is low, it is recommended to check each proxy node's QPS, resource utilization, and latency. When accessing with the proxy address of BytePlus Cache for Redis, it is recommended to turn on the underlying connection pool.

## Enable underlying connection pool

If contention or response backlog is confirmed on shared connections, a connection pool can alleviate connection\-level pressure. For synchronous calls using `RedisTemplate` or `StringRedisTemplate`, configure them as follows:

1. Introduce `org.apache.commons:commons-pool2`.

   Add the following dependency to the `<dependencies>` node in `pom.xml`. The versions below are examples only; the actual versions should be compatible with the Spring Data Redis and Lettuce versions in your project.

```XML
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-pool2</artifactId>
    <version>2.11.1</version>
</dependency>
```

2. Configure the connection pool and disable underlying connection sharing.

   Integrate the following key configurations into the existing connection factory creation logic. `redisConfiguration` reuses existing connection information; adjust connection pool capacity based on actual business requirements.

```Java
import io.lettuce.core.api.StatefulConnection;
import org.apache.commons.pool2.impl.GenericObjectPoolConfig;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettucePoolingClientConfiguration;

// 1. Set connection pool capacity
GenericObjectPoolConfig<StatefulConnection<?, ?>> poolConfig = new GenericObjectPoolConfig<>();
poolConfig.setMaxTotal(16);   // Example value, adjust according to actual scenario
poolConfig.setMaxIdle(16);    // Example value, adjust according to actual scenario

// 2. Use pooled client configuration
LettucePoolingClientConfiguration clientConfiguration = LettucePoolingClientConfiguration.builder()
    .poolConfig(poolConfig)
    .build();

// 3. Create connection factory, and close underlying connection sharing before initialization
LettuceConnectionFactory factory = new LettuceConnectionFactory(redisConfiguration, clientConfiguration);
factory.setShareNativeConnection(false);
```

> **warning**

> **Enabling pooling and disabling sharing requires simultaneous configuration.** `LettucePoolingClientConfiguration` enables the connection pool, and `setShareNativeConnection(false)` ensures that regular operations also use connections from the pool. Only disabling sharing without enabling pooling increases the overhead of connection creation and closure.

## Directly use Lettuce API

The above switch belongs to Spring Data Redis. When directly using the Lettuce API, explicitly create and return connections via `ConnectionPoolSupport`; asynchronous or reactive applications should use corresponding non\-blocking connection pool methods to avoid blocking and waiting for connections in the event loop. For more information, refer to the official documentation [Lettuce: Connection Pool Usage Instructions](https://redis.github.io/lettuce/advanced-usage/connection-pooling/).

Below is the key code for synchronous calls, which also requires the aforementioned `commons-pool2` dependency. `redisUri` reuses the existing connection URI (including required authentication and TLS configuration).

```Java
import io.lettuce.core.RedisClient;
import io.lettuce.core.api.StatefulRedisConnection;
import io.lettuce.core.support.ConnectionPoolSupport;
import org.apache.commons.pool2.impl.GenericObjectPool;
import org.apache.commons.pool2.impl.GenericObjectPoolConfig;

// Create during application initialization, subsequent requests reuse the same connection pool
RedisClient client = RedisClient.create(redisUri);
GenericObjectPoolConfig<StatefulRedisConnection<String, String>> poolConfig = new GenericObjectPoolConfig<>();
poolConfig.setMaxTotal(16);   // Example value, adjust according to actual scenario
poolConfig.setMaxIdle(16);    // Example value, adjust according to actual scenario

GenericObjectPool<StatefulRedisConnection<String, String>> pool = ConnectionPoolSupport.createGenericObjectPool(client::connect, poolConfig);

// For each operation, borrow a connection; automatically return it after completion; connection borrowing exceptions are handled by business code
try (StatefulRedisConnection<String, String> connection = pool.borrowObject()) {
    String value = connection.sync().get("example:key");
}

// Only execute after the application stops and in-flight operations are completed.
pool.close();
client.shutdown();
```

This creation method returns a wrapped connection by default; when `try-with-resources` calls `close()`, the connection is returned to the pool, eliminating the need to manually call `returnObject()`. This method directly manages the Lettuce connection pool and does not involve Spring Data Redis's `setShareNativeConnection` switch.

## Relevant documents

[Why does Redis still experience high latency even when its average QPS and resource utilization are not high?](https://docs.byteplus.com/en/docs/redis/why-high-latency-with-low-qps-resource-utilization)
