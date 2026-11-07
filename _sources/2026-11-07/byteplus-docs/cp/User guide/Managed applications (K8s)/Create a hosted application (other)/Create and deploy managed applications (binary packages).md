---
title: "Create and deploy managed applications (binary packages)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_binary_packages"
---

Managed applications provide general binary package deployment capabilities, supporting delivery of containerized applications in all languages using the traditional binary package method. This article introduces how to quickly create a managed application using a binary package and deploy it to a Kubernetes cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The application's binary package has been prepared.

* The Kubernetes cluster to be deployed has been connected. For specific operations, see [Connecting deployment resources](https://docs.byteplus.com/en/docs/cp/Deploy_resource).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To deploy the application with VCI, the deployment resource must be a VKE cluster, and the <strong>vci\-virtual\-kubelet</strong> addon must be installed in advance in the cluster.</div>



* (Optional) The NAS file system and mount point have been created. The NAS and the VKE cluster to be deployed must be in the same VPC. For specific operations, see [Getting started with file storage](https://docs.byteplus.com/en/docs/nas/Manual).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to the [CP Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **App delivery \> App management**.

2. On the application management page, click **create application**.

3. On the create application page, select **managed application**, and fill in the required configuration information.

   1. Fill in **application information**. After you finish, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |App ID |Fill in the App ID according to the interface prompt. The App ID is the unique identifier for the App and cannot be modified after creation. |
      |App display name |Customize the app's display name. |
      |App technology stack |In this scenario, select **Others**. |
      |Description |Enter the notes for the current App. This field can be left blank. |
      |Member management |Quickly configure the current App's Members and assign different permissions to each Member to meet the needs of multi\-role collaboration for App delivery.<br><br><br>* Add Members: Add multiple Members to the current App. Only Users with visible permission in the current workspace are supported. The System will by default add the BytePlus root user (root user) and the App creator as administrators.<br><br>* Permission: The System provides two Built\-in roles: administrator and Read only. Each Member can be assigned one or more role permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not allowed to cancel the administrator permission of the root user, and deletion of the root user is not allowed.</div><br> |
      

   2. Fill in **environment configuration**. After you finish, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |Deployment resources |Select the actual deployment location of the App, such as Kubernetes Cluster, cloud server, virtual machine, Physical server, and more. Currently, only Kubernetes Cluster Type deployment resource is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the Previous step is checked to Deploy using the VCI Method, the deployment resource must be a VKE Cluster, AND Install the <strong>vci\-virtual\-kubelet</strong> Addon in the cluster in advance, otherwise the Next step cannot proceed.</div><br> |
      |Namespace |Select the specific namespace. Kubernetes uses namespaces for logical isolation, allowing different groups to share the entire cluster's resources while being managed separately. |
      |Environment ID |Set the unique identifier for the current environment. By default, `${App ID}-prod` is used, and custom values are supported. After the Environment ID is created successfully, modification is not supported. |
      

   3. Fill in **Basic configuration**. After you finish, click **Next: Advanced settings**.

      
      |Parameter |Description |
      |---|---|
      |Deployment method |In this scenario, select **binary package**. |
      |Binary package |The binary package can be provided in the following way:<br><br><br>* **Upload**: Locally upload the required binary package, with a maximum size of 2G supported. |
      |Version |Custom the App's Version number.<br><br>You can click the **Version number uses timestamp** on the right for automatic generation of the Version number. |
      |VCI |Whether to deploy the App using the VCI method. Use this method to deploy the App. There is no need to manage underlying cloud servers or other infrastructure. You only need to provide the image to run the container and pay for the actual resources consumed. For billing details, see [VCI Instructions](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview).<br><br><br>* If checked, the App will be deployed using the VCI method.<br><br>* If not checked, the App will be deployed using the standard Kubernetes method.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To deploy the App using VCI, the deployment resource must be a VKE cluster, and the vci\-virtual\-kubelet addon (<strong>vci\-virtual\-kubelet</strong>) must be installed in the cluster in advance.</div><br> |
      |Service specifications |Define the Service specifications of the App according to business requirements, including: Number of instances, CPU and Memory specifications for each Instance. Support **Default specification** and **Custom specification**.<br><br><br>* Default specification: Supports custom Number of instances and provides common CPU and Memory combinations. Please select the appropriate combination according to business requirements. In the Default specification, CPU request = CPU limit; Memory request = Memory limit.<br><br>* Custom specification: If the Default specification does not meet your requirements, Custom specification is supported, including: custom Number of instances, CPU request, CPU limit, Memory request, and Memory limit. Among them, CPU request ≤ CPU limit; Memory request ≤ Memory limit.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For Deploying using the VCI method, only the upper limit for CPU and Memory needs to be defined. The System will provide the closest VCI Instance specification based on the upper limit you select.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For standard Kubernetes deployment, CPU and memory can be set with no resource limit.</div><br> |
      

   4. (Optional) Fill in **Advanced settings**.

      * Start command

      
      |Parameter |Description |
      |---|---|
      |Startup method |Configure the app's start method. The following two start methods are supported. Please select as needed.<br><br><br>* **Cloud\-native command**: Specify the start command and start parameter according to business requirements. The start command is required, and the start parameter is optional.<br><br>* **Custom script**: If a series of initialization scripts need to be executed before the app starts, it is recommended to start the app by writing a custom script. |
      

      * Runtime environment

      
      |Parameter |Description |
      |---|---|
      |Runtime environment |Set the runtime environment for the binary package. Select according to the actual business scenario.<br><br><br>* **Built\-in**: Debian 12 is used as the default runtime environment for the binary package.<br><br>* **Custom**: If the built\-in environment does not meet requirements, you can customize the runtime environment by setting the **image** and **environment initialization script**.<br><br>   * **Image**: Supports selecting a built\-in image or manually entering a custom image address.<br><br>      * **Built\-in**: The system provides several built\-in base images for common operating systems. By selecting a built\-in image and a custom environment initialization script, you can skip writing a Dockerfile and complete a custom container runtime environment.<br><br>      * **Custom**: Enter the container image address used by the environment. The image address format is `host/namespace/repo:tag`.<br><br>   * **environment initialization script**: Optional. Support custom environment initialization scripts according to business requirements. The environment initialization script is executed when generating the App's runtime environment. |
      

      * Environment variable

      
      |Parameter |Description |
      |---|---|
      |Environment variable |Configure environment variables as needed. The information of environment variables will be injected into the app's running environment, allowing dynamic configuration of the app during runtime.<br><br>Click  **+ Environment variables** and enter the key and value for the environment variables. |
      

      * Health check

         Currently, liveness check: checks whether the container is running. If the probe fails, the container will restart.

      
      |Parameter |Description |
      |---|---|
      |Check method |* HTTP request check: Use the HTTP or HTTPS protocol to send an HTTP GET request to the container, and confirm the container state by checking the response. You need to check the following items:<br><br>   * Protocol: Select HTTP or HTTPS.<br><br>   * Request header: Custom request headers (HTTP headers) in the HTTP request. Click **Add** and enter the key and value for the request header.<br><br>   * Path: Enter the access path used for health check in the business code. The default is `/`, and you can modify it.<br><br>   * Port: Enter the app's access port. The default is 8080, and you can modify it.<br><br>* TCP port check: Send a TCP socket to the app to detect whether a normal connection can be established. You need to check the following items:<br><br>   * Port: Enter the app's access port. The default is 8080, and you can modify it. |
      |Time setting |Specify the time parameters for the check. Valid values:<br><br><br>* Initial wait time: The time to wait after the App starts before the first probe is executed. Default is 1 s.<br><br>* Timeout: The amount of time that you wait for a response after you send a check request. If this time is exceeded, the App is considered unresponsive. Default is 1 s.<br><br>* Check interval: the time interval at which checks are performed. Default value: 10 seconds. |
      |Threshold setting |The result threshold for configuration checks includes:<br><br><br>* Success threshold: The number of successful responses that indicates the system runs as expected after a check request is sent. Default value: 1. This parameter cannot be specified.<br><br>* Failure threshold: The number of consecutive failed responses that indicate the system is abnormal after a check request is sent. Default value: 3. If the App does not respond to the request 3 times, the Application status is considered abnormal. |
      

      * Storage configuration

         Click **add storage mount** to mount storage configuration for the current application instance. Supports mounting multiple storage.

      
      |Parameter |Description |
      |---|---|
      |Type |Currently, **NAS mount** is supported. |
      |File system type |Select the file system type. Supports **Extreme speed** and **Capacity type**. The NAS and the VKE cluster to be deployed must be in the same VPC. |
      |Mount point |select the **File system** and **Mount point** to mount. |
      |Subdirectory |Enter the subdirectory information of the file system to be mounted. The default is the root directory`/`. |
      |Mount path |Mount path in the Managed App Instance. |
      

4. Click **confirm**, and the application will start to deploy. You can view the application deployment progress in the environment tab.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After deployment is complete, the deployment status will change to **Completed**. You can view deployed instance information on the List of instances tab. A running state of **running** indicates that the deployment was successful.


* To view real\-time logs, click **Real\-time log** to access the instance's real\-time log information, which facilitates operations and troubleshooting.

* To view events, click **Event** to see information about events that occurred within the last hour for the instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Create Service resources for the App to enable public network or private network access. For specific operations, see [Access method](https://docs.byteplus.com/en/docs/cp/Access_methods).
