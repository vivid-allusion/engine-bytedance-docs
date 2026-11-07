---
title: "Building images and pushing to Container Registry service"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Building_and_pushing_images_to_the_image_repository_service"
---

CP provides a built\-in **Building images and pushing to Container Registry service** task, which supports building container images via Dockerfile and pushing them to BytePlus Container Registry. This article provides usage instructions for this built\-in task.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

The maximum size for built images is ≤ 5 GB.

<span id="hiXySZ2z"></span>
## Prerequisites


* A Container Registry instance has been created. For specific operations, please see [Create Standard Edition instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* A target namespace has been created in the Container Registry. For specific operations, please see [Create namespace ](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

* The required Dockerfile for building has been prepared.

* (Optional) To specify a cache file for image loading, the cache file must be in tarball format with the suffix `.tar`.


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select the job template **Pushing Built Images to the Container Registry Service**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Description

The following describes the parameters for this built\-in task.


* **Job name**

   The default is Building images and pushing to Container Registry. Custom job names are supported.

* **Upstream task**

   Displays the name of the upstream serial task for the current task. If there is no upstream task, displays `-`.

* **Code source download policy**

   Select the code source download policy based on whether the current task needs to use the code source.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes a default predefined step (Building images and pushing to Container Registry service). Supports adding other serial steps to the current task as needed. The following describes the parameters for this default predefined step.

   
   |Parameter |Description |
   |---|---|
   |Step name |By default, image builds are pushed to the Container Registry Service, and custom step names are supported. |
   |Region |Select the region where the container registry to push is located.<br><br>For currently supported regions, please see [Service region for container registry](https://docs.byteplus.com/en/docs/cr/Region).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Due to network impact, using the public resource pool to push to the Johor region may take longer. It is recommended to switch to the private resource pool to push tasks to Johor.</div><br> |
   |Container Registry instance |Select the target Container Registry instance to push to. Supports pushing to Trial Edition instances and Standard Edition instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Basic edition instance of the BytePlus Container Registry has been renamed to Trial Edition instance. To ensure service compatibility, existing users can still select the <strong>cr\-basic</strong> Basic edition instance. In this case, your image will actually be pushed to the repository with the same name in the Trial Edition instance.</div><br> |
   |Repository Domain Name |Select the domain name used by this Container Registry instance. |
   |Namespace |Configure the target namespace to push to. Supports selecting or directly entering the namespace name.<br><br>When entering directly, supports using the variable `$(parameters.变量名)` to dynamically set the namespace.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The namespace must already exist; otherwise, the push will fail and return the error 401 Unauthorized.</div><br> |
   |OCI Artifact Repository |Configure the target repository to push to. Support selecting or directly entering the OCI artifact repository name.<br><br>When entering directly, supports using the variable `$(parameters.变量名)` to dynamically set the OCI artifact repository. If the OCI artifact repository does not exist, the system will automatically create it. |
   |Image tag |Custom image tag number.<br><br><br>* Support entering a fixed value, such as v1.0.<br><br>* Supports using custom variables `$(parameters.变量名)` to dynamically set the version number.<br><br>* Supports using the system built\-in variable timestamp `$(DATETIME)` to enable dynamic changes to the version number.<br><br><br>The above three types can be used in combination, such as `test-$(parameters.变量名)`, `$(parameters.变量名)_$(DATETIME)`. |
   |Nydus conversion<br><br> |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only the step <strong>Building images Push to Container Registry Service version 5.0</strong> supports the Nydus conversion feature for images. To use this feature, please add the version 5.0 step in the task's <strong>Step \> Add \> Image \> Building images Push to Container Registry Service</strong> section<strong>.</strong></div><br><br><br>After turning on the Nydus conversion feature for images, the target image pushed to the container registry will automatically generate an accelerated image replica in Nydus format. Using the accelerated image in the Nydus format can effectively reduce container startup time and improve service development efficiency. |
   |Credential information |Configure the access credentials for the Container Registry. Click **add** on the right, and fill in the **Credential information**. |
   |Access credential type |Currently, two types are supported: service connection and username/password.<br><br><br>* Service connection: Select a service that has already been connected. For actions to connect a service, see [Service connection](https://docs.byteplus.com/en/docs/cp/Service_connection).<br><br>* Username/password: Enter the address, username, and password of the container registry. |
   |contextpath |docker build command execution context path. Enter the path relative to the code root directory. The default is `.`. |
   |Dockerfile |Specify the Dockerfile to be built. Dockerfile supports the following two configuration methods.<br><br><br>* **File path**: Enter the path of the Dockerfile relative to the root directory of the code repository.<br><br>* **Custom file**: Enter the content of the Dockerfile in the command box.<br><br><br>If you choose to build multi\-architecture images, you need to specify the Dockerfile for each architecture separately.<br><br><br>* **Multi\-architecture build**: Optional configuration. Whether to turn on multi\-architecture build.<br><br>   * Turn off: The image for the linux/amd64 architecture will be built by default.<br><br>   * Turn on: You need to further select the specific image architectures you want to build. Currently, building images for linux/arm64 and linux/amd64 architectures is supported. |
   |Build parameter |When using the docker build command to build images, supports specifying relevant build parameters to customize the image build process.<br><br>Example scenario:<br><br><br>* Use `--target <stage名称>` to specify the stage for building images. For example `--target hello`.<br><br>* Use `--build-arg <参数名>=<值>` to replace the ARG value in the Dockerfile. For example `--build-arg VERSION=1.21.3`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports common parameters for docker build.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports specifying multiple build parameters as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When specifying multiple build parameters, it is recommended to write each parameter on a separate line.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The value of build parameters supports referencing pipeline variables.</div><br> |
   |Ignore certificate validity |Optional configuration. After checking, all content in the current step will no longer validate the HTTPS certificate. For example: The repository URL for pushing or pulling images will no longer validate the HTTPS certificate.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration is mainly applicable when the repository uses an untrusted self\-signed certificate. Skipping certificate verification involves security risks and is generally not recommended.</div><br> |
   |Turn on cache |Turning on caching helps accelerate building images and shortens the time to pull base images.<br><br><br>* Turn on caching: After the first image build is complete, the system will generate a cache of the base image. During subsequent image builds, there is no need to repeat pulling the same base image, which can effectively reduce the time required for building images.<br><br>   * Default: The cache from the previous build is loaded by default for each build.<br><br>   * Custom: Download and load the cache from the specified URL. The cache file must be in tarball format, with the suffix `.tar `.<br><br>* Turn off cache: The System will append `--no-cache` to the build command. During the image build process, the base Image will be pulled again, which takes a longer time. |
   |Compression method |Select the image compression method. Currently, supports `gzip` and `zstd`. |
   |Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current step fails, it will be skipped. The remaining steps in the current task can continue to execute, and the pipeline can also continue to run.<br><br>* Turn off: After the current step fails, the remaining steps in the current task will not be executed, and the pipeline will fail. |
   

* **Task output**

   Displays all artifacts output by the current task, including artifacts from all steps under the current task. If there are no artifacts, displays `-`. Artifacts can be used as input for subsequent tasks.

   For the current default built\-in steps, the output will be the built image address `imageOutput_step-xxxx`.

* **Advanced settings**

   * **LimitRange**: Support settings for the upper limits of CPU and memory.

   * **Disk capacity limit**: Support settings for the upper limit of disk capacity, up to 100 GiB.

   * **Timeout time**: Set the timeout time for the entire task. The task will automatically fail after a timeout. A task can include multiple serial steps, and the total execution time of all steps must be less than the task's timeout time.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Support pushing task\-level messages via Webhook and Feishu bot, helping you stay informed of task updates in a timely manner.

   * **Automatic fail retry**: After turning on, enter the maximum number of retries supported. When a task execution fails, it will retry up to the configured maximum number of retries.


<span id=".5pel5b-X5Y-K5Lqn54mp"></span>
## Log and artifacts

The following introduces the details shown in the pipeline after this built\-in task completes.

On the run details page of the current pipeline, click the title of the Building images and Push to Container Registry Service card to view the run log, artifacts, and task configuration information.


* Run log: Show the run log of this task in real time.

* Task configuration: Show the configuration parameters of this task. For details, refer to the parameter description above.

* Artifacts: After a successful run, Building images and Push to Container Registry Service will output the image address of the successfully built image.
