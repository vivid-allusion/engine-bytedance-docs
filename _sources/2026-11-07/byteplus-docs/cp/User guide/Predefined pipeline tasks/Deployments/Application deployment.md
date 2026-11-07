---
title: "Application deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Application_deployment"
---

The Code Pipeline preconfigured **application deployment** task enables the pipeline to trigger application deployment in the application delivery module, achieving integration between the pipeline and the application delivery module. This article explains how to use application deployment tasks.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

By orchestrating **compile and build \> image build and push to image repository \> application deployment** tasks in the pipeline, you can implement the entire process from source code compilation and building, image creation and repository push, to application deployment.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An application has been created in the application delivery module, and application initialization has been completed. For detailed instructions, see [Application Delivery Quick Start (v2)](https://docs.byteplus.com/en/docs/cp/Quick_start_for_application_delivery).

* If you use a custom image, please prepare in advance the address of the target image to be deployed.

* Caution: If the target image is a private image, make sure to set up the credentials or configure passwordless components in advance when deploying the cluster. When configuring container services, you can refer to [secrets dictionary configuration](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret) and [passwordless component configuration](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2).


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add a task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Task template selection: **Application Deployment**

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter descriptions


|Configuration Item |Descriptions |
|---|---|
|Task name |The default is application deployment. Custom task names are supported. |
|Upstream tasks |Display the names of upstream serial tasks for the current task. Shown when there is no upstream task`-`。 |
|Application type |Select the type of application to deploy. Supports **K8s YAML application**, **OAM application**, and **managed application**. The following sections will introduce the configuration items for each application separately. |
|Deployment plans |Currently, only the **native deployment** strategy is supported. |
|Timeout duration |Set the automatic timeout period. If the task runs longer than the specified time, the deployment is considered failed, and the system automatically triggers a rollback to the version before the upgrade.<br><br>Default is 300 s. Range: 1 to 7200 s. |
|Task output |Display the current task artifacts. Displayed when empty`-`。 |
|Advanced settings |**Webhook notification**: Send task notifications via Webhook, so you can stay up to date with task activity. |


<span id=".azhzLXlhbWwt5bqU55So"></span>
### K8s YAML application


|Configuration Item |Descriptions |
|---|---|
|application |Set the K8s YAML application to be deployed; you can select it from a dropdown list or enter its Application ID.<br><br><br>* Dropdown: Displays all K8s YAML applications under the current workspace (provided that application initialization has been completed).<br><br>* Enter: Supports manual entry of K8s YAML Application ID. When entering the Application ID, you can reference pipeline variables.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the Application ID does not exist, the pipeline will fail to run.</div><br> |
|environment |Set the environment to be deployed by selecting from the dropdown or entering the Environment ID.<br><br><br>* Dropdown: Displays all environment instances for the current application after environment initialization is complete.<br><br>* Supports manual entry of Environment ID. You can reference pipeline variables when entering the Environment ID.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The absence of the Environment ID will cause the pipeline to fail.</div><br> |
|artifact |Set the artifact to be deployed. For K8s YAML applications, the artifact is the container image.<br><br><br>* **Artifact name**: In a K8s YAML application, the artifact name serves as a placeholder for the image, for example, backend. The system will automatically assemble the components as AppDeliver.Image.backend. During deployment, it will replace the image placeholder and provide the specific artifact.<br><br>   * When both the application and environment are selected, the system will automatically obtain the artifact quantity and artifact name.<br><br>   * When there is input in the application or environment, you must manually add artifacts. Multiple artifacts are supported. When entering the artifact name, you can reference pipeline variables.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the specified artifact name does not exist or is incorrect, the artifact may not be replaced correctly during this deployment, which can result in deployment failure or an outcome that does not meet deployment expectations.</div><br><br><br><br>* **Artifact source**: Supports two artifact sources: upstream and custom.<br><br>   * **Upstream artifact**: Select this option when the image to be deployed originates from the artifact of an upstream task. For example, in pipeline orchestration **compile and build \> image build and push to image repository \> application deployment** tasks, the image used is the output artifact from the upstream image build task.<br><br>   * **Custom**: If you have already prepared the image, select this option and enter the full image address. The image address format is `host/namespace/repo:tag`. When you enter the image address, you can reference pipeline variables. |
|Deployment YAML file |When application, environment, and artifact are all selected, display the application's deployment YAML.<br><br>Click **view details** to view the application's YAML details and confirm whether the application configuration meets expectations. |


<span id=".b2FtLeW6lOeUqA=="></span>
### OAM application


|Configuration Item |Descriptions |
|---|---|
|application |Set the OAM application to be deployed. You can select from a dropdown or enter the Application ID.<br><br><br>* Dropdown menu: Displays all OAM applications in the current workspace after application initialization is complete.<br><br>* Input: Supports manual entry of the OAM Application ID. When entering the Application ID, pipeline variables can be referenced.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The absence of the Application ID will cause the pipeline to fail.</div><br> |
|environment |Set the environment to be deployed by selecting from the dropdown or entering the Environment ID.<br><br><br>* Dropdown menu: Shows all environment instances for the current application after environment initialization is complete.<br><br>* Input: Supports manual input of Environment ID. When entering the Environment ID, referencing pipeline variables is supported.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The absence of an Environment ID will cause the pipeline to fail to run.</div><br> |
|artifact |Set artifacts to deploy. For OAM applications, an artifact refers to the container image of each component.<br><br><br>* **Component name**: The component name for which artifact information must be provided, for example, deployment.<br><br>* **Artifact name**: In an OAM application, the artifact name is a placeholder for the image used by a component, for example, backend. The system automatically forms the string "AppDeliver.Image.backend" by concatenation. During deployment, the image placeholder is replaced and the specific artifact is passed in.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When both the application and environment are selected, the system will automatically obtain the number and names of the components that require artifact information, as well as the artifact names.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When input is present in the application or environment, you must add artifacts manually. Adding multiple artifacts is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When entering a component name, you can reference pipeline variables. If the specified component name does not exist or is incorrect, the artifact may not be correctly replaced during this deployment, which may result in deployment failure or the deployment not meeting expectations.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can reference pipeline variables when entering the artifact name. If the artifact name provided does not exist or is incorrect, the artifact may not be properly replaced during this deployment, which can result in deployment failure or failure to meet deployment expectations.</div><br><br><br>* **Artifact sources**: Supports two methods: upstream artifacts and custom artifacts.<br><br>   * **Upstream artifact**: Select this option when the image to be deployed originates from the output of an upstream task. For example, in pipeline orchestration **compile and build \> image build and push to image repository \> application deployment** tasks, the image used for deployment is selected from the output of the upstream image build task.<br><br>   * **Custom**: If you have already prepared the image, select this option and enter the full address of the image. The image address format is `host/namespace/repo:tag`. When you enter the image address, you can reference pipeline variables. |


<span id=".5omY566h5bqU55So"></span>
### Managed application


|Configuration Item |Descriptions |
|---|---|
|application |Set the managed application to be deployed. You can select it from a dropdown or enter the Application ID.<br><br><br>* Dropdown menu: Displays all managed applications in the current workspace (requires application initialization to be completed).<br><br>* Input: Allows manual entry of the managed Application ID. When entering the Application ID, you can reference pipeline variables.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the Application ID is missing, the pipeline will fail to run.</div><br> |
|environment |Set the environment to be deployed.<br><br>A managed application can currently be associated with only one environment instance. When the application is set to select, the system automatically obtains the Environment ID; when the application is set to enter, environment information is not displayed. |
|Application technology stacks |Support **Java** and **other** languages.<br><br>When the application is selected, the system automatically obtains the application technology stack. When the application is entered, you must manually select the application technology stack. |
|Version number |Customize the application's version number.<br><br><br>* Support referencing pipeline variables.<br><br>* You can click **Use timestamp as version number** on the right to automatically generate a version number. |
|artifact |Set the artifacts to be deployed<br><br><br>* For Java managed applications, use binary package deployment. Artifacts only support selecting the output of an upstream **artifact upload** task.<br><br>* For other managed applications, deploy using container images. Artifact sources support two methods: upstream artifact and custom artifact.<br><br>   * **Upstream artifact**: Select this option when the image to be deployed is the output of an upstream task. For example, in pipeline orchestration, the **compilation and build \> image build and push to image registry \> application deployment** tasks are executed in sequence, and the image used for deployment is selected from the output of the upstream image build task.<br><br>   * **Custom**: If you have already prepared the image, select this option and enter the full address of the image. The image address format is `host/namespace/repo:tag`. You can reference pipeline variables when entering the image address. |


<span id=".5pel5b-X5Y-K6YOo572y6K-m5oOF"></span>
## Logs and deployment details

Below, we use a K8s YAML application as an example to describe the details displayed in the pipeline after the preset task is completed.


1. On the run details page of the current pipeline, click the title of the application deployment card to view the run log and task configuration information.

   * Running log: Displays the real\-time running log for application deployment tasks, including checking configuration, triggering deployment, tracking deployment progress, and more.

   * Task configuration: Displays the configuration parameters for this task. For details, refer to the parameter description above.

2. Click **view deployment details** to navigate to the deployment details page for the corresponding application in the application delivery module. View the deployment progress of all components within an application.

3. Click **details** to drill down further and view the deployment progress of the current component. For the Deployment resource, you can click **view logs** to view real\-time Pod logs.
