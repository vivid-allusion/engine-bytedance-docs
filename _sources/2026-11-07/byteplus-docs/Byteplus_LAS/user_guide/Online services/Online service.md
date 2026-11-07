---
title: "Online service"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Online_service"
---

Online servicesis a one\-stop service/model deployment feature provided by the LAS product. It enables users to deploy models or services as online services with one click, and allows access from the public network, VPC intranet, or by binding to a Cloud Load Balancer (CLB). Online services deployed on LAS support scaling, operations monitoring, logging, and other capabilities.

<span id="d136b064"></span>
# Limitations

Online service provides an image\-based deployment mode. Your image repository must be a standard edition instance, and your access control must have sufficient cross\-VPC access quota.

<span id="8e4b594a"></span>
# Deploy online service

<span id="b4104706"></span>
## Preparation


* Before deploying an online service, you must first create a standard edition image instance of the development environment for the debugged data processing task. After completion, deploy this image as an online service. For details, see [Image management](https://docs.byteplus.com/docs/Byteplus_LAS/Image_management).

* You must first prepare the queue resources required for the subsequent operation of the online service. For details, see [Queue management](https://docs.byteplus.com/docs/Byteplus_LAS/queue_manage).

* (Optional) To mount storage to the deployed online service, you must first prepare the storage product to be mounted and the relevant access configuration. Currently, mounting TOS is supported.

* (Optional) To write the deployed service log data into Log Service TLS, you must also enable TLS, prepare the TLS project and log topic for writing log data, and create an IAM role with permission to write data to TLS for subsequent log data writing.


<span id="f965e21d"></span>
## Deploy service: General deployment operations


1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

2. In the left navigation bar, click Online services. After entering the online service management page, click Deploy service to go to the deploy service page to configure.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b70d4b77b29343e5a8c874b7b0eb46fb~tplv-goo7wpa0wc-image.image) </span>

3. Configure service information.

   
   |Configuration item |Configuration description |
   |---|---|
   |Service name |The name of your service |
   |Service description |The description of your service |
   

4. Configure environment information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70b7bc78d0b24c2cab10d4d1c49115d1~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration description |
   |---|---|
   |Image namespace |The image repository address used by the service, which must be a Standard Edition instance and the cross\-VPC access quota must not be full. |
   |Image |The image used by the service |
   |Image version |The image version used by the service |
   |Run command |The startup command for your service, such as python app.py |
   |Port number |Set the listening ports inside the image and the ports exposed for external service. Currently, up to five ports are supported. |
   |Environment variables |The environment variables required for your service at runtime |
   

5. Configure resources for running the online service.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13e6effbf420475e8c112412b08cf269~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration description |
   |---|---|
   |Queue payment type |The type of queue where the service deployment resources reside |
   |Queue & Resource allocation &Instance count |Select the name of the online queue for deploying the service, and allocate the number of CUs and instances for the queue resources used to run the current online service.<br><br>Please ensure that there are enough CUs available for deploying the service. |
   |Storage mount |Select whether to mount storage. Currently, you can mount BytePlus TOS as storage for your online service.<br><br>After selecting to mount TOS, you need to configure the TOS address for the mounted storage, AKSK authentication information, mount point, and more. |
   |Log delivery |Select whether to enable the log delivery switch. After enabling, the log data of the online service will be delivered to the log service TLS for log collection, retrieval, analysis, monitoring, and alerting.<br><br>You need to enable the TLS log service before you can use the log delivery feature. After turning on the switch, you can select the log project and log topic in TLS to deliver log data to, and set the IAM role to be used when writing subsequent log data to TLS. |
   

6. Advanced settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66b3b722ee184893aafa5a653eae5fd0~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration description |
   |---|---|
   |Rolling update |Specify your rolling update strategy.<br><br><br>* MaxUnavailable: Maximum unavailable configuration. Specifies the maximum number of unavailable instances in your cluster during instance updates. The greater the maximum number of unavailable instances, the faster the update operation, but please ensure that the remaining number of instances during the upgrade meets business requirements.<br><br>* MaxSurge: Maximum surge instance configuration. Specifies the maximum number of additional instances that may be created in your cluster during instance updates. The more instances, the faster the update speed, but the update operation will require more additional resources. |
   |Health check & Ready check &Start check |Your configured health check strategy. The health check strategy helps the system determine the health status of your service, enabling load balancing and automatic fault recovery. |
   


<span id="b2e145ec"></span>
## Deploy service: Template deployment \- online retrieval service

You can quickly deploy online services for specific scenarios using templates. For example, in the case of an online retrieval service, you can vectorize your query and then perform retrieval using databases such as vikingdb or opensearch. Taking vikingdb as an example, the main steps are as follows.


1. After entering the Deploy service \*\*\*\* page, select **Use template for quick deployment**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86e968113cea4243b79ed0280f616975~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up sidebar, select Online Retrieval Service as the template name, then click "Use template" below. After completion, the page will pre\-fill the configuration parameters for this template. You need to further configure the following parameters based on your actual requirements.

   
   |Configuration item |Configuration description |
   |---|---|
   |Service name |The name of your service |
   |Environment variables |* [Modification] LAS_SERVICE_VIKINGDB_AK and LAS_SERVICE_VIKINGDB_SK should be set to the ak and sk of vikingdb, so you do not need to pass connection_info when making requests.<br><br>* [Modification] LAS_APP_WORKERS: Number of processes for service startup. Each process can provide services independently. The value should be less than or equal to the number of CPU cores.<br><br>* [New] LAS_SERVICE_OPERATOR_NUM_GPUS: Number of GPUs. 0 means GPUs are not used; any other value specifies the exact number of GPUs.<br><br>* Other environment variables generally do not need to be changed. |
   |Resource deployment |Select the appropriate queue, configure resource allocation, and set whether to mount storage or enable log delivery as needed. |
   

3. Click **Deploy** and wait for the status to change to success, indicating that deployment is complete.


<span id="e42491b5"></span>
## Deploy service: Template deployment \- LAS operator service

You can use templates to quickly deploy online services for specific scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only the bge_sparse_dense_embedding operator is supported.</div>


Taking LAS operator service as an example, you can vectorize your queries and then perform retrieval using databases such as vikingdb or opensearch. Taking vikingdb as an example, the main steps are as follows.


1. After entering the **Deploy service** page, select **Use template for quick deployment**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86e968113cea4243b79ed0280f616975~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up sidebar, select "LAS operator service" as the template name, then click "Use template" below. After completion, the page will pre\-fill the configuration parameters for this template. You need to further configure the following parameters based on your actual requirements.

   
   |Configuration items |Configuration description |
   |---|---|
   |Service name |The name of your service |
   |Environment variables |* [Modify] LAS_APP_WORKERS: Number of service startup processes. Each process can provide services independently. The value should be less than or equal to the number of CPU cores.<br><br>* [New] LAS_SERVICE_OPERATOR_NUM_GPUS: Number of GPUs. 0 means GPUs are not used; any other value specifies the exact number of GPUs.<br><br>* Other environment variables do not need to be modified. |
   |Resource deployment |Select the appropriate queue, configure resource allocation, and set whether to mount storage or enable log delivery as needed. |
   

3. Click **Deploy** and wait for the status to change to success, indicating that deployment is complete.


<span id="d4d3dcfe"></span>
# Invoke online service

<span id="e79eae6b"></span>
## Invocation methods

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The client should retry for connection\-related exceptions (such as IOException in Java) to avoid request errors during service instance upgrades or changes.</div>


<span id="702e9f41"></span>
### Examples

```Bash
curl http://{serving-address}:{serving-port}/api/predict_online -d '[{"gender":0}]'
```


For running online services, you can initiate requests using the curl command just like invoking a regular API service. Specifically:


* `serving-address`: Provided by different invocation methods. You can invoke using the internal network address, or after enabling CLB, use the public network address. For details, refer to the "Internal network address" and "CLB enablement" sections below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the address of the calling environment is within the range allowed by the security group.   </div>
   

* `serving-port`: Aligns with the container "external request call port" specified during deployment.


<span id="9cee8435"></span>
### Internal network address

On the invocation interface, LAS provides the internal address for the online service. This address can be used for communication between different online services.

<span id="59aa183b"></span>
### CLB enablement

For online service invocation, you can associate a CLB instance under your account. By enabling public access on the CLB instance, you can meet the requirements for public network access.

Click the CLB button to enter the configuration page.


* At this point, you need to select the VPC instance where the CLB instance to be connected is located, choose the CLB instance to be connected, and configure the subnet and security group.

* For the security group, you need to allow ICMP protocol access from 0.0.0.0/0 or 100.64.0.0/10 network segments, and allow the specific calling\-side IP to access the service port.


After association, LAS will identify the relevant information of the CLB and display it on the interface to facilitate usage.

<span id="c4ed9784"></span>
# Upgrade service

After the service is successfully deployed, you can perform upgrade operations on the service details page, including modifying the image version, adjusting resource usage, and configuring environment variables.

<span id="f1b0fcb8"></span>
## Operation steps


1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

2. In the left navigation bar, click **Online Service**, then click the target **Service \> Details** to enter the details page.

3. Modify the corresponding configuration information.


<span id="a9c79d11"></span>
## Description of rolling update configuration strategies for service updates

<span id="dc714bfc"></span>
### MaxUnavailable

Specifies the maximum number of service instances that can be unavailable during the update process. This value can be an absolute number (for example, 5) or a percentage of the desired number of instances (for example, 10%; the absolute number calculated from the percentage will be rounded down).

For example, when this value is set to 30%, at the start of the rolling update, the old service can immediately be reduced to 70% of the desired number of instances. Once the new instances are ready, the old instances can be further reduced, and then the new instances are scaled up, ensuring that at least 70% of the desired number of instances are available throughout the update process.

<span id="00ad1750"></span>
### MaxSurge

Specifies the maximum number of instances that can be created in excess of the desired number of service instances. This value can be an absolute number (for example, 5) or a percentage of the desired number of instances (for example, 10%; the absolute number calculated from the percentage will be rounded up).

For example, when this value is set to 30%, at the start of the rolling update, the new instances will be scaled up immediately, ensuring that the total number of old and new instances does not exceed 130% of the desired number of instances. Once the old instances are terminated, new instances will be further scaled out to ensure that the total number of running instances at any time during the update process does not exceed 130% of the desired instance count.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">A lower maximum unavailable value ensures the availability of your business during upgrades; a higher maximum surge value increases your update speed but may consume more additional resources during upgrades. Configure these two values appropriately based on your business requirements.</div>


2. <div data-tips="true" data-tips-type="tip">To ensure availability, instances that are being terminated are not counted when calculating the number of available service instances. Therefore, during rolling updates, you may notice that the number of instances is higher than expected, and before the resources of terminating instances are reclaimed by the system, the total resources currently consumed by the service may exceed the actual number of instances plus the maximum surge. Ensure that your queue has sufficient resources to meet your service availability requirements and update speed.</div>



<span id="ee1a4416"></span>
# Service monitoring

After the service is successfully deployed, you can view relevant metrics on the service monitoring page to understand the service's usage and operation.

Log in toLAS Console. In the left navigation bar, click Online services, then click the target **Service \> Monitoring** to enter the monitoring page and view service monitoring information.

The monitoring metrics are described as follows.


|Category |Metric |Unit |
|---|---|---|
|Service monitoring |Average CPU usage of the service |Cores |
||Average memory usage of the service |GiB |
||Average CPU utilization of the service |% |
||Average memory utilization of the service |% |
||Percentile of service request duration |% |
||Service request QPS |count |
||Service request invocation count |count |
||Service 5\-minute request rate |% |
|Instance monitoring |Instance CPU usage |Number of cores |
||Instance memory usage |GiB |
||Instance average CPU utilization |% |
||Instance average memory utilization |% |
||Instance GPU utilization |% |
||Instance GPU memory utilization |% |
||Instance GPU memory usage |GiB |
||Instance unused GPU memory |GiB |


<span id="1839a270"></span>
# Service scaling

When business load fluctuates, you can scale online services by adjusting the number of instances and the resource allocation per instance to ensure stable business operation and improve utilization.


1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

2. Click**Online Service** in the left navigation bar, then click the target **Service \> Scaling**.

3. After adjusting the resource allocation per instance and the number of instances, click Confirm to submit. Caution: Service deployment resources must not exceed the available resources of the queue they reside in.


<span id="82640e44"></span>
# Terminate service instance

To terminate a service instance, locate the corresponding service instance on the service details page, click "Terminate" after the instance, and confirm termination. The service instance status will transition through the following states until the instance is deleted: Running \> Stopping \> Deleted.
