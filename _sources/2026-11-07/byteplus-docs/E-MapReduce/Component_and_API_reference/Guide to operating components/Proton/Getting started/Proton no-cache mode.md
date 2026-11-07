---
title: "Proton no-cache mode"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_no-cache_mode"
---

This article explains how to use the Proton no\-cache mode in Volcano Engine E\-MapReduce (EMR) clusters.

<span id="_1-认证配置"></span>
## 1. Authentication configuration

The Proton acceleration service requires TOS authentication and supports three authentication methods: Assume Role, static AKSK, and environment variable configuration of AKSK. For details, refer to [Hadoop 使用 Proton](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE).

<span id="_2-安装proton-sdk组件"></span>
## 2. Install the Proton SDK component

<span id="_2-1-通过emr管控平台安装（推荐）"></span>
### 2.1 Install via the EMR management platform (recommended)

The EMR cluster will automatically install the Proton SDK component, and no additional action is required.

<span id="_2-2-手动安装"></span>
### 2.2 Manual installation


* **Jar package preparation**


Download the Proton installation package to your local machine. Download link: [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371)

```bash
# Example: Download the Proton installation package version 1.7.0 to your local machine.
wget https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz
# Example: Extract the installation package to your local machine. The extracted directory is the PROTON_HOME directory.
tar xvf proton-1.7.0-bin.tar.gz
```


Run the following command to copy the Proton Hadoop bundle package to the HDFS directory. In this command:


* `PROTON_HOME` is the directory after extracting the Proton installation package

* `hadoop.major.version` is the current Hadoop version. For example, 2 and 3 represent Hadoop 2 and Hadoop 3, respectively

* `proton.version` is the Proton version


```bash
# Copy the Proton Hadoop bundle package to the HDFS directory.
cp ${PROTON_HOME}/plugins/hadoop{hadoop.major.version}/proton-hadoop{hadoop.major.version}-bundle-{proton.version}.jar ${HADOOP_HOME}/share/hadoop/hdfs

# Example: hadoop.major.version=2, proton.version=1.7.0.
cp ${PROTON_HOME}/plugins/hadoop2/proton-hadoop2-bundle-1.7.0.jar ${HADOOP_HOME}/share/hadoop/hdfs
```



* **core\-site.xml configuration**


Add the following four properties to `core-site.xml`.

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
        <value>false</value>
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


<span id="_3-验证访问tos"></span>
## 3. Verify access to TOS

Use the HDFS client to verify TOS access. If you can successfully see the directories or files under the path, the access is successful. Caution: The bucket must be in the same region as the EMR cluster.

```bash
cd $HADOOP_HOME
./bin/hdfs dfs -ls tos://bucket/a/b/c
```
