---
title: "Cloud-based architecture solution for large-scale concurrent business systems"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cloud-architecture-solution-for-business-systems-that-require-large-scale-concurrency-capabilities"
---

This topic describes a cloud architecture solution for large\-scale concurrent business systems built on VKE.

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

Business systems that serve large user bases generally need to be deployed in large\-scale concurrent architectures to handle rapidly increasing business access. This effectively ensures business availability, reduces system overhead, improves business efficiency, and saves costs.

Typical business scenarios include:


* E\-commerce web systems

* Fast\-growing mobile apps


In these scenarios, traffic can surge during specific periods, so the architecture must support temporary business expansion without requiring a full system redesign or optimization.

We recommend that you use the following cloud\-based architecture for large\-scale concurrent business systems based on the preceding requirements:


1. Use CDN to forward static content to effectively reduce load on public network egresses and enhance system robustness.

2. Use Classic Load Balancer (CLB) to distribute access requests, reduce traffic hotspots on individual points, and improve overall system resource utilization. Use CLB together with the autoscaling capabilities of VKE to achieve quick scale\-out to process continuously increased business access requests.

3. Use VKE to deploy core application modules so that they can be built and upgraded quickly. Combined with CP and other pipeline capabilities, VKE also helps establish DevOps practices and improve delivery efficiency.

4. Use CR to effectively support image storage and distribution needs.

5. Use Redis to accelerate access to hot data and enhance system access support.

6. Use cloud databases to provide multi\-replica, high\-performance, and highly reliable database services.

7. Use TOS for static data storage at low costs.

8. Use services, such as APMPlus, VMP, IAM, Cloud Monitor, and TLS, to build a cloud\-based operation and maintenance management platform that meets system operation and maintenance requirements.


<span id=".5pa55qGI5LyY5Yq_"></span>
## Solution advantages


* Massive cloud resources meet quickly increasing access requirements for businesses.

* High availability design for cloud services effectively enhances system stability and availability.

* Specialized operation and maintenance services and back\-end support teams reduce the technical difficulty and complexity of operation and maintenance management.

