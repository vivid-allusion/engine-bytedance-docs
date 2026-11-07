---
title: "Resource deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Resource_deployment_steps"
---

Deployment\-type add\-ons are used to release build artifacts to the target running environment and support multiple deployment scenarios such as Kubernetes, ECS, FaaS, application delivery, and more.

<span id="6lQVvBik"></span>
## Kubernetes image upgrade

Update the container image of the specified workload in the Kubernetes cluster. By connecting to the specified deployment resource, match the app.name and containerName, and update their image address to the new version.


* **Addon**: kubernetes\-update\-image@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |app.kind |enum |Yes |Deployment |Workload type.<br><br><br>* Deployment: Stateless app deployment, elastic scaling, rolling update.<br><br>* StatefulSet: Stateful app, stable network and persistent storage.<br><br>* DaemonSet: Resident daemon on each node, automatically runs an instance on every node.<br><br>* CronJob: Scheduled task, automatically executes jobs periodically. |
   |app.name |string |Yes |\- |Name of the workload to be updated. |
   |containerName |string |Yes |\- |Container name of the image to be updated. |
   |deployImage.type |enum |Yes |Custom |Image source type.<br><br><br>* Custom: manually specify the image address.<br><br>* Output: reference upstream artifact. |
   |deployImage.content |string |Yes |\- |Image address. When type is Output, fill in the upstream artifact reference expression. |
   |deployResource |string |Yes |\- |ID of the deployment resource. To view the deployment resource ID, see [view deployment resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource_management?lang=en#.5p-l55yL6YOo572y6LWE5rqQ). |
   |namespace |string |Yes |\- |The namespace of the workload in Kubernetes. |
   |timeout |duration |Yes |30m |Timeout time for image upgrade operation. Default is 2h, supports minutes (m), hours (h), and days (d) units, maximum is 3 days. |
   

* **Example**

   ```YAML
   tasks:
     - task: task-update-image-custom
       displayName: "Kubernetes Image Update (Custom)"
       component: kubernetes-update-image@1.0.0
       inputs:
         app:
           kind: Deployment
           name: my-app-backend
         containerName: backend-server
         deployImage:
           type: Custom
           content: "registry.example.com/my-app/backend:v1.2.0"
         deployResource: "k8s-cluster-prod"
         namespace: "production"
         timeout: 30m
   ```
   


<span id="XSp68ptp"></span>
## Kubernetes batch release

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only the Deployment type is supported.</div>


Batch release for applications of the Kubernetes Deployment type. Allows definition of deployment batches, instance ratio per batch, and wait time between batches to achieve smooth and controllable online changes.


* **Addon**: rolling\-update\-image@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |app.kind |enum |Yes |Deployment |Workload type, fixed as Deployment. |
   |app.name |string |Yes |\- |Name of the deployment to be updated. |
   |containerName |string |Yes |\- |Container name of the image to be updated. |
   |deployImage.type |enum |Yes |Custom |Image source type.<br><br><br>* Custom: Custom images.<br><br>* Output: Upstream output. |
   |deployImage.content |string |Yes |\- |Image address or upstream artifact reference. |
   |deployResource |string |Yes |\- |ID of the deployment resource. |
   |namespace |string |Yes |\- |Namespace of the workload in Kubernetes. |
   |deployStrategy.ratio |list |Yes |\- |Pod ratio for each batch release; the sum of all elements must be 100. For example, [20, 80] means 20% in the first batch, 80% in the second batch. |
   |deployStrategy.round |int |Yes |\- |Total deployment batches, must be equal to the length of the ratio list. For example, if ratio is [20, 80], it means two batches, so round is 2. |
   |deployStrategy.waitTime |int |Yes |300 |Wait time between the completion of each batch release and the start of the next batch, in seconds, range: 1–7200. |
   

* Example:

   ```YAML
   tasks:
     - task: task-rolling-update
       displayName: "Service A Rolling Update (50/50)"
       component: rolling-update-image@1.0.0
       inputs:
         app:
           kind: Deployment
           name: service-a
         containerName: main-container
         deployImage:
           type: Custom
           content: "registry.example.com/my-org/service-a:1.5.0"
         deployResource: "k8s-cluster-prod"
         namespace: "production"
         deployStrategy:
           ratio:
             - 50
             - 50
           round: 2
           waitTime: 300
   ```
   

&nbsp;


<span id="hjO1haUa"></span>
## ECS operations and maintenance

Execute custom command or script on the specified ECS (Elastic Compute Service) instance. Supports Shell and Python scripts, and optionally downloads upstream artifacts to the target instance before executing the command.


* **Addon**: ecs\-ops@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |cmd.type |enum |Yes |Shell |Command type, Shell / Python. |
   |cmd.value |string |Yes |\- |Content of the script to be executed. |
   |region |enum |Yes |\- |Region where the ECS instance is located. |
   |instances |list |Yes |\- |ECS instance ID list, such as i\-xxxx. Supports parallel execution of multiple instances. |
   |path |string |Yes |\- |Path for executing the command on ECS instance. |
   |user |string |Yes |root |Operating system user for executing the command. |
   |timeout |duration |Yes |2h |Timeout time for command execution. Default 2h, supports m (minutes), h (hours), and d (days) units, maximum not exceeding 3 days. |
   |artifact.path |string |No |\- |The absolute path where the artifact is stored in the ECS instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If artifact is provided, both path and source must be filled in.</div><br> |
   |artifact.source |string |No |\- |Reference expression for upstream artifact. |
   

* **Example**

   ```YAML
   tasks:
     - task: task-ecs-shell
       displayName: "ECS Ops: Execute Shell Script"
       component: ecs-ops@1.0.0
       inputs:
         cmd:
           type: Shell
           value: |-
             #!/bin/bash
             echo "hello"
         instances:
           - i-ydy6itps74cva4fn****
           - i-ydy6itps74cva4fn****
         path: "/home"
         region: "cn-beijing"
         timeout: 5m
         user: "root"
   ```
   


<span id="CbL5hPlq"></span>
## Function deployment

Deploy code package or container image as a new version on the function compute platform. Supports two policies: full release and canary release.


* **Addon**: faas\-deploy@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |region |enum |Yes |\- |Region where the function is located. |
   |functionId |string |Yes |\- |Function ID to be deployed. |
   |functionVersion |string |Yes |\- |Function version number to be created in this deploy. Fill in 0 for the latest version. |
   |deployPolicy.type |enum |Yes |full |Deployment policy.<br><br><br>* full: full release.<br><br>* canary: canary release. |
   |deployPolicy.ratio |int |No |\- |Canary traffic ratio, scope 1~99. Required when deployPolicy.type is canary. |
   |artifact.mode |enum |Yes |output |Artifact source mode.<br><br><br>* output: Reference upstream artifact.<br><br>* custom: User custom. |
   |artifact.type |enum |Yes |tos |Artifact repository type.<br><br><br>* tos: object storage files (such as .zip).<br><br>* image: container image. |
   |artifact.value |string |Yes |\- |Specific value of the artifact (upstream reference expression or custom address). |
   

* **Example**

   ```YAML
   tasks:
     - task: task-faas-deploy-full
       displayName: "FaaS Full Deploy"
       component: faas-deploy@1.0.0
       inputs:
         region: "cn-beijing"
         functionId: "my-awesome-func"
         functionVersion: "0"
         deployPolicy:
           type: full
         artifact:
           mode: output
           type: tos
           value: "$(stages.build.tasks.zip.outputs.tosOutput_step-1)"
   ```
   


<span id="3EWW4F4Y"></span>
## Application deployment

General add\-ons for deploying various applications through the AppDeliver platform. Supports two application types: K8sYaml and Managed, and deploys the specified artifact to the target environment.


* **Addon**: appdeliver\-deploy@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |app |string |Yes |\- |The unique identifier of the app to be deployed on the app delivery platform. |
   |appType |enum |Yes |\- |Application type.<br><br><br>* K8sYaml: K8sYaml application.<br><br>* Managed: Managed application. |
   |env |string |Yes |\- |Target environment name, for example dev (test environment), staging (pre\-release environment), prod (production environment). |
   |timeout |duration |Yes |30m |Timeout time for deploy operation. Default 2h, supports m (minutes), h (hours), and d (days) units, maximum not exceeding 3 days. |
   |deployStrategy |string |Yes |RollingUpdate |Deployment policy, currently only supports RollingUpdate batch rolling release. |
   |versionNumber |string |No |Current timestamp |The version number of this deployment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when appType is Managed.</div><br> |
   |appStack |string |No |\- |Type of managed app, optional: Java / Other.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when appType value is Managed.</div><br> |
   |artifactList |list |No |\- |Artifacts to be deployed. Each item includes type (Custom/Output), artifact (artifact value), and placeholderName (template placeholder name). The default placeholder for K8sYaml is image.backend, and the default for managed application is Image. |
   

* **Example**

   ```YAML
   tasks:
     - task: appdeliver-deploy-1
       displayName: App Deploy
       component: appdeliver-deploy@1.0.0
       inputs:
         app: k8syaml
         appType: K8sYaml
         artifactList:
           - artifact: $(stages.exec-cmd.tasks.exec-cmd.outputs.imageOutput_step-c14)
             placeholderName: image.backend
             type: Output
         deployStrategy: RollingUpdate
         env: dev1
         timeout: 30m
   ```
