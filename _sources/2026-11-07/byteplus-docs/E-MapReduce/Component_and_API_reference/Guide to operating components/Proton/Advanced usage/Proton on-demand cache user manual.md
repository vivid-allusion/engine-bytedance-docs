---
title: "Proton on-demand cache user manual"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_on-demand_cache_user_manual"
---

<span id="_1-介绍"></span>
## 1 **Introduction**

Proton on\-demand cache refers to configuring rules to "allow or prohibit caching data under certain paths." On\-demand caching helps users better manage cache, improving both efficiency and security. By default, all accessible data will be cached.

<span id="_2-使用方法"></span>
## 2 **Usage**

<span id="_2-1-不缓存指定路径下的数据"></span>
### 2.1 Do not cache data under specified paths

In certain scenarios, it is desirable to prevent low\-value data from occupying excessive cache disk space, so that disk resources can be allocated to other high\-value scenarios. By configuring a "denylist," you can specify which paths' data will not be cached. In the EMR cluster details page, add a custom parameter to **Service List \> Proton \> Service Parameters \> Add Custom Parameter** for **proton.ini**.

The denylist configuration format is:

```Plain
proton.metaserver.<scheme>.<bucket_name>.data-cache.blacklist
```


For example:

```Plain
proton.metaserver.tos.my-bucket.data-cache.blacklist=/user/tmp,/tmp
```


Here, /user/tmp and /tmp are denylist paths. Multiple paths are separated by commas. Paths can be either directories or files. After configuration is complete, Proton must be restarted.

With the above configuration, any data under /user/tmp and /tmp (including all descendant paths) will not be cached in Proton. Data under other paths will be cached in Proton.

<span id="_2-2-仅缓存指定路径下的数据"></span>
### 2.2 Only cache data under specified paths

In certain scenarios, it is desirable to cache only some high\-value data. By configuring both an "allowlist" and a "denylist," you can specify which paths' data will be cached, and all other data will not be cached. In the EMR cluster details page, add a custom parameter to **Service List \> Proton \> Service Parameters \> Add Custom Parameter** for **proton.ini**.

The allowlist configuration format is:

```Plain
proton.metaserver.<scheme>.<bucket_name>.data-cache.allowlist
```


For example:

```Plain
proton.metaserver.tos.my-bucket.data-cache.allowlist=/user/hadoop,/user/hive
proton.metaserver.tos.my-bucket.data-cache.blacklist=/
```


After configuration is complete, Proton must be restarted. With the above configuration, any data under /user/hadoop and /user/hive (including all child paths, grandchild paths, and all descendant paths) will be cached in Proton. Data under other paths will not be cached in Proton.

<span id="_2-3-最长前缀匹配规则"></span>
## 2.3 Longest prefix matching rule

Blocklist and allowlist configurations follow the "longest prefix matching" rule. We use path_a to represent the path to be matched, and all paths in the allowlist and blocklist together form a path list. For any path path_i in the path list, if path_i is a prefix of path_a, then path_i and path_a are considered to have a prefix match. Among all paths in the path list that have a prefix match with path_a, the longest one is the "longest prefix match" of path_a.

For example, suppose we have the following allowlist and blocklist configurations.

```bash
/      --> [allow]
/a/b   --> [deny]
/a/b/c --> [allow]
```



* For /b/file, its longest prefix match is /, and / belongs to the allowlist, so /b/file can be cached.

* For /a/b/file, its prefix matches include: / and /a/b, where /a/b is longer, so the longest prefix match is /a/b. Since /a/b belongs to the blocklist, /a/b/file cannot be cached.

* For /a/b/c/file, its prefix matches include: /, /a/b, and /a/b/c, where /a/b/c is the longest. Since /a/b/c belongs to the allowlist, /a/b/c/file can be cached.


If neither the allowlist nor the blocklist configuration includes the root directory, the root directory will be automatically added to the allowlist configuration. Therefore, in the configuration section "Do not cache data under specified paths", configuring only the blocklist achieves the effect that all paths in the blocklist are not cached, while all other paths are cached.

<span id="_3-注意事项"></span>
## 3 Important notes


1. It is illegal for a path to exist in both the blocklist and allowlist simultaneously, and this will prevent Proton from starting. The same path can only exist exclusively in either the allowlist or the blocklist.

2. Only specific paths are supported for configuration; wildcards are not supported, and the '\*' symbol will be recognized as part of the path.
