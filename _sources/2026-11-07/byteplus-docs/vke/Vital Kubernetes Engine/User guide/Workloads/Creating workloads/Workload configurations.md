---
title: "Workload configurations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Workload_configurations"
---

This topic mainly describes the configuration of custom parameters for workloads such as Deployments, StatefulSets, DaemonSets, Jobs, and CronJobs. This helps you flexibly specify parameters and create workloads for different scenarios.

<span id="vim9qgBr"></span>
## Basic information


|Parameter |Description |
|---|---|
|Name |Enter the name of the workload based on the on\-screen prompts. The name must be unique within the same namespace. |
|Namespace |Select a namespace to deploy the workload in. You can select a custom namespace or a Kubernetes built\-in namespace. For a description of Kubernetes built\-in namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
|Number of instances |You can specify this parameter only for **Deployments** and **StatefulSets**.<br><br>Enter the number of pod instances for the workload. |
|Label |Enter the labels of the workload, which correspond to the label in Kubernetes. A label is a key\-value pair used to identify a workload. It helps Kubernetes quickly search for target workloads when it is used with the selector. For example, `service.istio.io/canonical-revision:latest`.<br><br>Click **Add new**, and enter the **key** and **value** based on the on\-screen prompts. |
|Annotation |Enter the annotation of the workload, which corresponds to the annotation in Kubernetes. It is primarily used to record additional information about application deployment, security policy, and scheduling policy. It is not used to identify or distinguish resources.<br><br>Click **Add annotation**, and enter the **key** and **value** based on the on\-screen prompts. |
|Computing power type |Only **Deployments**, **StatefulSets**, **Jobs**, and **CronJobs** in managed clusters support this parameter.<br><br>Select infrastructure resources where the workload is deployed. Valid values:<br><br><br>* **Elastic Compute Service instance**: The workload is deployed on Elastic Compute Service (ECS) nodes in the cluster.<br><br>* **Vital Container Instance**: The workload is deployed on Vital Container Instances (VCIs), which are virtual node in the cluster. For an introduction to VCI, see [What is VCI](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance)? |
|Synchronize time zone |After you enable this feature, the container uses the local time zone of the node, which is the Central Standard Time (CST) time zone. |
|Log collection |This parameter is displayed after you select **Vital Container Instance** for the **Computing power** type parameter. You need to enable this feature to collect VCI logs. For detailed instructions, see [Collecting VCI logs by using TLS](https://docs.byteplus.com/en/docs/vke/Collecting-VCI-container-logs-using-Torch-Log-Service). |


<span id="mQfdvfgR"></span>
## Container configuration

<span id="Judx4MEO"></span>
### Basic information


|Parameter |Description |
|---|---|
|Container name |Enter a container name based on the displayed naming rules. The container name must be unique under the same workload. |
|Container image |Select the image used by the container. You can use a third\-party image or an image from Container Registry (CR).<br><br><br>* Third\-party image: Enter the URL of a third\-party container registry, which includes the image tag, such as `example.com/namespace/repository:v1`.<br><br>* Image in CR: Click **Choose your own image**. In the panel that appears on the right side, select an image of the target CR instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to use a private image in CR, install the cr\-credential\-controller secret\-free add\-on first. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller">Using a secret\-free add\-on to pull private images to create workloads</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not use the cr\-credential\-controller secret\-free add\-on to pull private images, you need to configure the <strong>image key</strong>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you use images from a CR Standard Edition instance for which the access control permissions on the Virtual Private Cloud (VPC) of the current cluster are not granted, you need to configure the permissions based on the on\-screen prompts. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account">Connecting to the VPC of the current account</a>.   </div><br>    |
|Image tag |Select the version of the image. If you do not select a version, the `latest` version is pulled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If no image of the <code>latest</code> version exists, you need to enter or select a specific image tag.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you use a third\-party image, you do not need to specify this parameter.</div><br> |
|Image pull policy |Select a policy for pulling container images. Valid values:<br><br><br>* **Default policy**: Use the system default policy. The descriptions of the default policy are as follows:<br><br>   * When the AlwaysPullImages add\-on is disabled for the kube\-apiserver of the current cluster:<br><br>      * If **Image tag** is not specified or is set to `latest`, the image pull policy is set to **Always** by default.<br><br>      * If **Image tag** is specified and is not set to `latest`, the image pull policy is set to **IfNotPresent** by default.<br><br>   * When the AlwaysPullImages add\-on is enabled for the kube\-apiserver of the current cluster, the image pull policy is set to **Always** by default, and other policies will not take effect even if selected.<br><br>* **Always**: Always pull images.<br><br>* **IfNotPresent**: Prefer to use local images.<br><br>* **Never**: Use only local images. |
|Image key |This feature is not enabled by default. After you enable this feature, you need to configure a CR key. Select an existing repository key or click **Create repository key**. In the VKE console, add the CR key based on the following descriptions.<br><br><br>* **Name**: The repository name of the image used by the container. For example, if you use an image from CR, enter the name of the Open Container Initiative (OCI) artifact repository where the image is located.<br><br>* **Container Registry domain name**: Enter the CR domain name, for example, `cr-cn-beijing.volces.com`.<br><br>* **Username**: Enter the username used to log in to CR. For example, if you use an image from CR, enter the username for logging in to the instance where the image is located. You can obtain the username on the **Overview** page of the target instance in [CR console](https://console.byteplus.com/cr).<br><br>* **Password**: The password that corresponds to the username for logging in to CR.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to specify this parameter if you do not use the secret\-free add\-on and need to pull a private image.</div><br> |
|Full\-chain Application Performance Management |Select **Enable** to enable the workload application performance monitoring feature and specify the related parameters. For more configuration details, see [APMPlus](https://docs.byteplus.com/en/docs/vke/Application_performance_observability).<br><br><br>* **Monitor application type**: Select the type of monitored application. **Java**, **Python**, and **NodeJs** are supported.<br><br>* **Monitor Service Name**: (Optional) Specify the name of the monitoring service. This name will be used as the monitoring task name for the current workload and will be displayed in the service list of the APMPlus console. This makes it easier for you to distinguish between different monitoring tasks.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify the Monitor Service Name parameter, the system will use the workload name as the monitoring service name.</div><br> |
|ResourceQuota |You can configure the upper and lower limits for CPU and memory at the container level based on your business requirements to ensure the normal operation of containers. If you do not specify this parameter, it indicates that the container ResourceQuota is not limited.<br><br><br>* **CPU request**: The minimum CPU that a container requires.<br><br>* **CPU limit**: The maximum CPU that can be allocated to a container. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Memory request**: The minimum memory that a container requires.<br><br>* **Memory limit**: The maximum memory that can be allocated to a container. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **GPU resource type**: You can configure GPU resources only for clusters with GPU\-accelerated nodes. Two types of GPU resources are available.<br><br>   * **Nvidia**: Use NVIDIA GPU resources. Enter the NVIDIA **GPU computing power** and **Graphics card type** that you need to use based on the on\-screen prompts. For detailed descriptions, see [NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling).<br><br>      This feature depends on the nvidia\-device\-plugin add\-on. If the add\-on is not installed, install it based on the on\-screen prompts.<br><br>   * **mGPU**: Use GPU resources shared among containers. Enter the required **GPU computing power**, **GPU memory**, and **Graphics card type** shared among containers based on the on\-screen prompts. For a detailed description, see [Container shared GPU scheduling](https://docs.byteplus.com/en/docs/vke/mGPU-overview).<br><br>      This feature depends on the mgpu add\-on. If the add\-on is not installed, install it based on the on\-screen prompts.<br><br>* **Number of RDMA cards**: [[Beta·Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Enable pod containers to use RDMA devices. We recommend that you configure two or four cards. For detailed operations, see [Using RDMA resources in VKE clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select only one type of GPU resource in a single workload.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">RDMA and mGPU cannot be used at the same time.</div><br> |
|Privileged container |This feature is disabled by default. After you enable the feature, privileged containers can access devices on the host. Containers deployed on Linux systems can control the network stack or access devices. |
|Init container |This feature is not enabled by default. After you enable the feature, this container will be set as an init container. Init containers are containers that run before application containers in a pod. Init containers can include tools, such as python and dig, and code used only during the installation process. This prevents redundant deployment in application containers and enhances the security of application images.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Init containers do not support setting post\-start processing and pre\-stop processing in lifecycle management, and do not support enabling health checks.</div><br> |
|Stdin |You can specify this parameter only for **Deployments** and **StatefulSets**.<br><br>After this feature is enabled, a buffer is allocated for the standard input (Stdin) of the container during the runtime of the container. |
|TTY |You can specify this parameter only for **Deployments** and **StatefulSets**.<br><br>After you enable this feature, a terminal is allocated to the container, and Stdin needs to be selected. |


<span id="7oGjKb9a"></span>
### Container port

Click **Add port**, and configure the port that the application in the container uses to connect to services outside the container based on the on\-screen prompts. The configuration items include the supported protocol, such as TCP and UDP, port number, and port name. For example, Nginx listens on TCP port 80 with the port name `nginx`.

<span id="gXp2YT5N"></span>
### Environment variables

Click **Add environment variables** to configure environment variables. When Kubernetes creates a pod, it injects environment variable information into the container.


|Parameter |Description |
|---|---|
|Custom |You can enter variable names and variable values to create custom environment variables. |
|ConfigMap |You can reference part or all of the variables in a ConfigMap. When you reference part of the variables, you can create one environment variable for a single key of a rule. |
|Secret |You can reference part or all of the variables in a secret. When you reference part of the variables, you can create one environment variable for a single key of a rule. |
|Instance field |You can reference the values of instance fields to create environment variables.<br><br><br>* **metadata.name**: the name of the workload<br><br>* **metadata.namespace**: the namespace where the workload resides<br><br>* **metadata.labels**: the labels of the workload<br><br>* **metadata.annotations**: the annotations of the workload<br><br>* **spec.nodeName**: the node where the workload is located<br><br>* **spec.serviceAccountName**: the used service account<br><br>* **status.hostIP**: the IP address of the node where the workload is located<br><br>* **status.podIP**: the IPv4 address of the pod in the workload<br><br>* **status.podIPs**: the IPv4 and IPv6 addresses of the pod in the workload |
|Container resources |You can reference the fields of the container as environment variables.<br><br><br>* **limits.cpu**: the upper limit of the container CPU usage<br><br>* **limits.memory**: the upper limit of container memory usage<br><br>* **requests.cpu**: the size of the container CPU request<br><br>* **requests.memory**: the size of the container memory request |


<span id="BnoPDxzh"></span>
### Storage configuration

Storing data in a container involves two steps. First, add a volume in the pod and then mount the volume to the container.


* Add a volume: Click **Add volume** to add a data volume. A volume is the location where data is stored in a container. Before allocating storage resources for a type of data, first specify the directory for the data to be stored in the container.

   
   |Parameter |Description |
   |---|---|
   |ConfigMap |You can create data volumes for all or part of the data in a ConfigMap. When you create PersistentVolumes (PV) for part of the data, you can configure multiple data items, which need to be separated by semicolons (;). For example, `cm1:path1;cm2:path2`. |
   |Secret |You can mount part or all of the data in a secret. When you create PVs for part of the data, you can configure multiple data items, which need to be separated by semicolons (;). For example, `cm1:path1;cm2:path2`. |
   |PersistentVolumeClaim |Select a created PersistentVolumeClaim (PVC) in the current workload namespace, and specify a data volume name. |
   |Temporary directory |Create a data volume name for the temporary directory. |
   |Host directory |Create a data volume for a directory in the host. |
   

* Mount the volume: Click **Add mount volume** to allocate storage resources for the created volume and grant read and write permissions. The configuration items are as follows:

   
   |Action |Description |
   |---|---|
   |Select a data volume |Select the data volume named in the **Add volume** step. |
   |Specify a mount path |Select the container path to which storage should be mounted. |
   |Select the path on the volume for mounting |* **subPath**: A subdirectory of the mounted volume. Specify a subdirectory of the mounted volume. If you leave it empty, the subdirectory mounting is not used.<br><br>* **subPathExpr**: Extended path of the mounted volume. Enter an extended path of the mounted volume. If you leave it empty, the extended path will not be used. |
   |Assign read/write permissions |Define the read and write restrictions for the path of the mounted volume. |
   


<span id="C2NkPEnK"></span>
### Life cycle

When a container is created, commands to execute before and after the container starts can be automatically injected. The specified commands and parameters are saved to the configuration file. The commands and parameters from the configuration file will overwrite the corresponding ones in the container image if duplicates exist.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">The following table describes lifecycle\-related parameters. Each command or parameter must be entered in a separate text box. Click <strong>Add</strong> to enter a command.</div>



|Parameter |Description |
|---|---|
|Run command |Enter the command to run before the container starts. |
|Run parameter |Enter the parameters of the command to run before the container starts. |
|Post\-startup processing |Enter the command to run after startup. |
|Pre\-stop processing |Enter a pre\-stop processing command. |


<span id="8fcIt21T"></span>
### Health check

You can specify the **Liveness check**, **Ready check**, and **Start check** parameters. You can use HTTP, TCP, or command execution to determine whether the application in the container is running properly.The following table provides an example of how to specify the Liveness check parameter.


|Parameter |Description |
|---|---|
|Check method |Select a check method. Valid values:<br><br><br>* **HTTP request check**: Use HTTP or HTTPS to send an HTTP GET request to the container, and confirm the container status by checking the response. You need to check the following items:<br><br>   * **Protocol**: Select HTTP or HTTPS.<br><br>   * **HTTP request header**: Enter a custom request header in the HTTP request. Click **Add** to enter a key\-value pair.<br><br>   * **Path**: Enter the path for accessing the HTTP server.<br><br>   * **Port**: Enter the access port number or port name exposed by the container.<br><br>* **TCP port check**: A TCP socket is sent to the container. The Kubelet will attempt to open the socket on the specified port. If a connection can be established, the container is deemed healthy. Otherwise, it is deemed abnormal. You need to check the following items:<br><br>   * **Port**: Enter the access port number or port name exposed by the container.<br><br>* **Command check**: Execute the specified command in the container and confirm the container status by examining the command result. You need to check the following items:<br><br>   * **Command**: Enter the command to check the container health status.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You need to enter each command in a separate text box. Click <strong>Add</strong> to add a text box.      </div><br>      <br><br>* **gRPC request check**: Use gRPC to check the health status of the server application by sending POST or GET requests.<br><br>   * **Service**: Enter a health check method. Valid values: POST and GET. |
|Time setting |Specify the time parameters for the check. Valid values:<br><br><br>* Initial wait: The amount of time that you need to wait after the container starts before the first check is performed. Default value: 1 second.<br><br>* Timeout: The amount of time that you wait for a response after you send a check request. If this period is exceeded, the container is deemed unresponsive. Default value: 1 second.<br><br>* Check interval: the time interval at which checks are performed. Default value: 10 seconds. |
|Threshold setting |Configure the check result threshold. The following information is included:<br><br><br>* Success threshold: The number of successful responses that indicates the system runs as expected after a check request is sent. Default value: 1. This parameter cannot be specified.<br><br>* Failure threshold: The number of consecutive failed responses that indicate the system is abnormal after a check request is sent. Default value: 3. If the container fails to respond to a request three times, the container is deemed abnormal. |


<span id="xvmXQEJL"></span>
## Advanced settings

<span id="nSMJTaOE"></span>
### Headless service

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify this parameter only for <strong>StatefulSets</strong></div>



|Parameter |Description |
|---|---|
|Name |Specify the name of the headless service. A headless service can interact with other service discovery mechanisms without being tied to the Kubernetes implementation. The platform does not provide load balancing or routing for a headless service. |
|Port |Specify the port number for the service running on TCP or UDP. Multiple port numbers can be configured. |


<span id="7ungQber"></span>
### Repeat regularly

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify this parameter only for <strong>CronJobs</strong>.</div>



|Parameter |Description |
|---|---|
|Cron expressions |A Cron expression is a string made of five fields separated by spaces. The fields include minutes, hours, dates, months, and weeks.<br><br>For detailed Cron expression usage, see [Cron expressions](https://docs.byteplus.com/en/docs/vke/Cron-expressions). |
|Number of successful Jobs retained |The number of retained records for executed Jobs. |
|Number of failed Jobs retained |The number of retained records for failed Jobs. |
|Concurrency policy |The policy for handling concurrent Job executions.<br><br><br>* **Allow**: Multiple Jobs can run simultaneously. When a new Job is triggered and the previous Job is still running, both Jobs will run simultaneously.<br><br>* **Forbid**: Multiple Jobs cannot run simultaneously. When a new Job is triggered and the previous Job is still running, the new Job will not start.<br><br>* **Replace**: Multiple Jobs cannot run simultaneously. When a new Job is triggered and the previous Job is still running, the new Job will replace the running Job. |


<span id="7ungQber"></span>
### Running policy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify this parameter only for <strong>Jobs</strong> and <strong>CronJobs</strong>.</div>



|Parameter |Description |
|---|---|
|Number of successful runs |Specify the number of times that pods need to run as expected in the Job. |
|Parallel number |Specify the maximum number of pods running concurrently. |
|Maximum timeout |Specify the maximum execution duration of the Job. |
|Number of retries |Specify the number of retries after the Job fails. |
|Restart policy |Configure the pod restart policy. Valid values: Never and OnFailure. |


<span id="OSBhCWnn"></span>
### VCI specification configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only workloads in a managed cluster and with <strong>Computing power type</strong> set to <strong>Vital Container Instance</strong> in the <strong>Basic information</strong> step require VCI specification settings.</div>



|Parameter |Description |
|---|---|
|Instance family type |Select a type of VCI instance families. You can create a workload by using the specifications of the **system default instance family** or the specifications of a custom **instance family**. |
|Instance family |This parameter is required if you select **Specify instance family**. Select one or more specific VCI instance families and corresponding instance specifications. For related information, see [VCI instance types](https://docs.byteplus.com/en/docs/vke/VCI-instance-types). |
|Number of instances |The number of pod instances in the workload, which are used to validate the available VCI ResourceQuota and inventory for the workload.<br><br><br>* For Deployments and StatefulSets, the value of this parameter is consistent with that of the **Number of instances** parameter set in the **Basic information** step, and any changes to one will be synchronized with the other.<br><br>* For Jobs and CronJobs, the value of this parameter is consistent with that of the **Parallel number** parameter set in the **Running policy** section in the **Advanced configurations** step and cannot be modified. |
|Pod subnets |Configure the VCI subnet. Valid values:<br><br><br>* **Cluster pod subnet**: Use the pod subnet of the cluster as the VCI subnet.<br><br>* **Specify pod subnet**: Specify a custom VCI subnet. If you select this option, you need to specify the **Availability zone** and **Select subnet** parameters. |


<span id="ADogSOLG"></span>
### Instance configuration


|Parameter |Description |
|---|---|
|Image cache |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] This parameter is displayed if you set the **Computing power** type parameter to **Vital Container Instance** in the **Basic information** step.<br><br>The system displays whether the image has been cached based on the **container image** that you select.<br><br><br>* **Image Cache not matched**: indicates that the container image selected in the previous step has not been cached. You can click **Create Image Cache** to create an image cache for the selected container image. For parameter configuration details, see [Creating VCIs by using manual image caches](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache).<br><br>* **Image Cache acceleration available**: indicates that the container image selected in the previous step has been cached. This can reduce image download time and accelerate container startup when you create the current workload. For information about image caches, see [Image caches](https://docs.byteplus.com/en/docs/vke/Image-Cache). |
|Elegant exit |You can specify this parameter only for **Deployments**, **StatefulSets**, and **DaemonSets**.<br><br>The grace period refers to the buffer period before an instance is terminated. Default value: 30 seconds. When the value is set to 0, it indicates that the instance is immediately deleted. |
|Update policy |You can specify this parameter only for **Deployments**, **StatefulSets**, and **DaemonSets**.<br><br>Configure the instance update policy. Valid values:<br><br><br>* **Rolling update**: During the rolling update, new instances gradually replace old instances. During the upgrade process, business traffic is load balanced across both old and new instances, which ensures business continuity.<br><br>* **Re\-create**: The old instances of the workload will be deleted first, and then the specified new instances will be installed. Business operations will be interrupted during the upgrade. |
|Maximum unavailable |This parameter needs to be specified only when the workload type is **Deployment** or **DaemonSet** and the **Rolling update** policy is selected.<br><br>Specify the minimum number of available instances (pods) in the workload during the **rolling update** scale\-in process. You can specify the maximum proportion or maximum number of unavailable pods. When you specify a proportion, the calculation result is converted to an absolute value, and the decimal part is removed. **Maximum unavailable** and **Maximum excess** cannot both be set to 0. |
|Maximum excess |This parameter needs to be specified only when the workload type is **Deployment** and the **Rolling update** policy is selected.<br><br>Specify the maximum number of available instances (pods) in the workload during the **rolling update** process. You can specify the maximum proportion or maximum number of pods. When you specify a proportion, the calculation result is converted to an absolute value, and the decimal part is removed. **Maximum unavailable** and **Maximum excess** cannot both be set to 0. |
|Instance label |Add labels to pods, which can help Kubernetes search for target pods when used with label selectors. Click **Add instance label** and enter a **key**\-**value** pair that complies with the on\-screen requirements. |
|Instance annotation |Enter annotations for pods. Click **Add instance annotations** and then enter a **key**\-**value** pair that complies with the on\-screen requirements. The annotations in Kubernetes are primarily used to record additional information about application deployment, security policy, and scheduling policy. They are not used to identify or distinguish resources. |
|DNS policy |Configure the Domain Name System (DNS) policy of the instance. Valid values:<br><br><br>* **ClusterFirst**: In this mode, the information about Kube\-dns or CoreDNS is used as preset parameters and written into the DNS configurations of the pods.<br><br>* **Default**: In this mode, the DNS configurations of the host apply to the pods. This means the DNS configurations of the pods are the same as those of the host.<br><br>* **ClusterFirstWithHostNet**: In this mode, both the DNS configurations of the host and Kube\-dns are used as the default DNS configurations of pods.<br><br>* **None**: In this mode, Kubernetes does not preload any logic for pods to determine the DNS configurations. |


<span id="31ecycUL"></span>
### Others

Workloads can be **run as non\-root users**. If you enable **Run as a non\-root user**, the specified container must be run as a non\-`root` user. Otherwise, the container would fail to start.
