---
title: "Proton cache mode"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_cache_mode"
---

This article introduces the usage of the Proton cache mode in Volcano Engine E\-MapReduce (EMR) clusters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For cache scenarios, it is recommended to use the TOS accelerator. For details, see the documentation <a href="https://docs.byteplus.com/docs/E-MapReduce/109379">Proton cache mode (TOS Accelerator)</a>.</div>


<span id="_1-认证配置"></span>
## 1 Authentication configuration

Proton acceleration service requires TOS authentication to access TOS, and supports three authentication methods: Assume Role, static AKSK, and environment variable AKSK. For details, refer to [Hadoop 使用 Proton](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE).

<span id="_2-安装proton组件"></span>
## 2 Install the Proton component

<span id="_2-1-通过emr管控平台安装（推荐）"></span>
### 2.1 Install via the EMR management platform (recommended)

When creating an EMR cluster, select the Proton component for installation as shown in the figure. When using the Proton component, it is recommended to select core node models with local SSDs to achieve the best acceleration performance.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce0b7979a770f48a2d4f5439369dd6c3.png) </span>

If you already have an EMR cluster, go to the "Cluster List" page, select "Service List", then click "Add Service", select Proton, and install it.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba8fed063f5b994aab2809822e781104.png) </span>

<span id="_2-2-手动安装"></span>
### 2.2 Manual installation


* **Jar package preparation**


Download the Proton installation package to the local machine. Download link: [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371)

```bash
# Example: Download the Proton installation package version 1.7.0 to the local machine.
wget https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz

# Example: Extract the installation package locally. The extracted directory is the PROTON_HOME directory.
tar xvf proton-1.7.0-bin.tar.gz
```


Run the following command to copy the Proton Hadoop bundle package to the HDFS directory. In this command:


* `PROTON_HOME` is the directory after extracting the Proton SDK installation package.

* `hadoop.major.version` is the current Hadoop version. For example, 2 and 3 represent Hadoop 2 and Hadoop 3, respectively.

* `proton.version` is the Proton version.


```bash
# Copy the Proton Hadoop bundle package to the HDFS directory.
cp ${PROTON_HOME}/plugins/hadoop{hadoop.major.version}/proton-hadoop{hadoop.major.version}-bundle-{proton.version}.jar ${HADOOP_HOME}/share/hadoop/hdfs

# Example: hadoop.major.version=2, proton.version=1.7.0.
cp ${PROTON_HOME}/plugins/hadoop2/proton-hadoop2-bundle-1.7.0.jar ${HADOOP_HOME}/share/hadoop/hdfs
```



* **core\-site.xml configuration**


Add the following three properties to `core-site.xml`. The difference from the non\-cache mode is `proton.cache.enable=true`. If static AKSK is used for TOS authentication, you also need to add the last two ak and sk configurations.

```bash
<configuration>
    <property>
        <name>fs.tos.impl</name>
        <value>io.proton.fs.ProtonFileSystem</value>
    </property>
    <property>
        <name>fs.AbstractFileSystem.tos.impl</name>
        <value>io.proton.fs.ProtonFS</value>
    </property>
    <property>
        <name>proton.cache.enable</name>
        <value>true</value>
    </property>
    <property>
        <name>fs.tos.endpoint</name>
        <value>您的TOS endpoint</value> <!-- 例如：[https://tos-cn-beijing.volces.com](https://tos-cn-beijing.volces.com) -->
    </property>

    <!-- 
    如果采用静态AKSK做TOS认证，需要core-site.xml中添加如下配置。采用其他认证方式则不需要配置。
    其他认证方式见：https://www.volcengine.com/docs/6491/708149#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE
    -->
    <!--
    <property>
        <name>fs.tos.access-key-id</name>
        <value>您的AK</value>
    </property>    
    <property>
        <name>fs.tos.secret-access-key</name>
        <value>您的SK</value>
    </property> 
    -->        
</configuration>
```



* **Start metaserver**


MetaServer needs to be installed on the primary node and started in daemon mode.

```bash
${PROTON_HOME}/bin/proton metaserver --daemon
```



* **Start dataserver**


DataServer needs to be installed on the core node and started in daemon mode.

```bash
${PROTON_HOME}/bin/proton dataserver --daemon
```


<span id="_3-加载元数据"></span>
## 3 Load metadata

After the Proton service is started, you need to run the load command to load TOS metadata. If there are many objects under the path, it may take longer. Upon success, the message "Finish loading path tos://bucket/a/b/c" will be displayed.

You can specify the number of concurrent loading threads using the \-t parameter. By default, the concurrency is set to the number of CPU cores on the node. When there is a large amount of metadata, it is recommended to increase concurrency using the \-t parameter.

```bash
${PROTON_HOME}/bin/proton load -t 10 -m tos://bucket/a/b/c
```


<span id="_4-验证访问tos"></span>
## 4 Verify access to TOS

Use the HDFS client to verify TOS access. If you can successfully see the directories/files under the path, the access is successful.

```bash
cd $HADOOP_HOME
./bin/hdfs dfs -ls tos://bucket/a/b/c
```
