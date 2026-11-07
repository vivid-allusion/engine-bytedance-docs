---
title: "Third-party SDK client instructions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/instructions-for-third-party-sdk-clients"
---

Redis version of the cache database is fully compatible with the community native Redis, and the database connection method is basically the same. You can choose any SDK client side program compatible with the Redis protocol to connect. This article describes the considerations and usage recommendations when connecting a Redis instance through a third\-party SDK client side program for your reference.

## Precautions

* When you connect to BytePlus cache database Redis version through a third\-party SDK client side program, you need to fully understand the connection management and thread safety issues on the client side to avoid business damage due to improper use of the client side or client side's own problems. You are responsible for the latent risk of data security, compliance, development and maintenance, failure, etc. arising from the use of third\-party SDKs. BytePlus assumes no responsibility for stability, service limitations, and security compliance associated with the above risks, and the quality of service of third\-party SDKs does not count towards service\-level agreements (SLAs) for cloud products and services. For more details, refer to [SLA for Cache for Redis](https://docs.byteplus.com/en/docs/redis/redis-sla).

* You must ensure that the third\-party SDK you use meets the requirements of the relevant software license. For example, some open\-source SDKs may require retention of copyright notices or compliance with specific open\-source licenses (such as Apache license and MIT license) when used, and violating these regulations may result in legal risks.

* In some industries or regions, there may be specific regulatory requirements for data storage, processing, etc. If the business involves cross\-border data storage, it must comply with local laws. You need to ensure that third\-party SDKs do not cause data processing to violate these regulations, especially when it comes to the caching of private data (such as users' personal information and financial data) in Redis.

* In some industries or regions, there may be specific regulatory requirements for data storage, processing, etc. If the business involves cross\-border data storage, it must comply with local laws and regulations. You are responsible for ensuring that third\-party SDKs do not result in data processing operations that violate these regulations, especially those involving the caching of private data (such as users' personal information and financial data) in Redis.

* Keep an eye on the version updates of the corresponding SDK official website or code hosting platform, regularly check the SDK version for known vulnerabilities (CVE), and upgrade in a timely manner. Try to choose a stable version with an active community and a relatively small number of known defects. You need to take the risk of choosing the SDK while choosing. For frequently asked questions about some client side programs, refer to [Error Reports and Exceptions](https://docs.byteplus.com/en/docs/redis/error-and-exception).

* If you use a commercial company's open\-source SDK products (such as Redisson), in order to obtain better support, it is recommended that enterprise users purchase the corresponding technical support services of the commercial company. BytePlus is not obligated to provide support for the products of other third\-party commercial companies.

## Suggestions for use

* Use client side programs in common development languages recommended in this article or by [open source Redis](https://redis.io/docs/latest/develop/clients/).

   > **tip**

   * > For specific procedures, refer to [Connecting to instance via client application](https://docs.byteplus.com/en/docs/redis/connect-instance-via-client).

   * > BytePlus is under no obligation to provide free technical support to cached database Redis Edition instances when you connect to them through third\-party client side programs. However, if you encounter any issues during use, BytePlus will still respond to your request in a timely manner to assist you in troubleshooting the issue.

   **Java**

|Recommended client side program |Recommended client side version |Client side program usage guide |
   |---|---|---|
   |[Jedis](https://github.com/redis/jedis) |* Jedis 3.9 and above: Redis 5.0, Redis 6.0<br><br>* Jedis 4.0 and above: Redis 5.0, Redis 6.0, Redis 7.0<br><br>* Jedis 5.0 and above: Redis 6.0, Redis 7.0 |[Jedis guide](https://redis.io/docs/latest/develop/clients/jedis/) |

   **Python**

|Recommended client side program |Recommended client side version |Client side program usage guide |
   |---|---|---|
   |[redis-py](https://github.com/redis/redis-py)<br><br> |* redis\-py 3.5.3 版本：Redis 5.0、Redis 6.0<br><br>* Redis\-Py 4.5.0 and above: Redis 5.0, Redis 6.0, Redis 7.0 |[redis-py guide](https://redis.io/docs/latest/develop/clients/redis-py/) |

   **Go**

|Recommended client side program |Recommended client side version |Client side program usage guide |
   |---|---|---|
   |[go-redis](https://github.com/redis/go-redis) |Go\-redis v9.0 and above. |[go-redis guide](https://redis.io/docs/latest/develop/clients/go/) |

   **PHP**

|Recommended client side program |Recommended client side version |Client side program usage guide |
   |---|---|---|
   |[Predis](https://github.com/predis/predis) |Predis v3.0.1 and above. |[Predis guide](https://redis.io/docs/latest/develop/clients/php/) |

   **C#**

|Recommended client side program |Recommended client side version |Client side program usage guide |
   |---|---|---|
   |[StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) |StackExchange.Redis 2.7.20 and above.<br><br>> **tip**<br><br><br>> To improve operational stability, we recommend upgrading your client to version 2.7.20 or later. This version fixes a [timeout issue when switching databases using the SELECT command](https://github.com/StackExchange/StackExchange.Redis/issues/2642) that could occur in earlier versions.<br> |[StackExchange.Redis guide](https://stackexchange.github.io/StackExchange.Redis/)<br><br> |

* Make sure sensitive data (such as user privacy and payment information) is encrypted during storage and transmission, and avoid clear text storage; avoid hardcoding passwords or connection information in logs, code repositories.

   Cache for Redis provides SSL (Secure Sockets Layer) encryption service. You can enable SSL encryption in advance, and improve the security of the data link by setting SSL encryption when connecting to the database. For more details, refer to [Client side using SSL encryption to connect to Redis](https://docs.byteplus.com/en/docs/redis/connect-redis-from-client-via-ssl).

* Pay close attention to client side connectivity, bandwidth usage and other monitoring metrics and regularly optimize. For more details, refer to [Data monitoring guide](https://docs.byteplus.com/en/docs/redis/data-monitoring-guide).

* Optimize batch operations and use Pipeline (Jedis/go\-redis) or Lua scripts to reduce network round trips. For more details, refer to [Suggestions for business code development](https://docs.byteplus.com/en/docs/redis/business-code-development-suggestion) and [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).

* Actively feedback problems to the client side community, actively participate in community collaboration, and promote continuous improvement and optimization on the client side.
