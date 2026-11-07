---
title: "Best practices for integrating DolphinScheduler with TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Best_practices_for_integrating_DolphinScheduler_with_TOS"
---

The DolphinScheduler resource center supports the use of object storage. According to the description on the open\-source official website, integration with S3, OSS, and more is already supported. EMR on ECS integrates the open\-source component DolphinScheduler 3.1.9. To expand the product ecosystem, this document provides instructions for using Volcengine TOS as an external object storage link.

<span id="bb7dfa08"></span>
## Prepare Proton

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document uses Proton version 2.2.1 as an example.</div>



1. Download the Proton SDK. For more versions, refer to: [Proton release versions](https://docs.byteplus.com/docs/undefined/69a9698da2ab0e050eaf36f4).


```Bash
wget proton https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.1-bin.tar.gz
```



2. Extract Proton and check whether the bundle.jar package exists under the corresponding Hadoop version in the plugin directory.


Example: The plugins directory contains the proton\-hadoop3\-bundle\-2.2.1.jar package.

<span id="3ba3d1dc"></span>
## Configure DolphinScheduler


1. Prepare dependencies.

   Move proton\-hadoop3\-bundle\-2.2.1.jar to the libs directory of api\-server and worker\-server.

2. Modify common.properties.

   The common.properties files of api\-server and worker\-server both need to be modified as follows.

   ```Bash
   # resource storage type: HDFS, S3, OSS, NONE
   resource.storage.type=HDFS
   # resource store on HDFS/S3 path, resource file will store to this base path, self configuration, please make sure the directory exists on hdfs and have read write permissions. "/dolphinscheduler" is recommended
   resource.storage.upload.base.path=/dolphinscheduler
   # if resource.storage.type=HDFS, the user must have the permission to create directories under the HDFS root path
   resource.hdfs.root.user=hdfs
   # if resource.storage.type=S3, the value like: s3a://dolphinscheduler; if resource.storage.type=HDFS and namenode HA is enabled, you need to copy core-site.xml and hdfs-site.xml to conf dir
   # Resource storage path
   resource.hdfs.fs.defaultFS=tos://${tos_bucket}/dolphinscheduler
   # Specify Proton to access TOS
   fs.tos.impl=io.proton.fs.ProtonFileSystem
   fs.AbstractFileSystem.tos.impl=io.proton.fs.ProtonFS
   # TOS bucket endpoint, using Beijing as an example; select the internal or external domain name as appropriate
   fs.tos.endpoint=tos-cn-beijing.volces.com
   # TOS bucket region
   fs.tos.region=cn-beijing
   # AK/SK for accessing TOS
   fs.tos.access-key-id=xxx
   fs.tos.secret-access-key=xxx
   ```
   


<span id="3861cf86"></span>
## Restart DolphinScheduler


1. After completing the configuration, restart api\-server and worker\-server to apply the changes.

2. Upload files in the resource center.

3. Go to the corresponding TOS bucket and check the files that have been successfully uploaded.
