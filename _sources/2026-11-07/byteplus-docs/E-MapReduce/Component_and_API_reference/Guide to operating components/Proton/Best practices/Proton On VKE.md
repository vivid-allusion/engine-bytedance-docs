---
title: "Proton On VKE"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_On_VKE"
---

<span id="2eeffeb6"></span>
## prerequisites

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from EMR on VKE version 3.17.0, the Proton component is integrated into the software stack to provide computational acceleration for the engine.</div>


Ensure that the EMR on VKE virtual cluster version is ≥3.17.0, and that the Proton service has been enabled.

<span id="179e7e1f"></span>
## Create Proton

When creating an EMR On VKE cluster and selecting the Proton service, pay special attention to the following configurations:


1. **Node pool and Pod specifications**: By default, there is 1 ProtonMetaServer Pod and 2 ProtonDataServer Pods. Because ProtonDataServer depends on SSDs, the node pool must have at least 2 nodes with local SSDs.

2. **Storage Class requirements**: For newly created VKE resources, the ebs\-csi plugin is installed by default and no additional configuration is required. When binding existing VKE resources, ensure that the cluster has a Storage Class of ebs\-ssd.

3. **TOS access authorization**: Enter the AK and SK to allow ProtonDataServer to access TOS (the bucket is not bound; you can later access other buckets by changing the AK/SK or modifying the bucket configuration).

4. **Pod anti\-affinity**: By default, ProtonDataServer Pods and Celeborn Pods have anti\-affinity. For mixed deployment requirements, contact technical support.


<span id="d42c5ba1"></span>
## Basic configuration


1. **Cache capacity adjustment**: The cache capacity of ProtonDataServer Pods is controlled by the `limit_cached_bytes` parameter, which defaults to 200 GiB. Since Proton's cache acceleration capability depends on local SSDs, adjust this value according to the size of the local SSD to avoid filling up the node disk.

2. **Scaling requirements**: ProtonDataServer Pods support scaling, with a minimum of 2 Pods. Before scaling, ensure that there are enough nodes with local SSDs.


<span id="b5848acf"></span>
## Node disk cleanup

By default, ProtonDataServer Pods are mounted to the host's local SSD mount directory, that is, the /emr directory (when there are multiple local SSDs, the mount directories are /emr, /emr1, and so on). If, for special reasons, a ProtonDataServer Pod is removed from a node and cache data needs to be cleared, first check the hostpath corresponding to the Proton Pod volume, then go to the local disk mount directory on the host node and delete the files at the corresponding path.

<span id="0c7d3c0f"></span>
## Enable cache acceleration

Currently, the Spark engine supports the Proton cache acceleration feature. Before Proton is installed, Spark uses client\-side acceleration by default; after Proton is installed, Spark supports server\-side acceleration.

<span id="3f0247aa"></span>
### procedure


1. Go to the Spark service parameter configuration page and select the configuration file: **envs**.

2. Edit the parameter `proton_server_mode` \*\*\*\* to `true`, then save and restart the Spark service.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After enabling server\-side cache acceleration, Spark will access ProtonDataServer. At this point, TOS permission control is determined by the AK and SK configured in Proton. Please adjust the AK and SK in advance to avoid job failures due to permission issues.</div>


<span id="f40cac08"></span>
## Proton best practices

<span id="cd25f97a"></span>
### TOS bucket permission isolation

By default, Proton uses the AK and SK specified when creating the cluster to access all TOS buckets. This can be viewed and modified as needed in the service parameters.


|Parameters |Note |
|---|---|
|`fs_tos_access_key_id` |AK used by Proton Server to access TOS |
|`fs_tos_secret_access_key` |SK used by Proton Server to access TOS |


To achieve more granular permission isolation and use different AK/SK pairs to access different buckets, add configurations in the `custom_core_site_dynamic_properties` parameter in the format Key=Value, separated by semicolons, for example:

```HTML
fs.tos.bucket.<bucket>.access-key-id=<AK>;
fs.tos.bucket.<bucket>.secret-access-key=<SK>;
```


After configuration is complete, restart the Proton service for the changes to take effect.

<span id="13ff5187"></span>
### Accelerate TOS access across regions

By default, the TOS region accessed by Proton matches the region where the VKE cluster is located. To accelerate TOS access across regions, modify the Proton service parameters.


|Parameters |Note |
|---|---|
|`tos_endpoint` |Specify the endpoint for accessing TOS |


To configure region settings for accessing TOS buckets in multiple regions within a single Proton cluster, configure endpoints separately for buckets in non\-default regions. Add the configuration to the custom_core_site_dynamic_properties parameter:

```HTML
fs.tos.bucket.<bucket>.endpoint=<endpoint>
```


After completing the configuration, restart the Proton service for the changes to take effect.

<span id="d44042af"></span>
### Proton on\-demand caching

Proton on\-demand caching refers to configuring rules to "allow or prohibit caching of data under certain paths". On\-demand caching helps users better manage cache, improving both efficiency and security. By default, all accessible data will be cached.

**Usage**

In certain scenarios, it is desirable not to cache low\-value data and only cache high\-value data. This can be achieved by configuring allowlist and denylist to specify which paths' data can be cached; data outside these paths will not be cached. Add the configuration to the custom_core_site_dynamic_properties parameter:

```HTML
proton.metaserver.<scheme>.<bucket>.data-cache.blacklist=<blacklist>;
proton.metaserver.<scheme>.<bucket>.data-cache.allowlist=<allowlist>;
```


For example:

```HTML
proton.metaserver.tos.my-bucket.data-cache.blacklist=/;
proton.metaserver.tos.my-bucket.data-cache.allowlist=/user/hadoop,/user/hive;
```


After completing the configuration, restart the Proton service for the changes to take effect. With the above configuration, any data under the /user/hadoop and /user/hive paths will be cached in Proton. Data under other paths will not be cached in Proton.

**Longest prefix matching rule**

Allowlist and denylist configurations follow the "longest prefix matching" rule. For example, suppose we have the following allowlist and denylist configurations.

```Bash
/      --> [allow]
/a/b   --> [deny]
/a/b/c --> [allow]
bash
```



* For /b/file, its longest prefix match is /, and / belongs to the allowlist, so /b/file can be cached.

* For /a/b/file, its prefix matches include / and /a/b, with /a/b being longer. Therefore, the longest prefix match is /a/b, and /a/b belongs to the denylist, so /a/b/file cannot be cached.

* For /a/b/c/file, its prefix matches include /, /a/b, and /a/b/c, with /a/b/c being the longest. Therefore, the longest prefix match is /a/b/c, and /a/b/c belongs to the allowlist, so /a/b/c/file can be cached.


If neither the allowlist nor the denylist configuration includes the root directory, the root directory will be automatically added to the allowlist configuration. Therefore, in the configuration section 'Do not cache data under specified paths', configuring only the denylist achieves the effect where all paths in the denylist are not cached, and all other paths are cached.

**important notes**


* It is invalid for a path to exist in both the allowlist and the denylist simultaneously, which will prevent Proton from starting. The same path can only exist exclusively in either the allowlist or the denylist.

* Only specific paths are supported for configuration; wildcards are not supported, and the '\*' character will be recognized as part of the path.
