---
title: "Overview of supported commands"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/supported-command"
---

Cache for Redis supports multiple database versions and instance architectures. Different types of instances have varying levels of support and usage restrictions for Redis commands. This article summarizes the command support documentation for Cache for Redis across different types of commands, helping you quickly find the support status and usage considerations for specific commands.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more details about command limits in Cache for Redis, refer to <a href="https://docs.byteplus.com/en/docs/redis/command-limit">Command limits</a>.</div>


* <div data-tips="true" data-tips-type="tip">Cache for Redis supports processing CAS (compare\-and\-swap) commands through Lua scripts to meet the requirements of Redis atomic actions and improve Redis performance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/lua-user-guide">Lua scripting guide</a>.</div>




|Supported command categories |Description |
|---|---|
|[Redis open-source command support](https://docs.byteplus.com/en/docs/redis/redis-open-source-command-support) |Cache for Redis supports multiple engine versions and architecture types. Different engine versions and architecture types have varying levels of support for open\-source Redis commands. This article uses native Redis commands as a benchmark to provide a detailed reference for command support in Cache for Redis. |
|[Self-developed proxy commands of Cache for Redis](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command) |In addition to being compatible with open\-source Redis commands, the Cache for Redis also supports several self\-developed Proxy commands. You can use these commands in a Redis instance with sharding cluster enabled, which can help you manage the sharding cluster instance more conveniently. |
|[Extension module](https://docs.byteplus.com/en/docs/redis/extended-data-structure) |Building upon native Redis data structures, Cache for Redis also supports [ExBloomFilter](https://docs.byteplus.com/en/docs/redis/exbloom), [ExString](https://docs.byteplus.com/en/docs/redis/exstring), [ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts), [Valkey-Search](https://docs.byteplus.com/en/docs/redis/valkey-search), and [Valkey-Json](https://docs.byteplus.com/en/docs/redis/Valkey-Json) extension modules to meet diverse business scenario requirements. |
