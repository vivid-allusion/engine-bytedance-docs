---
title: "Create and deploy Managed App (JAR/WAR)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_apps_JAR_WAR"
---

This article describes how to quickly create a Java App using a JAR or WAR package and deploy it to a Kubernetes cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The JAR or WAR package for the App has been prepared.

* The Kubernetes cluster to be deployed has been connected. For specific operations, see [Connect deployment resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To deploy the App using a VCI, the deployment resource must be a VKE cluster with the network model set to <strong>VPC\-CNI</strong>, and the cluster must have the vci\-virtual\-kubelet<a href="https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet"><strong> addon</strong></a> installed in advance.   </div>
   

* (Optional) The NAS file system and mount point have been created. The NAS and the VKE cluster to be deployed must be in the same VPC. For specific operations, see [Getting Started with File Storage](https://docs.byteplus.com/en/docs/nas/Manual).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the App management page.

   1. Log in to the [CP Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the workspace.

   4. In the left navigation bar, select **App delivery \> App management**.

2. On the App management page, click **Create App**.

3. On the Create App page, select **Managed App**, and fill in the required configuration information for the App.

   1. Fill in the **App information**. After completion, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |App ID |According to the prompt on the interface, enter the app ID. The app ID is the unique identifier for the app and cannot be changed after creation. |
      |App display name |Customize the App display name. |
      |App deployment types |Select **container**. |
      |App technical stack |This scenario selects **Java**. |
      |Description |Enter the app's notes, which can be left blank. |
      |Member management |Quickly configure app members and assign different permissions to each member to meet the requirements of multi\-role collaboration for app delivery.<br><br><br>* Add members: Add multiple members to the app. Only users with workspace visible permission can be selected. The system will, by default, add the BytePlus root user (primary account) and the app creator as administrators.<br><br>* Permissions: The system has built\-in administrator and read only roles. Each member supports configuring one or more role permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot remove the administrator permission from the root user, and you cannot delete the root user.</div><br> |
      

   2. Fill in the **Basic configuration**. After completion, click **Next: Environment configuration**.

      
      |Parameter |Description |
      |---|---|
      |Deployment method |Select **binary package** in this scenario. |
      |App package type |Supports **JAR package** and **WAR package** types.<br><br><br>* JAR package: General JAR package deployment, suitable for Dubbo and Spring Boot applications.<br><br>   * Java version: Select the runtime environment version for the JAR package. Supports OpenJDK8, OpenJDK11, OpenJDK17, and OpenJDK21.<br><br>* WAR package: General WAR package deployment, suitable for Dubbo and Spring applications.<br><br>   * Select the runtime environment version for the WAR package, including Java version and Tomcat version.<br><br>   * Java version supports OpenJDK8, OpenJDK11, OpenJDK17, and OpenJDK21.<br><br>   * Tomcat version supports Apache Tomcat 10.1.11, Apache Tomcat 9.0.78, Apache Tomcat 8.5.91, and Apache Tomcat 7.0.109. |
      |App package |Upload the app's JAR package or WAR package locally. The maximum supported size is 2G, and the file format must be `*.jar` or `*.war`. |
      |Version |Custom version number for the App.<br><br>You can click **Version number use timestamp** on the right to automatically generate the version number. |
      |VCI |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deploy using the VCI method. This is only applicable to VKE clusters with the network model <strong>VPC\-CNI</strong>, and in the cluster, you must install <a href="https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet"><strong>vci\-virtual\-kubelet</strong></a> addon in advance.</div><br><br><br>Whether to deploy the App using the VCI method. Deploying the App using this method does not require managing underlying cloud servers or other infrastructure. You only need to provide the image to run the container and pay for the actual resources consumed. For billing details, see [VCI billing instructions](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview).<br><br><br>* If checked, the App will be deployed using the VCI method.<br><br>* If not checked, the App will be deployed using the standard Kubernetes method. |
      |Service specifications |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For deployment using the VCI method, you only need to define the upper limit for CPU and memory. The system will provide the closest VCI instance specification based on the upper limit you select.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For deployment using the standard Kubernetes method, CPU and memory can have no upper limit.</div><br><br><br><br>Define the service specifications for the App according to business requirements, including the number of instances and the CPU and memory specifications for each instance. Supports **default specifications** and **custom specification**.<br><br><br>* Default specifications: You can customize the number of instances, and common CPU and memory combinations are provided. Please select the appropriate combination according to your business needs. In default specifications, CPU request = CPU limit; memory request = memory limit.<br><br>* Custom specification: If the default specifications cannot meet your requirements, you can use custom specifications, including custom number of instances, CPU request, CPU limit, memory request, and memory limit. Among them, CPU request ≤ CPU limit; memory request ≤ memory limit. |
      

   3. Fill in the **Environment configuration**. After completion, click **Next: Advanced settings**.

      
      |Parameter |Description |
      |---|---|
      |Deployment resource |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you check to deploy using the VCI method in the previous step, you can only select VKE clusters with the network model set to <strong>VPC\-CNI</strong>. In addition, the cluster must have the vci\-virtual\-kubelet<a href="https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet"><strong> addon</strong></a> installed; otherwise, you cannot proceed to the next step.</div><br><br><br>Select the actual deployment location for the App, such as a Kubernetes cluster, cloud server, virtual machine, physical server, and so on. Supports deployment resources of the Kubernetes cluster type. |
      |Namespace |Select the specific namespace. Kubernetes uses namespaces for logical isolation, making it easier to manage different groups separately while sharing the entire cluster's resources. |
      |Environment ID |Set the unique identifier for the environment. The default is `${App ID}-prod`, and customization is supported. Modification of the environment ID is not supported after it is created successfully. |
      

   4. (Optional) Fill in the **Advanced settings**.

      * Start command

         
         |Parameter |Description |
         |---|---|
         |Start command (JAR) |* Start command: set the start command according to business requirements. The default command `java -jar "$PACKAGE_PATH" $ARGS` supports most scenarios. Among them, `$PACKAGE_PATH` indicates the path where the JAR package is uploaded to the container.<br><br>* Start parameter: set the start parameter according to business requirements; this can be left blank. The start parameter will be filled into the start command's `$ARGS`. |
         |Start command (WAR) |* Start command: Set the start command according to business requirements. The default command`CATALINA_OPTS="$OPTIONS" catalina.sh run` supports most scenarios.<br><br>* Start parameter: Set the start parameter according to business requirements. This can be left empty. The start parameter will be filled into the start command's `$OPTIONS`. |
         |Tomcat configuration (WAR) |* Port: set the App's port. The default is 8080 and can be modified.<br><br>* Tomcat context: set the App's access path. The default is `/` and can be modified.<br><br>* Maximum thread count: configure the connection pool size; the corresponding parameter is maxThreads. The default is 400 and can be modified.<br><br>* Tomcat encoding: select the Tomcat encoding method. Supports GBK, GB2312, ISO\-8859\-1 (default value), and UTF\-8.<br><br>   * Use HTTP body encoding for URL: after turning on, the URL will use the same encoding method as the HTTP body. This is mainly used to resolve garbled characters when special characters such as Chinese are present in the URL's request parameter. |
         

      * Environment variable

         
         |Parameter |Description |
         |---|---|
         |Environment variable |Configure environment variables as needed. The information of environment variables will be injected into the App's runtime environment, allowing dynamic configuration of the application at runtime.<br><br>Click  **+ Environment variables** and enter the key and value for the environment variables. |
         

      * Health check

         Check whether the container is running. If the probe fails, the container will be restarted.

         
         |Parameter |Description |
         |---|---|
         |Check method |* HTTP request check: use the HTTP or HTTPS protocol to send an HTTP GET request to the container, and confirm the container state by checking the response. You need to check the following items:<br><br>   * Protocol: Select HTTP or HTTPS.<br><br>   * Request header: custom request headers (HTTP headers) in the HTTP request. Click **Add** and enter the key and value for the request header.<br><br>   * Path: enter the access path used for health check in the business code. The default is `/` and can be modified.<br><br>   * Port: enter the App's access port. The default is 8080 and can be modified.<br><br>* TCP port check: Attempt to establish a TCP connection to the App to detect whether a connection can be established normally. You need to check the following items:<br><br>   * Port: Enter the access port for the App. The default is 8080, which can be modified. |
         |Time setting |Specify the time parameters for the check. Valid values:<br><br><br>* Initial wait time: The time to wait after the app starts before executing the first probe. The default is 1 s.<br><br>* Timeout: The amount of time that you wait for a response after you send a check request. If this time is exceeded, the app is considered unresponsive. The default is 1 s.<br><br>* Check interval: the time interval at which checks are performed. Default value: 10 seconds. |
         |Threshold setting |Configure the result threshold for the check, including:<br><br><br>* Success threshold: The number of successful responses that indicates the system runs as expected after a check request is sent. Default value: 1. This parameter cannot be specified.<br><br>* Failure threshold: The number of consecutive failed responses that indicate the system is abnormal after a check request is sent. Default value: 3. That is, if the App does not respond to the request 3 times, the application status is considered abnormal. |
         

      * Storage configuration

         Click **Add storage mount** to mount storage configuration for the App instance. Mounting multiple storage resources is supported.

         
         |Parameter |Description |
         |---|---|
         |Type |Supports **NAS mount**. |
         |File system type |Select the file system type. Supports **Extreme speed** and **Capacity type**. NAS and the VKE cluster to be deployed must be in the same VPC. |
         |Mount point |Select the **file system** and **mount point** to mount. |
         |Subdirectory |Enter the subdirectory information of the file system to be mounted. The default is the root directory `/`. |
         |Mount path |Mount to the path in the Managed App Instance. |
         

      * Custom tag/annotation

         Click **Tag** or **Annotation** to add custom tags and annotations to the App to meet more diverse business scenarios.

5. Click **Confirm**, and the App will start to deploy. You can view the deployment progress of the App on the environment tab.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After the deployment is completed, the deployment state will change to **Completed**. You can view deployed instance information on the List of instances tab. If the running state is **running**, the deployment was successful.


* To view real\-time logs, click **Real\-time log** to access the instance's real\-time log information, which facilitates operations and troubleshooting.

* To view events, click **Event** to see information about events that occurred within the last 1 hour for the instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Create Service resources for the App to enable public network or private network access. For specific operations, see [Access method](https://docs.byteplus.com/en/docs/cp/Access_methods).
