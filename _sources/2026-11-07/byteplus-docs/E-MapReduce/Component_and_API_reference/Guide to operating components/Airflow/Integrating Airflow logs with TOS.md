---
title: "Integrating Airflow logs with TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Integrating_Airflow_logs_with_TOS"
---

Airflow supports configuring S3, GCS, WASB, or OSS as remote log service capabilities. TOS, as an BytePlusobject storage solution, can also be integrated in a similar way. This article introduces how to integrate Airflow logs and store them in TOS.

<span id="6c91babe"></span>
# Important notes

When integrating Airflow logs and storing them in TOS, you need to ensure network connectivity between Airflow and the corresponding TOS.

<span id="e62bf8a0"></span>
# Airflow configuration: Create a Connection


1. Log in to Airflow with the admin account. In the Admin menu dropdown in the top navigation, click Connections, create a new Connection, and configure the required parameters on the New Connection page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fbc3237c4f640fb9b20c2fcb668e0fb~tplv-goo7wpa0wc-image.image) </span>

   The core parameters are as follows.

   
   |Parameters |Configuration notes |
   |---|---|
   |**AWS Access Key ID** & **AWS Secret Access Key** |Set to the BytePlusaccount's AK and SK information. For details on obtaining AK and SK, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
   |**Extra** |In Extra, refer to the following format to configure other TOS connection parameters.<br><br>```JSON```<br>```{```<br>```  "region_name": "cn-beijing",```<br>```  "endpoint_url": "https://tos-s3-cn-beijing.ivolces.com",```<br>```  "config_kwargs": {```<br>```    "signature_version": "s3v4",```<br>```    "s3": {```<br>```      "addressing_style": "virtual"```<br>```    }```<br>```  }```<br>```}```<br><br><br>Among them:<br><br><br>* region_name and endpoint_url: Fill in according to actual requirements,<br><br>* addressing_style: Set to "virtual". Airflow uses virtual host style by default when integrating with TOS. |
   

2. After creation, you can see the newly added Connection on the List Connection page. Record the value of "Conn id" for later management configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f5e97643d2e4da9ae5d0f9bb7e3bd7f~tplv-goo7wpa0wc-image.image) </span>


<span id="a2c5b48a"></span>
# EMR management configuration: Modify service parameters


1. Log in to the [EMR on ECS console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/cluster-management/cluster-list). In the service parameters of the Airflow service for the corresponding cluster, search for the keyword "remote" to find and configure remote log\-related parameters.

   * remote_log_conn_id: Set to the value of "Conn id" from the Connection added in Airflow in the previous step.

   * remote_base_log_folder: Configure the default directory in TOS for subsequent log files according to actual business planning.

   * remote_logging: Set to "True" to enable Airflow's remote log feature.

2. After modification, restart the Airflow component to apply the configuration.


<span id="4e3a07b3"></span>
# Service functionality verification


1. You can use a test DAG to verify whether Airflow logs can be properly stored in the TOS Bucket. The following is a simple test DAG example.

   ```Python
   from airflow.decorators import dag
   from airflow.operators.bash import BashOperator
   import pendulum
   @dag(
       dag_id='tos_remote_log_dag',
       start_date=pendulum.datetime(2023, 1, 1, tz="UTC"),
       catchup=False,
       schedule=None,
       tags=['debug'],
   )
   def tos_remote_dag():
       BashOperator(
           task_id='simple_bash_task',
           bash_command='echo "Hello Tos!"',
       )
   tos_remote_dag()
   ```
   

2. View the corresponding Log information in Airflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e6bada3633748e3b6d0c33c7c7ccca7~tplv-goo7wpa0wc-image.image) </span>

3. Check in the TOS console whether the corresponding DAG has written the runtime logs to the configured Bucket.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5722f2174d694796b47ba15b3cfd0bae~tplv-goo7wpa0wc-image.image) </span>
