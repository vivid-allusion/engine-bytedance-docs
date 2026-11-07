---
title: "Artifact management"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Artifact_management_steps"
---

The artifact management step is used in the pipeline to upload, download, and manage build artifacts that are not container images, such as binary files, compressed packages, configuration files, and more.

<span id="wpYu4Nhm"></span>
## TOS upload

Upload the specified file or directory to the specified storage bucket in TOS (object storage).


* **Addon**: upload\-tos@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |bucketRegion |string |Yes |\- |The region where the TOS storage bucket is located. |
   |bucketName |string |Yes |\- |The name of the target storage bucket. |
   |sourcePath |string |Yes |\- |The path of the source file or directory to upload. |
   |tosPath |string |Yes |/ |The target path in the storage bucket to upload to. |
   |containsParentDir |boolean |No |false |When uploading a directory, whether to retain the source directory under the target path.<br><br><br>* `true`: Retain the source directory.<br><br>* `false`: Default value, do not retain the source directory. |
   

* Example:

   ```YAML
   tasks:
     - task: task-tos-upload
       displayName: TOS Upload
       steps:
         - step: step-tos-upload
           component: upload-tos@1.0.0
           inputs:
             bucketRegion: cn-beijing
             bucketName: my-release-artifacts
             sourcePath: ./dist/app.zip
             tosPath: /releases/v1.0/
   ```
   


<span id="F0XisUuc"></span>
## TOS download

Download files or directories from the specified TOS storage bucket to the pipeline workspace.


* **Addon**: download\-tos@1.0.0

* **Parameter**:

   
   |**Parameter** |**Data type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |bucketRegion |string |Yes |\- |The region where the TOS storage bucket is located. |
   |bucketName |string |Yes |\- |The name of the target storage bucket. |
   |path |string |Yes |\- |The path of the file or directory in the storage bucket to download. |
   |targetPath |string |Yes |\- |The target path to download to the local workspace. |
   

* Example:

   ```YAML
   tasks:
     - task: task-tos-download
       displayName: TOS Download
       steps:
         - step: step-tos-download
           component: download-tos@1.0.0
           inputs:
             bucketRegion: cn-beijing
             bucketName: my-build-dependencies
             path: common-libs.zip
             targetPath: /workspace/libs
   ```
