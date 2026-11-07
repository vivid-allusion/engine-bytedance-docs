---
title: "Build image and push to custom image repository"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Build_and_push_images_to_a_custom_image_repository"
---

The CP built\-in **Build image and push to custom image repository** task supports building container images using a Dockerfile and pushing them to a custom image repository (self\-built container registry or third\-party cloud provider container registry). This document provides usage instructions for this built\-in task.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

The maximum supported image size is 5 GB.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The repository address, account, and password for the image to be pushed have been prepared.

* The Dockerfile required for building has been prepared.


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select the **Build image and push to custom image repository** task template.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following describes the parameters for this built\-in task.


* **Job name**

   The default is Build image and push to custom image repository; custom job names are supported.

* **Upstream task**

   Display the name of the upstream serial task for the current task. If there is no upstream task, display as `-`.

* **Code source download policy**

   Select the code source download policy based on whether the current task requires a code source.

   * **Download code**: The current task requires downloading the code source.

   * **Do not download code**: The current task does not require a code source.

* **Steps**

   The current task includes a default predefined step (building images and pushing to a custom repository). You can add other serial steps to the current task as needed. The parameters for the default predefined step are described below.



|Parameter |Description |
|---|---|
|Step name |By default, images built are pushed to the custom repository; supports custom step names. |
|Image address |Docker image upload address, supports HTTP and HTTPS protocols.<br><br><br>* The address supports a fixed repository, for example: `xxx.com/ns/demo:1.0`.<br><br>* The address supports dynamic parameters, for example: `xxx.com/ns/demo:$(DATETIME)`. |
|Credential information |Configure access credentials for the custom repository. Click **add** on the right, then fill in **Credential information**. |
|Access credential type |Currently supports two types: service connection and username/password.<br><br><br>* Service connection: select a service that has already been integrated. For service connection setup actions, see [Service connection](https://docs.byteplus.com/en/docs/cp/Service_connection).<br><br>* Username/password: enter the address, username, and password of the custom repository.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Pulling private base images that require secondary authentication is not currently supported. To pull private base images, it is recommended to use the same Container Registry instance to store both the base image to be pulled and the image to be pushed. In this scenario, push and pull share the same account and password.</div><br> |
|contextpath |Execution context path for the docker build command. Enter the path relative to the root directory of the code; the default is `.`. |
|Dockerfile |Specify the Dockerfile to be built. Dockerfile supports the following two configuration methods.<br><br><br>* **File path**: enter the path of the Dockerfile relative to the root directory of the code repository.<br><br>* **Custom file**: enter the content of the Dockerfile in the command box.<br><br><br>When building multi\-architecture images, you need to specify the Dockerfile for each architecture separately.<br><br><br>* **Multi\-architecture build**: optional configuration. Whether to enable multi\-architecture build.<br><br>   * Disabled: by default, builds an image for the linux/amd64 architecture.<br><br>   * Enabled: you need to further check the specific image architectures you want to build. Currently supports building images for two architectures: linux/arm64 and linux/amd64. |
|Build parameters |When using the docker build command to build images, you can specify relevant build parameters to customize the image build process.<br><br>Example:<br><br><br>* Use `--target <stage name>` to specify the stage for building the image. For example, `--target hello`.<br><br>* Use `--build-arg <parameter name>=<value>` to replace the ARG value in the Dockerfile. For example, `--build-arg VERSION=1.21.3`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports common docker build parameters.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports specifying multiple build parameters as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When specifying multiple build parameters, it is recommended to write each build parameter on a separate line.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The value of a build parameter supports referencing pipeline variables.</div><br> |
|Skip certificate verification |Optional configuration. When selected, all content in the current step will no longer validate the HTTPS certificate. For example, the repository URL for pushing or pulling images will no longer validate the HTTPS certificate.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration is mainly applicable when the repository uses an untrusted self\-signed certificate. Ignoring certificate validity involves security risks and is generally not recommended.</div><br> |
|Enable cache |Cache is enabled by default to accelerate image building and address the issue of long base image pull times.<br><br><br>* Enable cache: After the first image build is complete, the system will generate a cache of the base image. During subsequent image builds, there is no need to repeatedly pull the same base image, which effectively reduces image build time.<br><br>* Disable cache: The system will append `--no-cache` to the build command. During image building, the base image will be pulled again, which takes longer. |
|Compression method |Select the image compression method. Currently, `gzip` and `zstd` are supported. |
|Skip on failure |Optional configuration.<br><br><br>* Enable: If the current step fails to run, it will be skipped directly. The remaining steps of the current task can continue to execute, and the pipeline can also continue to run.<br><br>* Disable: After the current step fails, the remaining steps of the current task will no longer execute, and the pipeline will fail to run. |



* **Task output**

   Display all artifacts output by the current task, including artifacts from all steps within the task. If there are no artifacts, display as `-`. Artifacts can be used as input for subsequent tasks.

   For the current default predefined step, the built image address `imageOutput_step-xxxx` will be output.

* **Advanced settings**

   * **Resource limits**: You can set upper limits for CPU and memory.

   * **Disk capacity limit**: You can set an upper limit for disk capacity, up to 100 GiB.

   * **Timeout**: Set the timeout for the entire task. The task will automatically fail after exceeding the timeout. A task can include multiple serial steps. The total execution time of all steps must be less than the task's timeout.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports sending task\-level messages via Webhook and Larkbot to help you stay informed about task status.

   * **Automatic fail retry**: After enabling, enter the maximum number of retries supported. When task execution fails, it will retry up to the specified number of times according to the configured maximum retries.


<span id=".5pel5b-X5Y-K5Lqn54mp"></span>
## Logs and artifacts

The following section introduces the details displayed in the pipeline after this built\-in task is completed.

On the current pipeline run details page, click the title of the card labeled "Building images and pushing to the custom image repository" to view the run log, artifacts, and task configuration information.


* Run log: Displays the real\-time run log for this task.

* Task configuration: Displays the configuration parameters for this task. For details, refer to the parameter description above.

* Artifacts: After a successful run, the process of building images and pushing them to the custom image repository will output the address of the successfully built image.
