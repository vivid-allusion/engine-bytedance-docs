---
title: "DolphinScheduler uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DolphinScheduler_uses_Proton"
---

DolphinScheduler's resource center is used to manage and store various resource files used in workflows. It supports remote storage using HDFS and other systems. To use TOS storage, Proton can be leveraged.

<span id="7696046f"></span>
## Self\-managed DolphinScheduler cluster

<span id="799a45df"></span>
### Download dependencies

Please refer to the version information in [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371), select the corresponding Proton version, download the appropriate Proton package, and after extraction, place plugins/hadoop3/proton\-hadoop3\-bundle\-\*.jar into the libs directory of api\-server, master\-server, and worker\-server respectively. If DolphinScheduler is deployed in standalone mode, place it in the libs directory of standalone\-server.

<span id="6f5dc793"></span>
### Configure DolphinScheduler

<span id="182a3229"></span>
#### Modify common.properties

Modify the common.properties file in the conf directory of api\-server, master\-server, and worker\-server. If deployed in standalone mode, modify the common.properties file in the conf directory of standalone\-server.

```Bash
resource.storage.type=HDFS
resource.hdfs.fs.defaultFS=tos://<TOS-bucket-name>
resource.storage.upload.base.path=/dolphinscheduler
```


<span id="26350c07"></span>
#### Modify core\-site.xml

Modify the core\-site.xml file in the conf directory of api\-server, master\-server, and worker\-server. If deployed in standalone mode, modify the core\-site.xml file in the conf directory of standalone\-server. If the file does not exist in the corresponding directory, create it. For detailed configuration, refer to [Using Proton with Hadoop - Configuration changes](https://docs.byteplus.com/docs/E-MapReduce/109384#_2-1-hadoop3-%E7%B3%BB%E5%88%97).

```XML
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>fs.AbstractFileSystem.tos.impl</name>
    <value>io.proton.fs.ProtonFS</value>
  </property>
  <property>
    <name>fs.tos.impl</name>
    <value>io.proton.fs.ProtonFileSystem</value>
  </property>
  <property>
    <name>fs.tos.endpoint</name>
    <value>http://tos-{region}.ivolces.com</value>
  </property>
  <property>
    <name>fs.tos.credentials.provider</name>
    <value>io.proton.common.object.tos.auth.SimpleCredentialsProvider</value>
  </property>
  <property>
    <name>fs.tos.access-key-id</name>
    <value>{your-access-key}</value>
  </property>
  <property>
    <name>fs.tos.secret-access-key</name>
    <value>{your-secret-key}</value>
  </property>
</configuration>
```


<span id="a5d21ef8"></span>
## Verification

After completing the above modifications, restart api\-server, master\-server, and worker\-server to apply the changes.

Try uploading a file in the resource center.
