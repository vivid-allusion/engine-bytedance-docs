---
title: "Create and deploy managed app (container image)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_app_container_image"
---

Deploy managed app using container images, not restricted by technology stack or language. This article describes how to quickly create a managed app using container images and deploy it to a Kubernetes cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The container image to be used is ready. Please prepare the image address in advance, or upload the image to the BytePlus Container Registry. For specific operations, see [Getting started with pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* The Kubernetes cluster to be deployed has been connected. For specific operations, see [Connecting deployment resources](https://docs.byteplus.com/en/docs/cp/Deploy_resource).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To deploy the app using VCI, the deployment resource must be a VKE cluster, and the <strong>vci\-virtual\-kubelet</strong> addon must be installed in the cluster in advance.   </div>
   

* (Optional) The NAS file system and mount point have been created. The NAS and the VKE cluster to be deployed must be in the same VPC. For specific operations, see [Getting started with file storage](https://docs.byteplus.com/en/docs/nas/Manual).

* (Optional) To use the IRSA authentication feature, please first complete VKE cluster creation, IAM role creation, and authorization. For operation details, see [Using IRSA capability in the cluster](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters). In the IAM role **Trust policy ** Statement, {serviceaccount} corresponds to {App ID\-sa} in CP, for example `appname-sa`.

   ```JSON
   "Condition": {
       "StringLike": {
           "oidc:aud": "sts.volcengine.com", // The fixed value of the audience in OIDC.
           "oidc:iss": "https://oidc-vke-cn-beijing.tos-cn-beijing.volces.com/ccog93v********", // Set the value to the provider URL displayed in the console after you enable the IRSA feature for your cluster.
           "oidc:sub": "system:serviceaccount:oidc-ns:oidc-sa" // Required format: system:serviceaccount:{namespace}:{serviceaccount}, where {namespace} and {serviceaccount} are the namespace and service account in the Kubernetes cluster.
        }
   },
   ```
   


<span id="6N97JWf0"></span>
## Procedure


1. Log in to the app management page.

   1. Log in to the [CP Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **Workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **App delivery \> App management**.

2. On the app management page, click **Create app**.

3. On the create app page, select **Managed app**, and fill in the relevant configuration information as required.

   1. Fill in **App information**. After completion, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |App ID |According to the interface tips, enter the App ID. The App ID is the unique logo of the App and cannot be changed after creation. |
      |App display name |Customize the application's display name. |
      |App deployment Type |In this scene, select **Container**. |
      |App technology stack |In this scene, select **Others**. |
      |Description |Enter notes for the current App. This field can be left blank. |
      |Member management |Quickly configure the members of the current App and assign different permissions to each member to meet the needs of multi\-role collaboration for App delivery.<br><br><br>* Add members: Add multiple members to the current App. Only users with visible permissions in the current workspace can be selected. The system will add the BytePlus root user (root user) and the App creator as administrators by default.<br><br>* Permission: The system provides two built\-in roles, administrator and Read only. Each member can be assigned one or more role permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not allowed to cancel the administrator permission of the root user, nor to delete the root user.</div><br> |
      

   2. Fill in **Environment configuration**. After completion, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |deployment resource |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To deploy using the VCI Method, the deployment resource must be a VKE Cluster, AND In the cluster, Install the <strong>vci\-virtual\-kubelet</strong> addon in advance.</div><br><br><br>select the actual deployment location for the App, for example, Kubernetes Cluster, cloud server, virtual machine, Physical server, and so on. Currently, only Kubernetes Cluster type deployment resource is supported. |
      |Namespace |Select the specific Namespace. Kubernetes uses Namespaces for logical isolation, allowing different groups to share Resources across the entire Cluster while still being managed separately. |
      |Environment ID |Set the unique identifier for the current environment. The default is `${App ID}-prod`, custom values are supported. After the environment ID is created successfully, modification is not supported. |
      

   3. Fill in **Basic configuration**. After completion, click **Next: Advanced settings**.

      
      |Parameter |Description |
      |---|---|
      |Deployment method |This scenario selects **image deployment**. |
      |Image selection |Set application image. Supports **CR repository image** and **custom images** methods. Please select as needed.<br><br><br>* **CR repository image**: Select container image from your BytePlus container registry. Please select the region, instance, namespace, OCI repository, and tag where the target image is located: **Region**, **Instance**, **Namespace**, **OCI repository**, **Tag**.<br><br>* **Custom images**: Directly enter the image address used by the App. The image address format is `host/namespace/repo:tag`. |
      |Image pull authentication |To Use a Private Image, turn on the Image pull authentication switch and enter the correct Container Registry username and Password. |
      |Version |Custom App version number.<br><br>You can click **Version number uses timestamp** on the right to automatically generate the version number. |
      |VCI |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select VCI Deploy application, the deployment resource must be a VKE Cluster, AND you must Install the <strong>vci\-virtual\-kubelet</strong> addon in the Cluster in advance.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">VCI does Not support Pod IRSA (IAM Roles for Service Accounts) OIDC (OpenID Connect) feature. IRSA is a security mechanism that allows applications in a VKE cluster to use BytePlus IAM roles through Kubernetes service accounts. For details about IRSA, see <a href="https://docs.byteplus.com/en/docs/vke/IRSA-overview">IRSA overview</a>.</div><br><br><br><br>Whether to Deploy application using the VCI method. Deploying application using this method does not require Management of underlying cloud servers or other infrastructure. You only need to provide the Image to run the Container and pay for the Actual Resources consumed. For Billing details, see [VCI Instructions](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview).<br><br><br>* If checked, the App will be deployed using the VCI method.<br><br>* If not checked, the App will be deployed using the standard Kubernetes method. |
      |Service specifications |Define the App's Service specifications according to business requirements, including: Number of instances, CPU and Memory specifications for each Instance. Support **Default Specifications** and **Custom specification**.<br><br><br>* Default Specifications: Support Custom Number of instances and provide common CPU and Memory combinations. Please select the appropriate combination according to business needs. In Default Specifications, CPU request = CPU limit; Memory request = Memory limit.<br><br>* Custom specification: If Default Specifications cannot meet your requirements, Custom specification is supported, including: Custom Number of instances, CPU request, CPU limit, Memory request, Memory limit. Among them, CPU request ≤ CPU limit; Memory request ≤ Memory limit.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For deployments using the VCI Method, only the upper limit for CPU and Memory needs to be defined. System will provide the closest VCI Instance specification based on the upper limit you select.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For deployments using the standard Kubernetes Method, CPU and Memory are allowed to have No limit on Resources.</div><br> |
      

   3. (Optional) Fill in **Advanced settings**.

      * Start command

      
      |Parameter |Description |
      |---|---|
      |Start method |Configure the app's start method. The following two start methods are supported. Please select as needed.<br><br><br>* **Cloud\-native command**: Specify the start command and start parameters according to business requirements. If not filled in, the app will be started according to the image ENTRYPOINT configuration.<br><br>* **Custom script**: If a series of initialization scripts need to be executed before the app starts, it is recommended to start the app by writing a custom script. |
      

      * Container permission and IAM

      
      |1 parameter |Description |
      |---|---|
      |Pod IRSA OIDC |After enabling, the IRSA (IAM Role for Service Account) mechanism is supported at the pod level. The IRSA mechanism associates a specific IAM role with a service account. This enables pods running in a VKE cluster to obtain the permissions granted to the role through the service account. In this way, the pods can access corresponding cloud service resources. For a detailed introduction to IRSA, see [IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview). |
      |IAM role |Select the IAM role associated with this App. For details about IAM role creation and authorization Actions, see [Use IRSA capability in the cluster](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters). In the IAM role **trust policy** Statement, {serviceaccount} corresponds to {App ID\-sa} in CP, for example, `appname-sa`. |
      |Credential file address |IAM credential file path, default is /var/run/secrets/iam/credential. After specifying the value, it will be automatically written into the app deployment YAML to support IRSA identity authorization. |
      

      * Environment variable

      
      |Parameter |Description |
      |---|---|
      |Environment variable |Configure environment variables as needed. The information of environment variables will be injected into the app's runtime environment to dynamically configure the application during runtime.<br><br>Click  **+ Environment variable** and enter the key and value of the environment variable. |
      

      * Health check

      The current setting is a liveness check: checks whether the Container is running. If the probe fails, the Container will be restarted.

      
      |Parameter |Description |
      |---|---|
      |Check method |* HTTP request check: Use the HTTP or HTTPS protocol to send an HTTP GET request to the Container. Pass the response to confirm the Container state. You need to check the following items:<br><br>   * Protocol: Select HTTP or HTTPS.<br><br>   * Request header: Custom request headers (HTTP Headers) in the HTTP request. Click **Add,**  then enter the key and value for the request header.<br><br>   * Path: Enter the access path in your business code for health check. Default is `/`. Modify is supported.<br><br>   * Port: Enter the access port of the App. Default is 8080. Modify is supported.<br><br>* TCP port check: Send a TCP socket to the App to detect whether a normal connection can be established. You need to check the following items:<br><br>   * Port: Enter the access port of the App. Default is 8080. Modify is supported. |
      |Time setting |Specify the time parameters for the check. Valid values:<br><br><br>* Initial wait time: Refers to the time to wait before the first probe after the app starts. The default is 1 s.<br><br>* Timeout: The amount of time that you wait for a response after you send a check request. Exceeding this time indicates the App is unresponsive. The Default is 1 s.<br><br>* Check interval: the time interval at which checks are performed. Default value: 10 seconds. |
      |Threshold setting |Configure the result threshold for the check, including:<br><br><br>* Success threshold: The number of successful responses that indicates the system runs as expected after a check request is sent. Default value: 1. This parameter cannot be specified.<br><br>* Failure threshold: The number of consecutive failed responses that indicate the system is abnormal after a check request is sent. Default value: 3. If the App does not respond to the request 3 times, the application status is considered abnormal. |
      

   * Storage configuration

      Click **add storage mount** to mount storage configuration for the current App instance. Supports mounting multiple storage.

      
      |Parameter |Description |
      |---|---|
      |Type |Currently supports **NAS mount**. |
      |File system type |Select the file system type. Support **Extreme speed** and **Capacity type**. NAS and the to be deployed VKE Cluster must be in the same VPC. |
      |Mount point |select the **File system** and **Mount point** to mount. |
      |Subdirectory |Enter the subdirectory information of the file system to be mounted. The default is the root directory `/`. |
      |Mount path |Path mounted to the managed app instance. |
      

   * Custom labels

      
      |Parameter |Description |
      |---|---|
      |Tag |App Tag (Label). After you add key\-value pairs, other resources can easily identify this App. |
      |Annotation |App annotation (Annotation). After adding annotation key\-value pairs, they can be used to store app configuration and other additional information. |
      

   * App monitoring

      Click **add storage mount** to mount storage configuration for the current App instance. Supports mounting multiple storage.

      
      |Parameter |Description |
      |---|---|
      |APMPlus |After turning on APMPlus Monitoring metrics, Support Pass Trace for link tracing to locate business link issues, and Support to view the App's related Runtime metrics. For the cost of APMPlus Monitoring Service, see [Monitor Billing Description](https://docs.byteplus.com/en/docs/cp/Product_billing). |
      |Monitor application type |Select the corresponding Monitoring Type according to your App programming language.<br><br>According to the configuration in **App information \> App technology stack**, the selectable language types are as follows:<br><br><br>* When **Java** is selected, **Java** is automatically selected.<br><br>* When **Others** is selected, **Java**, **Python**, and **Node.js** are supported. |
      |Monitor Service Name |Configure the monitoring service Name. This Name will be used as the current App Name and shown in the service list of the APMPlus server Console, making it easier to distinguish between different monitoring tasks. If this Name is not specified, the Default **App ID** will be used. |
      



&nbsp;

4. Click **confirm** to start deploying the App. You can view the App's deployment progress in the environment tab.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After deploy is complete, the deployment state will change to **Completed**. You can view the deployed instance information in the list of instances tab. A running state of **running** indicates deploy success.


* View real\-time log: Click **real\-time log** to view real\-time log information for the instance, which is helpful for operations and troubleshooting.

* View event: Click **event** to view event information that occurred within the past hour for the instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Create Service resources for the App to enable public network and private network access. For specific operations, see [Access method](https://docs.byteplus.com/en/docs/cp/Access_methods).
