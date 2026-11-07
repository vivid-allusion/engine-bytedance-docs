---
title: "Function deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Function_deployment"
---

By orchestrating the **function deployment** task in the pipeline, you can deploy function as a service. This article introduces how to use functions to deploy tasks.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|Configuration Item |Descriptions |
|---|---|
|Task name |Defaults to function deployment and supports custom task names. |
|Upstream task |Display the name of the upstream serial task of the current task. Displays "None" when there is no upstream task`-`. |
|Region |Select the Region where the function needs to be deployed. |
|Function ID |Select an existing Function Service. Supports selecting a specific Function Service name or entering a variable for a custom Function Service ID (for example, `$(parameters.id)`). Variables can support more flexible function selection. For information on how to use custom variables, refer to [Custom variables](https://docs.byteplus.com/en/docs/cp/Custom_variables). |
|Version |Select the version of Function Service to be deployed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When <strong>function ID</strong> is a variable, <strong>version</strong> must specify the version ID. For example, if the <strong>function ID</strong> is <code>$(parameters.id)</code> and you need to select the <code>latest</code> version, enter <code>latest</code> in the <strong>version</strong> field.<code>0</code>.</div><br> |
|artifact |Set the artifact to be deployed.<br><br><br>* **Artifact type**: Supports two types: TOS zip package and image.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Ensure that the artifact type selected in the pipeline and in Function Service are the same. For example, both are Top zip packages or both are images.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the artifact name provided does not exist or is incorrect, the artifact may not be replaced correctly during this deployment, which can result in deployment failure or outcomes that do not meet deployment expectations.</div><br><br><br>* **Artifact source**: Supports two methods: upstream artifact and custom method.<br><br>   * **Upstream artifact**: Only supported when the upstream artifact is used to build an image. Select this option when the image to be deployed is the output of an upstream task. For example, in pipeline orchestration **compilation and build \> image build and push to image repository \> function deployment** tasks, the image is selected as the artifact produced by the upstream image build task.<br><br>      * Artifact type is **TOS zip package**: only supported when the upstream output is **TOS upload**. For the method of creating upstream products, refer to [TOS upload](https://docs.byteplus.com/en/docs/cp/TOS_upload).<br><br>      * Artifact type is **image**: Supported only when the upstream artifact is built as an image. For instructions on how to create the upstream artifact, refer to [image build and push](https://docs.byteplus.com/en/docs/cp/Build_and_push_images).<br><br>   * **Custom**: Enter the full address of a created image or TOS.<br><br>      * Artifact type: **TOS zip package**: Enter the complete address of the created TOS. The TOS address is a string in the format `bucket_name:object_key`, for example, `vefaas-test:vefaas-python38-default.zip`.<br><br>      * When the artifact type is **image**: enter the full address of the created image. Here, the image address format is `host/namespace/repo:tag`. When you enter the image address, you can reference pipeline variables. |
|Deployment policy |Supports two methods: **full release** and **gray release**. After selecting the gray release option, you need to specify the proportion of users for the gray version.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The first deployment of a function does not support canary release. Canary release is supported from the second deployment onward.</div><br> |
|Task output |Displays parameters used for querying the output status of a task. |
|Advanced settings |**Webhook notification**: You can receive task\-level messages via two methods: Webhook and Lark Bot, helping you stay informed about task updates in a timely manner. |
