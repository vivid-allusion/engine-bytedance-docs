---
title: "Reading data from Kafka to ES by using Function Service"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Reading_data_from_Kafka_to_ES_by_using_Function_Service"
---

The following content introduces how to use the microservices application template that is built on BytePlus Function Service (FaaS) to quickly launch a data processing service, which can read data from [Message Queue for Kafka](https://docs.byteplus.com/en/docs/kafka/what-is-message-queue-for-kafka) to [Cloud Search (ES)](https://docs.byteplus.com/en/docs/cloudsearch/what-is-cloudsearch).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Data processing services are mainly used for log processing and analysis, helping enterprises quickly identify and resolve issues while improving operational efficiency. In large systems, to ensure proper collection and analysis of complex log data, the common approach is using Kafka streaming architecture for large\-scale asynchronous data collection. In turn, the collected log data is read by consumer components from Kafka and written in Elasticsearch. FaaS is an alternative to open\-source LogStash. Self\-built LogStash solutions face issues such as data loss, poor collection performance, high resource consumption, and steep learning curves. The FaaS is a Serverless data processing solution that is simpler, lighter, and provides advantages such as auto\-scale, low cost, high throughput, and low latency.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Virtual Private Cloud (VPC)

   * Permission for using VPC has been obtained.

   * A VPC, subnets, and security groups have been created in the region for function deployment. For details, see [Creating Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Creating security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend confining data transmission within the VPC, i.e., creating Kafka instances, ES instances, and FaaS microservices applications within the same VPC.   </div>
   

* Message Queue for Kafka

   * Permission for using Message Queue for Kafka has been obtained.

   * A Kafka instance and the corresponding SASL user, Topic, and Consumer Group have been created. For details, see [Creating instance](https://docs.byteplus.com/en/docs/kafka/creating-instance), [Creating Topic](https://docs.byteplus.com/en/docs/kafka/creating-topic), [Creating Group](https://docs.byteplus.com/en/docs/kafka/creating-group), and [Creating SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser).

* Cloud Search service (ES)

   * Permission for using BytePlus Cloud Search has been obtained.

   * An ES instance has been created. Note that there are requirements for selecting a specific ES version and setting a login password. For details, see [Creating instances](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).

   * An ES index has been created. For details, see [Creating ES index](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65b6u5pyN5Yqh5bqU55So"></span>
### Step 1: Create a microservices application

Create an application with one click by selecting **vefaas\-native\-microservice\-kafka\-to\-es\-exporter** function template.


1. Log in [Function Service console](https://console.byteplus.com/vefaas).

2. In the top bar, select the target region.

3. On the **Function list** page, click **Create function**, and then select **Create [Microservices applications]** .

4. Configure the options on the page as required. The table below contains descriptions of the key options on the page. The rest can keep the default settings.



|Parameter |Description |
|---|---|
|Deployment method |Select **function template: vefaas\-native\-microservice\-kafka\-to\-es\-exporter**. |
|Network |Select the **Virtual Private Cloud**, **subnet**, and **Security groups**  you created as required in the prerequisites above. |



5. Click **Create** to create the function.


<span id=".5q2l6aqk5LqM77ya5pu05paw6YWN572u5paH5Lu2"></span>
### Step 2: Update configuration file

Update the config.json file with your Kafka and ES settings.


1. On the **Code** tab of the function, click the download icon in the upper right to download the code package.

2. Extract the code package.

3. Update the config.json file.

   1. Copy the config_template.json file in the code package to a new file named config.json.

   2. Modify the config.json file as needed.

   ```json
   
   {
     // Kafka related configuration
     "kafka": {
       //Kafka endpoint information
       "bootstrap.servers": "127.0.0.1:8092",
       //Security protocol 
       "security.protocol": "SASL_PLAINTEXT",
       //Debug mode enabled or not
       "debug": false,
       //Topics from which messages will be read
       "topics": "my-topic",
       //Consumer group ID
       "consumer.group.id": "test",
       //SASL related configuration
       "sasl": {
         //SASL enabled or not
         "enabled": true,
         //Authentication mechanism
         "mechanism": "PLAIN",
         //Username
         "username": "test-user",
         //Password
         "password": "test-password"
       }
     },
     // elasticsearch related configuration
     "elasticsearch": {
       //ES address
       "host": "127.0.0.1:9200",
       //Username
       "username": "test-user",
       //Password
       "password": "test-password",
       //Index name under which data will be written
       "index": "test-index"
     }
   }
   ```
   

   
   |Field |Description |
   |---|---|
   |Kafka\-related configuration ||
   |security.protocol |Security protocol. Available values:<br><br><br>* PLAINTEXT<br><br>* SASL_PLAINTEXT (default)<br><br>* SASL_SSL |
   |bootstrap.servers |kafka endpoint information.<br><br><br>* Use the default endpoint if security.protocol is PLAINTEXT.<br><br>* Use the SASL_PLAINTEXT endpoint if security.protocol is SASL_PLAINTEXT.<br><br>* Use the SASL_SSL endpoint if security.protocol is SASL_SSL.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can view endpoint address in <strong>Instance Details \> Service access</strong> on the Message Queue for Kafka console. Setting the address to a private IP is recommended.</div><br> |
   |debug |Whether to enable debug mode.<br><br><br>* true: enable.<br><br>* false: disable |
   |topics |A list of topics from which messages will be read. Separate multiple topics with \",\" e.g., `\"topic1,topic2\"`. |
   |consumer.group.id |Corresponding consumer group ID. |
   |sasl |SASL\-related configuration.<br><br><br>* enabled: whether SASL is enabled. When security.protocol is SASL_PLAINTEXT or SASL_SSL, SASL\-related configurations are required and the value of the field enabled needs to be true.<br><br>* mechanism: authentication algorithm. Currently, only PLAIN or SCRAM\-SHA\-256 are supported. Select one based on password type.<br><br>* username & password: username and password. You can view them in **Instance Details \> User Management** on the Message Queue for Kafka console. |
   |ES\-related configuration ||
   |host |ES address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can view the address on the <strong>Basic information</strong> page of the instance on the Cloud Search console. Setting the address to a private IP with HTTPs as the protocol is recommended..</div><br> |
   |username |User name. You can view the user name on the **Basic information** page of the instance on the Cloud Search console. The default user name is admin. |
   |password |Password. The login password that is required when creating the instance. You can reset the password on the ** Basic information** page of the instance on the Cloud Search console. |
   |index |The index name under which data will be written needs to be created in advance in ES. |
   

4. Run `sh build_and_zip.sh` to start code compilation and packaging.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It must be executed on a Linux platform. Cross\-compilation is not supported.   </div>
   

5. Upload code.

   On the **Code** tab of the function,  click **Upload** \> **Upload local file** to upload the code package generated in step 4.


<span id=".5q2l6aqk5LiJ77ya6YOo572y5bqU55So"></span>
### Step 3: Deploy an application Release code and configurations online for the function.


1. On the page of the function, click **Release** in the upper right corner.

2. Select Latest for the function revision. Other options can keep the default settings.

3. Click **OK**. Wait until the function release is finished.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Send a message using Kafka Topic.

   On the Message Queue for Kafka console, click the instance to go to the **Instance details \> Topic management** tab, then click **Send message** in the Action column of the corresponding topic. Send the word hello as a message.

2. Use ES API to check if the document was created successfully.

   ```graphql
   # The https is allowed --insecure for quick verification
   # test-index is the index name to be used in this example
   curl https://elasticsearch-o-xxxxx.escloud.byteplus.com:9200/test-index/_search --insecure -u admin:xxxx
   ```
   

   The expected ES response is shown below:

   ```json
   {
       "took": 3,
       "timed_out": false,
       "_shards": {
           "total": 1,
           "successful": 1,
           "skipped": 0,
           "failed": 0
       },
       // Created document: contains topic, value, partition, offset, and timestamp of kafka messages. The pair "value": "hello" indicates that message synchronization succeeded.
       "hits": {
           "total": {
               "value": 1,
               "relation": "eq"
           },
           "max_score": 1.0,
           "hits": [
               {
                   "_index": "test-index",
                   "_type": "_doc",
                   "_id": "0xKjb5IBOCL******",
                   "_score": 1.0,
                   "_source": {
                       "header": {},
                       "key": "",
                       "offset": 0,
                       "partition": 7,
                       "timestamp": "2024-10-09 12:57:48.631 +0800 CST",
                       "topic": "my-topic",
                       "value": "hello"
                   }
               }
           ]
       }
   }
   ```
   


<span id=".55u45YWz5pON5L2c"></span>
## Related operation

After deployment succeeds, users do not need to manually adjust the number of instances. The FaaS automatically scales instances in to reduce costs during low load or out to meet the need during heavy load. You can also set scaling policies as needed. For details, refer to [Auto-scaling](https://docs.byteplus.com/en/docs/faas/Elastic_scaling).
