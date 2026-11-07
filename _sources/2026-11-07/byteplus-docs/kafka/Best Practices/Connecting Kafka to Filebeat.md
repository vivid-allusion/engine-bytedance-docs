---
title: "Connecting Kafka to Filebeat"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Connecting_Kafka_to_Filebeat"
---

Filebeat is a lightweight shipper for log forwarding and aggregation. It plays the role of the logging agent, monitoring a specified log file or location, collecting log events, and forwarding the data to either Logstash for more advanced processing or directly into Elasticsearch for indexing.

This topic describes how to connect Message Queue for Kafka to Filebeat.

<span id="ead031da"></span>
## Background Information

The workflow of Filebeat is as follows:


1. Filebeat starts one or more inputs that look in the specified locations for log data.

2. For each log that Filebeat locates, Filebeat starts a harvester. Each harvester reads a single log for new content and sends the new log data to libbeat.

3. Libbeat aggregates the events and sends the aggregated data to the specified output of Filebeat.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b32a9fefee66462bb09b8458d17fca5f~tplv-goo7wpa0wc-image.image) </span>

For more information about Filebeat, please see the below listed OSS reference documents:


* [Filebeat overview](https://www.elastic.co/guide/en/beats/filebeat/8.12/filebeat-overview.html)

* [Filebeat quick start: installation and configuration](https://www.elastic.co/guide/en/beats/filebeat/8.12/filebeat-installation-configuration.html)

* [How Filebeat works](https://www.elastic.co/guide/en/beats/filebeat/8.12/how-filebeat-works.html)


<span id="08867363"></span>
## Prerequisites

The ECS to install Filebeat and the Kafka instances should be in the same region and VPC to ensure smooth network connection.


* Virtual Private Cloud (VPC) and subnet are created in advance. For more information, please see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* ECS instance has been created to install Filebeat and connect to Kafka instances. For more information, please see [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Java Development Kit (JDK) of Java 1.8 or higher versions is installed in the ECS. For more information, please see [Download JDK](https://www.oracle.com/cn/java/technologies/downloads/).

* Kafka instance and topic are created in advance. For more information, please see [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

* If you want to connect to Kafka instances via SASL_SSL and SASL_PLAINTEXT endpoints, a SASL user should be created in advance. For more information, please see [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser).


<span id="e67f5861"></span>
## Step1 download and install Filebeat.


1. Connect to ECS instance. For more information, please see [Login method overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Download the compressed file of Filebeat.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Filebeat 8.X and higher versions are recommended in order to avoid the issue existing in the lower versions that Topic in uppercase cannot be identified, and thus the request cannot find the subscribed Topic.</div>


* <div data-tips="true" data-tips-type="tip">This topic takes installing Filebeat in Linux system as an example. For more information, please see <a href="https://www.elastic.co/guide/en/beats/filebeat/8.12/filebeat-installation-configuration.html">Filebeat quick start: installation and configuration</a>.</div>



```Shell
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.12.0-linux-x86_64.tar.gz
```



3. Unpack the compressed file of Filebeat.


```Shell
tar xzvf filebeat-8.12.0-linux-x86_64.tar.gz
```



4. (Optional) View the Filebeat file.


```Shell
cd filebeat-8.12.0-linux-x86_64
```


Below listed `filebeat`(shown in green) is the binary file to start Filebeat.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdd39459693e4338bce31a01dad35bb0~tplv-goo7wpa0wc-image.image) </span>

<span id="72eab4bf"></span>
## Step2 connect Kafka to Filebeat.

Kafka can be connected to Filebeat as an input or output. Please see the desired chapter according to your actual business scenario.

<span id="f2597524"></span>
### Connect Kafka to Filebeat as an Input


1. Send message from Kafka client to the target Topic.


A proper connection method for sending messages to the target Topic needs to be determined in advance. For more information, please see [Connecting to an instance by using the default endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-default), [Connecting to an instance by using a SASL_PLAINTEXT endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_PLAINTEXT) or [Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

Listed below is a sample message for connecting and sending messages to an instance by using a default (PLAINTEXT) endpoint.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc9f2b162b045c6bcaeb46dd769e604~tplv-goo7wpa0wc-image.image) </span>


2. Connect Kafka to Filebeat, and consume the messages from the target Topic.

   1. Create a configuration file named `filebeat.yaml` in the installation directory of Filebeat.


```Shell
touch filebeat.yaml
```



2. Edit `filebeat.yaml` and configure the related information of Kafka to implement reading data from Kafka.


```Shell
vim filebeat.yaml
```


The configuration information of Kafka varies from different types of endpoints. Please see the desired chapter according to your actual business scenario.


* **PLAINTEXT (Default) endpoints**


The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: kafka
  # Replace it with the actual default endpoint of Kafka instance.
  hosts: ["127.0.0.1:9092"]
  # The client version.
  version: "2.8.0"
  # Replace it with the actual topic to be read from.
  topics: ["topic-test"]
  # The name of ConsumerGroup which is automatically created by Kafka server.
  group_id: "group-test"
  fetch:
    min: 10240
 
output.file:
  # Replace it with the actual local directory path of the file containing the written data.
  path: "{$filepath}/output"
  # The prefix of the file containing the written data.
  filename: "kafka"
```



|**Parameter** |**Description** |
|---|---|
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topics |It is used to specify the Topic list where data is read. |
|group_id |It is used to specify the name of ConsumerGroup to consume the data.<br><br>The ConsumerGroup used by Filebeat is automatically created during client operation process, which means there is no need for manual creation. |
|fetch.min |It is used to specify the minimum message size of each pull from server. The default value is 1, which means at least 1 byte of message for a single pull from server can be returned. It is recommended to increase this minimum value to reduce reading workload. |
|output.file.path |It is used to specify the directory path of the file where the data is written (e.g. `/doc/output`). |
|output.file.filename |It is used to specify the prefix of the file where the data is written. If set as "kafka", then the generated file name is similar to`kafka-20240206.ndjson`. |



* **SASL_PLAINTEXT endpoints**


Access protocol and user configuration are specified in the configuration file when using SASL_PLAINTEXT endpoints. Currently, user types of both PLAIN and SCRAM mechanisms are supported in Kafka instances.

The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: kafka
  # Replace it with the actual SASL_PLAINTEXT endpoint of Kafka instance.
  hosts: ["127.0.0.1:9093"]
  # The client version
  version: "2.8.0"
  # WReplace it with the actual topic to be read from.
  topics: ["topic-test"]
  # The name of ConsumerGroup which is automatically created by Kafka server
  group_id: "group-test"
  fetch:
    min: 10240
  
  # Replace them with the actual user and password.
  username: "user-xxx"
  password: "password-xxx"
  # Configure user type as PLAIN or SCRAM-SHA-25 based on the actual business scenario.
  sasl.mechanism: "PLAIN"
  
output.file:
  # Relapce it with the actual local directory path of the file containing the written data.
  path: "{$filepath}/output"
  # The prefix of the file containing the written data.
  filename: "kafka"
```



|**Parameter** |**Description** |
|---|---|
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topics |It is used to specify the Topic list where data is read. |
|group_id |It is used to specify the name of ConsumerGroup to consume the data.<br><br>The ConsumerGroup used by Filebeat is automatically created during client operation process, which means there is no need for manual creation. |
|fetch.min |It is used to specify the minimum message size of each pull from server. The default value is 1, which means at least 1 byte of message for a single pull from server can be returned. It is recommended to increase this minimum value to reduce reading pressure. |
|username |When using SASL_PLAINTEXT endpoints, SASL username and password authentication are required to access Kafka instances.<br><br>Please fill in the username of PLAIN or SCRAM users. |
|password |Please fill in the password of PLAIN or SCRAM users. |
|sasl.mechanism |Please configure user type as `PLAIN` or `SCRAM-SHA-25` based on the actual business scenario. |
|output.file.path |It is used to specify the directory path of the file where the data is written (e.g. `/doc/output`). |
|output.file.filename |It is used to specify the prefix of the file where the data is written. If set as "kafka", then the generated file name is similar to`kafka-20240206.ndjson`. |



* **SASL_SSL endpoints**


Access protocol and user configuration are specified in the configuration file, and SSL\-encrypted transmission is enabled when using SASL_SSL endpoints. Currently, user types of both PLAIN and SCRAM mechanisms are supported in Kafka instances.

The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: kafka
  # Replace it with the actual SASL_SSL endpoint of Kafka instance.
  hosts: ["127.0.0.1:9095"]
  # The client version.
  version: "2.8.0"
  # Replace it with the actual topic to be read from.
  topics: ["topic-test"]
  # The name of ConsumerGroup which is automatically created by Kafka server.
  group_id: "group-test"
  fetch:
    min: 10240
   
  # Replace them with the actual user and password.
  username: "user-xxx"
  password: "password-xxx"
  # Configure user type as PLAIN or SCRAM-SHA-25 based on the actual scenario.
  sasl.mechanism: "PLAIN"
  
  # Enable SSL configuration.
  ssl.enabled: true
  # Disable domain validation SSL certificate.
  ssl.verification_modeedit: none
  
output.file:
  # Relapce it with the actual local directory path of the file containing the written data.
  path: "{$filepath}/output"
  # The prefix of the file containing the written data.
  filename: "kafka"
```



|**Parameter** |**Description** |
|---|---|
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topics |It is used to specify the Topic list where data is read. |
|group_id |It is used to specify the name of ConsumerGroup to consume the data.<br><br>The ConsumerGroup used by Filebeat is automatically created during client operation process, which means there is no need for manual creation. |
|fetch.min |It is used to specify the minimum message size of each pull from server. The default value is 1, which means at least 1 byte of message for a single pull from server can be returned. It is recommended to increase this minimum value to reduce reading pressure. |
|username |When using SASL_SSL endpoints, SASL username and password authentication are required to access Kafka instances.<br><br>Please fill in the username of PLAIN or SCRAM users. |
|password |Please fill in the password of PLAIN or SCRAM users. |
|sasl.mechanism |Please configure user type as `PLAIN`or `SCRAM-SHA-25` based on the actual scenario. |
|ssl.enabled |When using SASL_SSL endpoints, SSL\-encrypted transmission must be enabled. Therefore, the value for this parameter should be fixed as `true`. |
|ssl.verification_modeedit |It is specified as `none` meaning the domain validation SSL certificate is disabled. |
|output.file.path |It is used to specify the directory path of the file where the data is written (e.g. `/doc/output`). |
|output.file.filename |It is used to specify the prefix of the file where the data is written. If set as "kafka", then the generated file name is similar to`kafka-20240206.ndjson`. |



3. Start Filebeat, and read the data from the target Topic of Kafka.


```Shell
./filebeat -e -c ./filebeat.yaml
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3f1675aec6c4e179f701288daa2980f~tplv-goo7wpa0wc-image.image) </span>


4. In the specified directory where the data is written (e.g. `/doc/output`), you can view the acquired data file named with a specific prefix (e.g. `kafka`).


```Shell
# Enter the target directory.
cd /doc/output

# Replace it with the actual file name (e.g. kafka2-20240206.ndjson) to view the acquired data file.
tail -f ${filename}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef24f206fa2448509bd0c77753e0aa4e~tplv-goo7wpa0wc-image.image) </span>

<span id="12036b7c"></span>
### Connect Kafka to Filebeat as an **Output**


1. Create the data source, i.e. the log file.


Here we choose to create a log file to store log data in file path `/doc/input` of the ECS where Filebeat is installed.

Listed below is a sample command to create a log file and write three records into the file.

```Shell
# Enter the target directory.
cd /doc/input

# Create a log file named test.log and write data into it.
echo "test-msg-1" >> test.log
echo "test-msg-2" >> test.log
echo "test-msg-3" >> test.log
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data in the log file can be read and sent by Filebeat for only once. New data needs to be written into the log file for continuous messages sending.</div>



2. Connect Kafka to Filebeat, read the content of local log file and write it into Kafka.

   1. Create a configuration file named `filebeat.yaml` in the installation directory of Filebeat.


```Shell
touch filebeat.yaml
```



2. Edit `filebeat.yaml` and configure the related information of Kafka to implement reading the content of local log file and writing it into Kafka.


```Shell
vim filebeat.yaml
```


The configuration information of Kafka varies from different endpoints. Please see the desired chapter according to your actual business scenario.


* **PLAINTEXT (Default) endpoints**


The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: log
  # Replace it with actual local directory path for file to be read from. 
  paths:
    - {filepath}/test.log
 
output.kafka:
  # Replace it with the actual PLAINTEXT (default) endpoint of Kafka instance.
  hosts: ["127.0.0.1:9092"]
  # The client version.
  version: "2.8.0"
  # The name of Topic where data is written into.
  topic: "topic-test"
  # Reliability configuration.
  required_acks: -1
  # Partition selection strategy.
  partition.round_robin:
    reachable_only: false
```



|**Parameter** |**Description** |
|---|---|
|paths |The directory path of local log file to be read from, e.g. `/doc/input`. |
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topic |It is used to specify the Topic where data is written. |
|required_acks |It is used to specify the reliability of data writing. Default value is `-1`.<br><br><br>* Value `0` stands for low reliability, meaning the data writing result is ignored.<br><br>* Value `1` stands for medium reliability, meaning successful writing result is returned when data is written into the primary replica.<br><br>* Value `-1` stands for high reliability, meaning successful writing result is returned when data is written into all replicas currently running properly.<br><br><br>Please configure the reliability of data writing based on the actual business scenario. Medium or high level of reliability is recommended. |
|partition.round_robin |It is used to specify the data allocation method. `round_roubin` is recommended since it can increase data aggregation and reduce writing workload.<br><br>Besides `round_roubin`, options `range` and `hash` are also available, and the default value is `range`. |
|partition.round_robin.reachable_only |It is used to specify the partition selection scope. Default value is `false`, which means selecting from all partitions for data writing. Value `true` means only selecting from the normal partitions for data writing. |



* **SASL_PLAINTEXT endpoints**


Access protocol and user configuration are specified in configuration file when using SASL_PLAINTEXT endpoints. Currently, user types of both PLAIN and SCRAM mechanisms are supported in Kafka instances.

The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: log
  # Replace it with actual local directory path for file to be read from.
  paths:
    - {filepath}/test.log

output.kafka:
  # Replace it with the actual SASL_PLAINTEXT endpoint of Kafka instance.
  hosts: ["127.0.0.1:9093"]
  # The client version.
  version: "2.8.0"
  # The name of Topic where data is written into.
  topic: "topic-test"
  # Reliability configuration.
  required_acks: -1
  # Partition selection strategy.
  partition.round_robin:
    reachable_only: false
 
  # Replace them with the actual user and password.
  username: "user-xxx"
  password: "password-xxx"
  # Configure user type as PLAIN or SCRAM-SHA-25 based on the actual business scenario.
  sasl.mechanism: "PLAIN"
```



|**Parameter** |**Description** |
|---|---|
|paths |The directory path of local log file to be read from, e.g. `/doc/input`. |
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topic |It is used to specify the Topic where data is written. |
|required_acks |It is used to specify the reliability of data writing. Default value is `-1`.<br><br><br>* Value `0` stands for low reliability, meaning the data writing result is ignored.<br><br>* Value `1` stands for medium reliability, meaning successful writing result is returned when data is written into the primary replica.<br><br>* Value `-1` stands for high reliability, meaning successful writing result is returned when data is written into all replicas currently running properly.<br><br><br>Please configure the reliability of data writing based on the actual business scenario. Medium or high level of reliability is recommended. |
|partition.round_robin |It is used to specify the data allocation method. `round_roubin` is recommended since it can increase data aggregation and reduce writing workload.<br><br>Besides `round_roubin`, options `range`and`hash` are also available, and the default value is `range`. |
|partition.round_robin.reachable_only |It is used to specify the partition selection scope. Default value is `false`, which means selecting from all partitions for data writing. Value `true` means only selecting from the normal partitions for data writing. |
|username |When using SASL_PLAINTEXT endpoints, SASL username and password authentication are required to access Kafka instances.<br><br>Please fill in the username of PLAIN or SCRAM users. |
|password |Please fill in the password of PLAIN or SCRAM users. |
|sasl.mechanism |Please configure user type as PLAIN or SCRAM\-SHA\-25 based on the actual business scenario. |



* **SASL_SSL endpoints**


Access protocol and user configuration are specified in configuration file, and SSL\-encrypted transmission is enabled when using SASL_SSL endpoints. Currently, user types of both PLAIN and SCRAM mechanisms are supported in Kafka instances.

The content of configuration file is as follows:

```Shell
filebeat.inputs:
- type: log
  # Replace it with actual local directory path for file to be read from. 
  paths:
    - {filepath}/test.log

output.kafka:
  # Replace it with the actual SASL_SSL endpoint of Kafka instance.
  hosts: ["127.0.0.1:9095"]
  # The client version.
  version: "2.8.0"
  # The name of Topic where data is witten into.
  topic: "topic-test"
  # Reliability configuration.
  required_acks: -1
  # Partition selection strategy.
  partition.round_robin:
    reachable_only: false 
  
  # Replace them with the actual user and password.
  username: "user-xxx"
  password: "password-xxx"
  # Configure user type as PLAIN or SCRAM-SHA-25 based on the actual business scenario.
  sasl.mechanism: "PLAIN"
  
  # Enable SSL configuration.
  ssl.enabled: true
  # Disable domain validation SSL certificate.
  ssl.verification_modeedit: none
```



|**Parameter** |**Description** |
|---|---|
|paths |The directory path of local log file to be read from. |
|hosts |It is the endpoint of Kafka instance and multiple endpoints of different protocols can be configured. For more information, please see [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
|version |It is the adopted version of Kafka client and is recommended to configure it according to the version of the purchased server (Kafka instance). For example, configure it as "2.2.0" if Kafka instance of version 2.2.2 is purchased, and similarly "2.8.0" for Kafka instance of version 2.8.2. |
|topic |It is used to specify the Topic where data is written. |
|required_acks |It is used to specify the reliability of data writing. Default value is `-1`.<br><br><br>* Value `0` stands for low reliability, meaning the data writing result is ignored.<br><br>* Value `1` stands for medium reliability, meaning successful writing result is returned when data is written into the primary replica.<br><br>* Value `-1` stands for high reliability, meaning successful writing result is returned when data is written into all replicas currently running properly.<br><br><br>Please configure the reliability of data writing based on the actual business scenario. Medium or high level of reliability is recommended. |
|partition.round_robin |It is used to specify the data allocation method. `round_roubin` is recommended since it can increase data aggregation and reduce writing workload.<br><br>Besides `round_roubin`, options `range`and`hash` are also available, and the default value is `range`. |
|partition.round_robin.reachable_only |It is used to specify the partition selection scope. Default value is `false`, which means selecting from all partitions for data writing. Value `true` means only selecting from the normal partitions for data writing. |
|username |When using SASL_SSL endpoints, SASL username and password authentication are required to access Kafka instances.<br><br>Please fill in the username of PLAIN or SCRAM users. |
|password |Please fill in the password of PLAIN or SCRAM users. |
|sasl.mechanism |Please configure user type as PLAIN or SCRAM\-SHA\-25 based on the actual business scenario. |
|ssl.enabled |When using SASL_SSL endpoints, SSL\-encrypted transmission must be enabled. Therefore, the value for this parameter should be fixed as `true`. |
|ssl.verification_modeedit |It is specified as `none`, meaning the domain validation SSL certificate is disabled. |



3. Start Filebeat, read the content of local log file and write it into Kafka.


```Shell
./filebeat -e -c ./filebeat.yaml
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d74d04d99f74f18aab36659b979fed3~tplv-goo7wpa0wc-image.image) </span>


4. Consume the data from the target Topic via Kafka clients.


A proper connection method for consuming data from the target Topic needs to be determined in advance. For more information, please see [Connecting to an instance by using the default endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-default), [Connecting to an instance by using a SASL_PLAINTEXT endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_PLAINTEXT) or [Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f11a3bdad9b54d4287647f8bf6fd7545~tplv-goo7wpa0wc-image.image) </span>
