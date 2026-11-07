---
title: "Code management"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Code_management"
---

The code management step is used in the pipeline to execute version control actions on the code repository, such as creating tags, managing branches, and more.

<span id="Wf2TpMIa"></span>
## Git tag creation

Create a Git tag on the specified commit of the code repository associated with the current pipeline.


* **Addon**: git\-tag@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |tagName |string |Yes |\- |The name of the tag to create, such as v1.0.0. It must comply with Git tag naming conventions and must not already exist in the repository. |
   |description |string |No |\- |Annotation information for the tag (Annotation). |
   

* Example:

   ```YAML
   tasks:
     - task: task-git-tag
       displayName: Create Git Tag
       steps:
         - step: step-git-tag
           component: git-tag@1.0.0
           inputs:
             tagName: release-v1.2.0
             description: "Production release version 1.2.0"
   ```
