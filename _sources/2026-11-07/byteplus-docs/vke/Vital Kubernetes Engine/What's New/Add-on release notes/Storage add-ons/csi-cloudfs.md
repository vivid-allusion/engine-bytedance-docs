---
title: "csi-cloudfs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-cloudfs"
---

The csi\-cloudfs is a CloudFS add\-on that enables container clusters to use the service through the standard CSI interface. This topic mainly describes the change history of the csi\-cloudfs add\-on. For more add\-on related introductions and usage methods, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta: Apply for Trial</strong></a>]: This add\-on is in beta. Apply to use it.</div>


<span id="_2024-03"></span>
## March 2024


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.6 |All versions |Maintained |1. The fuse version was updated from 1.5.0\-b1185 to 1.5.0\-hotfix.48\-b1874.<br><br>   New requirements are as follows:<br><br>   * The fuse statfs interface will return current cache space data, supporting but not limited to Linux df/statfs commands.<br><br>   * Using the cloudfs\-fuse command, when specifying the configuration file with the `--config-file` parameter, relative paths are supported.<br><br>   * Calling nn\-\>getFsStats request returns inode information.<br><br>   * Metrics optimization: When saving metrics locally in Prometheus format, timestamps are recorded, and an InfluxDB upload script is added.<br><br>   * Random read scenario optimization: When the difference between the cursor recorded by file and the offset passed by the kernel exceeds 1M, the SDK pread interface will be called; if two consecutive sequential reads occur, it will switch to seek+read.<br><br>   Configuration file optimization is as follows:<br><br>   * output.default.packetsize: 64k \-\> 128k, reduces DN CPU usage, improves performance.<br><br>   * cfs.client.file\-info\-with\-location.enable: false \-\> true; returns block information when you call getfileinfo.<br><br>   * cfs.client.metadata\-cache.enable: false \-\> true, SDK metadata cache is turned on by default.<br><br>2. mount pod uses DNSClusterFirstWithHostNet. |None |


<span id="_2024-01"></span>
## January 2024


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.5 |All versions |Maintained |Avoid scheduling add\-on pods to DCP registered nodes. |None |


<span id="_2023-12"></span>
## December 2023


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.4 |All versions |Maintained |Fixed an issue where csi\-cloudfs might fail to refresh token periodically. |None |


<span id="_2023-10"></span>
## October 2023


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.3 |All versions |Maintained |Updated the CloudFS SDK to the official 1.5 release. |None |


<span id="_2023-08"></span>
## August 2023


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.2 |All versions |Maintained |csi\-cloudfs can be scheduled to nodes marked with taint. |None |


<span id="_2023-07"></span>
## July 2023


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.1 |All versions |Maintained |Fixed the issue where residual CloudFS pods could not be destroyed. |None |


<span id="_2023-06"></span>
## June 2023


|Version number |Compatibility with Kubernetes version |Version status |Change |Impact |
|---|---|---|---|---|
|v1.0.0 |All versions |Maintained |First release of the csi\-cloudfs add\-on, Vital Kubernetes Engine supports using CloudFS through CSI. |None |
