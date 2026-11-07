---
title: "Kubectl release"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/The_Kubectl_release"
---

CP provides the **Kubectl release** task, which allows users to create Kubernetes release tasks based on YAML resource description files, deploying YAML files from the code repository or custom YAML files to the Kubernetes cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster to be deployed must be connected. For specific operations, see [Connect deployment resource](https://docs.byteplus.com/en/docs/cp/Integrate_deployment_resources).

* The YAML file must be prepared.

* If the target image is private, ensure that the secret or secretless addon is configured in the deployment cluster in advance. For VKE service configuration, refer to [Configure Secret ](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret), [Configure secretless addon ](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2). Add task


When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select **Kubectl release** as the task template.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following describes the parameters for this built\-in task.


* **Job name**

   The default is Kubectl release; you can customize the job name.

* **Upstream task**

   Displays the name of the upstream sequential task for the current task. If there is no upstream task, `-` is displayed.

* **Code source download policy**

   Select the code source download policy based on whether the current task needs to use the code source.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes a default step (Kubectl release). You can add other sequential steps to the current task as needed. The following describes the parameters for this default step.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is Kubectl release; you can customize the step name. |
   |Deployment resource |Select the connected cluster to be deployed. |
   |YAML file |Enter the YAML file. You can specify a file path or input a custom YAML file; choose as needed.<br><br><br>* **File path**: Enter the name of the YAML file to be deployed or the relative path to the YAML file directory in the source code. The default is `./manifest`.<br><br>* **Custom file**: Write the YAML file yourself. You can use templates to quickly create YAML files. The system provides five templates: Namespace, Deployment, StatefulSet, Service, and ConfigMap. |
   |Image reference |Optional configuration. When referencing upstream pipeline outputs for images in the YAML file, this parameter must be specified.<br><br>Set the variable key, select the output of the preceding image packaging task, and use `$(key)` in YAML to replace the value of the corresponding image parameter. For example: set the key to `image` and select the target upstream artifact. In YAML, use `$(image)` to replace the original image value. |
   |Variable |Optional configuration. Replace parameters in the YAML file with variables to improve the generality and flexibility of the YAML file.<br><br>Click `+` to add a variable. Supports adding multiple variables.<br><br>Variables consist of a key and a value:<br><br><br>* key: Variable name. Caution: The key here must be consistent with the key specified in the YAML file. In YAML, reference the variable using `$(key)`.<br><br>* value: Variable value. The value can be a constant or a pipeline variable.<br><br>   For example: In the Deployment.yaml file, set the namespace to be deployed as the variable `$(namespace)`. In this case, the key should be `namespace`; the value can be a constant (for example, `default`) or a pipeline variable (for example, `$(parameters.ns)`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the image reference key conflicts with the variable key, the image reference has higher priority.</div><br> |
   |Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current step fails, it will be skipped. The remaining steps of the current task and the pipeline will continue.<br><br>* Turn off: If the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |
   

* **Task output**

   Show all outputs of the current task, including outputs from all steps within the current task. If there are no outputs, display as `-`. Outputs can be used as input for subsequent tasks.

   For the current default built\-in steps, outputs the deployment resource ID.

* **Advanced settings**

   * **Timeout time**: Set the timeout time for the entire task. The task will automatically fail after timing out. A task can include multiple serial steps. The total execution time of all steps must be less than the task's timeout time.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Larkbot, helping you stay informed about task status in a timely manner.


<span id=".5pel5b-X6K-05piO"></span>
## Log description

The following describes the information displayed in the pipeline after this built\-in task is completed.

On the run details page of the current pipeline, click the title of the Kubectl Release card to view run logs, task configuration, and other information.


* Run log: Shows the run log of this task in real time.

* Task configuration: Shows the configuration parameters of this task. For details, refer to the parameter description above.
