---
title: "Command execution"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Command_execution_steps"
---

The command execution step is used to run custom Shell scripts in the pipeline or execute commands in the specified container environment, meeting flexible automation requirements.

<span id="BmkrdqcX"></span>
## Shell command execution

Execute user\-provided Shell commands in a standard Bash environment.


* **Addon**: exec@1.0.0

* **Parameter**:

   
   |**Parameter** |**Type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |cmd |string |Yes |\- |The command script to be executed (multi\-line Shell). |
   |shell |string |Yes |BASH |Shell type, fixed as BASH. |
   

* Example:

   ```YAML
   tasks:
     - task: task-exec-shell
       displayName: Execute Shell Command
       steps:
         - step: step-exec-shell
           component: exec@1.0.0
           inputs:
             cmd: |
               echo "Starting custom script..."
               ls -la
               echo "Script finished."
             shell: BASH
   ```
   


<span id="4DDGJtjd"></span>
## Custom environment command execution

Pull the Docker image specified by the user, and execute commands in the environment provided by that image. Suitable for scenarios requiring specific tools or dependencies.


* **Addon**: custom\-image@2.0.0

* **Parameter**:

   
   |**Parameter** |**Type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |image |string |Yes |\- |The Docker image used to execute commands, such as ubuntu:20.04. |
   |cmd |string |Yes |\- |The command to be executed in the container (multi\-line Shell). |
   |loginCredential |list |No |\- |Credentials for accessing the private container registry, use service connection. |
   

* **Example**

   ```YAML
   tasks:
     - task: task-custom-public
       displayName: Custom Image Command (Public)
       steps:
         - step: step-custom-public
           component: custom-image@2.0.0
           inputs:
             image: 'node:18-alpine'
             cmd: |
               echo "Node.js version:"
               node -v
   ```