* Comprehensive security infrastructure and management systems ensure business and data security.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Complete real\-name authentication for the account. For instructions, see [Real name authentication](https://docs.byteplus.com/en/docs/6261/64935).

* ICP filing has been completed for the access domain name in BytePlus. For instructions, see [ICP filing process](https://docs.byteplus.com/en/docs/6428/68727).

* Deploy the application in containers. For instructions, see [Deploying applications](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console#.5q2l6aqk5LqM77ya6YOo572y5bqU55So).

* Upload the image to CR. For instructions, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* (Optional) Set up a Redis database. For Redis instructions, see [Cache for Redis usage process](https://docs.byteplus.com/en/docs/redis/usage-process).

* (Optional) TOS has been integrated. For instructions, see [Getting started with TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* Docker has been installed. For specific operations, see [Installing Docker](https://docs.docker.com/engine/install/centos/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5LiK5Lyg5Lia5Yqh5a655Zmo6ZWc5YOP6Iez6ZWc5YOP5LuT5bqTLWNy"></span>
### Step 1: Upload business container images to CR

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed operating instructions, see <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Getting started with CR</a>.</div>



1. Configure a password to access the repository. This password is required for docker login when using CR.

2. Create a namespace.

3. Create an OCI artifact repository.

4. Push and pull images.

   1. Run the following command to log in to the CR instance.

   ```Bash
   docker login --username=<volcengine_username>@<UserID> cr-cn-<image_repo_instance_region>.volces.com
   ##Example:
   ##docker login --username=v**@100**** cr-cn-beijing.volces.com
   ```
   

   2. Run the following command to tag a local image.

   ```bash
   docker tag [ImageId or image_name] cr-cn-<image_repo_instance_region>.volces.com/<namespace_name>/<image_name>:[image_tag]
   ##Example
   ##docker tag mysql cr-cn-beijing.volces.com/space/mysql:latest
   ```
   

   3. Run the following command to push the image to the CR instance.

   ```bash
   docker push  cr-cn-<image_repo_instance_region>.volces.com/<namespace_name>/<image_name>:[image_tag]
   ##Example
   ##docker push cr-cn-beijing.volces.com/space/mysql:latest
   ```
   

   After the image is transferred, you can query the specified container image in the CR instance and use this image to create an application workload in VKE.


<span id=".5q2l6aqk5LqM77ya6Z2Z5oCB5YaF5a655LiK5Lyg6Iez5a-56LGh5a2Y5YKoLXRvcw=="></span>
### Step 2: Upload static content to TOS

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed operating instructions, see <a href="https://docs.byteplus.com/en/docs/tos/docs-quick-start_1">Getting started with TOS</a>.</div>



1. Activate the TOS service. Log in to the [TOS console](https://console.byteplus.com/tos) and activate the TOS service based on the on\-screen prompts.

2. Create a bucket. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

3. Upload files. For detailed operations, see [Uploading files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65pWw5o2u5bqT"></span>
### Step 3: Create a database

Create a database based on your business requirements, such as MySQL or Redis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can create a Redis database in the same way as creating a MySQL database described in the following content. For detailed operating instructions, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/use_process">Getting started with databases</a> or <a href="https://docs.byteplus.com/en/docs/redis/usage-process">Getting started with cache databases</a>.</div>



1. Create an instance: Create an RDS for MySQL instance and confirm the instance version and instance specification. For the method of creating an instance, see [Creating instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/create_instance).

2. Create a database and account: Create a database and account based on your business requirements, and configure account permissions. For details, see [Creating databases and accounts](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts).

3. Configure an IP allowlist: Only devices added to the allowlist can access the instance. For details, see [Adding IP addresses to allowlists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).

4. Connect to the instance: You can use multiple methods such as a client or the command line to connect. For specific methods, see [Connecting to databases](https://docs.byteplus.com/en/docs/RDS_for_MySQL/connect_instance).


<span id=".5q2l6aqk5Zub77ya5Yib5bu66LSf6L295Z2H6KGh5bm25YWz6IGU5YWs572RLWlw"></span>
### Step 4: Create a CLB instance and associate an EIP

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed operating instructions, see <a href="https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01">Getting started with CLB</a>.</div>



1. [Create a CLB instance](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-02): Create a CLB instance based on your business scenarios and traffic volume.

2. [Create a back-end server group](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-03): Create a back\-end server group and add back\-end servers to provide services.

   1. Create a back\-end server group.

   2. Add back\-end servers.

3. [Create a listener](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-04): Add a listener to the instance and associate it with the back\-end server group.


<span id=".5q2l6aqk5LqU77ya5Yib5bu65a655Zmo6ZuG576k77yM5bm26YOo572y5Lia5Yqh55u45YWz5bel5L2c6LSf6L29"></span>
### Step 5: Create a VKE cluster and deploy business\-related workloads

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed operating instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Quick-guide">Getting started with VKE</a> and <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">VKE user guide</a>.</div>



1. Create a cluster. For detailed steps, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

2. Deploy an application. For detailed operating instructions, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

3. Access the application.

   1. On the **Deployment** page, click the name of the created Deployment.

   2. On the **Deployment details page**, click the **Access method** tab.

   3. On the **Access method** tab, click the **Service** tab, and then click **Create Service**.

   4. On the **Create Service** page, configure service information. After you complete the configuration, click **Confirm** in the lower\-right corner of the page.

   5. On the **Deployment details page**, click the **Access method** tab. Copy the address in the **External endpoint** column on the **Service** tab.

   6. In the browser address bar, enter the **External endpoint** address. If the application can be accessed as expected, it indicates that the application is deployed.

4. Monitor the application.

   After the application is deployed, you can use the Cloud Monitor service to monitor the status of the application, including CPU  and memory usage, to provide support for operation and maintenance. For details about observability in VKE, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id=".5q2l6aqk5YWt77ya5byA5Y-R5Lia5Yqh6YC76L6R"></span>
### Step 6: Develop business logic

Develop the business logic in the database based on your business system plan.

<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After you perform the preceding operations, you can build a system based on VKE for large\-scale concurrent business scenarios.
