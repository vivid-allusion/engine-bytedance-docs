---
title: "Resource deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Resource_deployment"
---

The deployment step is used to deploy build artifacts to target resources.

<span id="KJbKFyVS"></span>
## Kubectl deployment

Use the kubectl apply command to deploy the specified Kubernetes YAML manifest to the target cluster.


* **Addon**: kubectl\-deploy\-yaml@1.0.0

* **Parameters**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |deployResource |string |Yes |\- |Service connection ID of the target Kubernetes cluster. |
   |yamlManifest.type |enum |Yes |\- |Manifest type. Supports the following values:<br><br><br>* `Path`: Points to the file path.<br><br>* `File`: Inline YAML content. |
   |yamlManifest.content |string |Yes |\- |Content of the Kubernetes YAML resource manifest.<br><br><br>* When `type` is `Path`: Enter the file path for the content.<br><br>* When `type` is `File`: Enter the YAML text content. |
   |variables |list |No |[] |Variable replacement rule list, used to dynamically replace placeholders in YAML. Each item includes a key and value. |
   

* **Example:** 

   ```YAML
   tasks:
     - task: task-kubectl-path
       displayName: Kubectl Deploy (File Path)
       steps:
         - step: step-kubectl-path
           component: kubectl-deploy-yaml@1.0.0
           inputs:
             deployResource: my-k8s-cluster-connection
             yamlManifest:
               type: Path
               content: k8s/deployment.yaml
             variables:
               - key: image
                 value: demo:v1
   ```
