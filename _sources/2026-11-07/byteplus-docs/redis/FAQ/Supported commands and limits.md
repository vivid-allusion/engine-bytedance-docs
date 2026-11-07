---
title: "Supported commands and limits"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/supported-command-and-limit"
---

This topic summarizes the FAQs related to the command support of Cache for Redis.

<span id=".5Li65L2V5pyJ55qELXJlZGlzLeWunuS-i-S4jeiDveS9v-eUqC1rZXlzLeWRveS7pO-8nw=="></span>
### Why can't some Redis instances use the KEYS command?

Redis disables the `flushall`, `flushdb`, and `keys` commands by default. Executing these disabled commands results in `no permission to execute the command`. For more details about the command limit, refer to [Command limits](https://docs.byteplus.com/en/docs/redis/command-limit).

<span id=".5aaC5L2V5ZCv55So6KKr56aB55So55qE5ZG95Luk77yM5aaCLWZsdXNoZGLvvJ8="></span>
### How can I use disabled commands, such as FLUSHDB?

To use the disabled commands (such as `flushall`, `flushdb`, `keys` and so on), you need to remove corresponding commands from the default value of the disabled command parameter (the `disabled commands` parameter). For specific procedures, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

<span id=".5ZCv55So5YiG54mH6ZuG576k55qELXJlZGlzLeWunuS-i-S4uuS9leS9v-eUqOS4jeS6huS6i-WKoeWRveS7pO-8nw=="></span>
### Why can't Redis instances with sharding cluster enabled use transaction commands?

For instances with sharding clusters enabled, you need to ensure that the keys for a transaction command are distributed across a hash slot, whether you connect to the instance in proxy mode (that is, using a public/private address) or in direct mode (that is, using a direct address). You can use hash tags to construct keys for the same slot. For how to use hash tags, refer to [Keys hash tags](https://redis.io/docs/reference/cluster-spec/#hash-tags).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When connecting to an instance to execute transaction commands through <strong>proxy mode</strong>, the keys within the transaction can be distributed in different slots. For more details about transaction command limits for Redis instances with sharding clusters enabled in proxy mode, see <a href="https://docs.byteplus.com/en/docs/redis/command-limit">Transaction command limits</a>.</div>


* <div data-tips="true" data-tips-type="tip">When executing transaction commands using <strong>direct connection mode</strong> to connect instances, you <strong>must strictly ensure that the keys of the transaction operations are all on the same slot</strong>, otherwise the transaction commands will fail to execute.</div>



For more information about command limits, refer to [Command limits](https://docs.byteplus.com/en/docs/redis/command-limit).

<span id=".5ZCv55So5YiG54mH6ZuG576k55qELXJlZGlzLeWunuS-i-mAmui_hy1sdWEt6ISa5pys5omn6KGM5ZG95Luk5pe277yM5Li65LuA5LmI5Lya5Ye6546wLWNyb3Nzc2xvdC1rZXlzLWluLXJlcXVlc3QtZG9uLXQtaGFzaC10by10aGUtc2FtZS1zbG90LeaKpemUme-8nw=="></span>
### Why does the error "CROSSSLOT Keys in request don't hash to the same slot" reported when Redis instances with sharding cluster enabled execute commands through Lua scripts?

For Redis instances with sharding cluster enabled, if the keys to be operated by the command are not distributed in one hash slot, the error `CROSSSLOT Keys in request don't hash to the same slot` is reported. You can build keys with the same slot through hash tag. For how to use hash tags, refer to [Keys hash tags](https://redis.io/topics/cluster-spec?spm=a2c4g.11186623.0.0.335e5ea0K8PtiE).

For more information on the Redis command limit, refer to [Limits on multiple key commands](https://docs.byteplus.com/en/docs/redis/command-limit).

<span id=".5Li65L2V5omn6KGMLWNsdXN0ZXIt55u45YWz5ZG95Luk5pe277yM57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOWSjOWOn-eUny1yZWRpcy3nmoTov5Tlm57nu5PmnpzmnInlt67lvILvvJ8="></span>
### Why do Cache for Redis and the native Redis have different responses when executing Cluster\-related commands?

The proxy nodes are added to Cache for Redis of BytePlus based on the native Redis architecture. The Redis services are accessible through a unified address (domain name) to help reduce application development difficulty and code complexity. When executing Cluster\-related commands, it will have responses different from those of native Redis executing corresponding Cluster\-related commands.

For more details on the Cluster commands supported by Cache for Redis, refer to [Cluster management](https://docs.byteplus.com/en/docs/redis/Cluster_management).
