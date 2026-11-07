---
title: "Define pipelines with YAML"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Define_pipelines_with_YAML"
---

<span id="基本结构"></span>
# basic structure

The definition of a pipeline consists of three parts:


* Pipeline global configuration: Pipeline globally valid configuration items

* Task template: Configuration template for nodes (subtasks), each node in the pipeline is used as custom training (see [Feature Overview](https://docs.byteplus.com/docs/undefined/67e50da70145ec05386c0641)), and the configuration information and input are defined in the task template

* Task Choreography: Define what each node runs by referencing task templates, and orchestrate the execution order and dependencies of nodes


The following is the basic structure of a pipeline configuration yaml, in which:


* `Inputs`defines the global input parameters of the pipeline

* `taskTemplates`defines the configuration of subtasks (nodes), and the detailed parameter description refers to the custom training configuration .

* `Tasks`arranges the execution order and dependencies of the tasks in the pipeline, and defines the input value of each task node


```yaml
version: v1 
kind: PipelineTemplate  
inputs:    ...
taskTemplates:    ...
tasks:    ...
```


<span id="yaml-example"></span>
# YAML Example

<span id="hello-world-创建一个单任务工作流"></span>
## Hello World: Create a single\-task pipeline


* **Define task template**

* ```yaml

```



...

taskTemplates:


* name: hello_world_temp

   type: CustomTask

   spec:

   # Entry command    <span id="entry-command"></span>

   Entrypoint: echo "Hello World!"

   # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom    <span id="training-framework-supports-tensorflowps-pytorchddp-mpi-byteps-custom"></span>

   Framework: Custom

   # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field    <span id="image-url-use-this-field-when-using-byteplus-image-or-public-image-imageurl-takes-precedence-over-the-image-field"></span>

   ImageUrl: vemlp\-ap\-southeast\-1.cr.volces.com/preset\-images/python:3.7\-ubuntu20.04

   # Queue name    <span id="queue-name"></span>

   ResourceQueueName:

   # Instance configuration    <span id="instance-configuration"></span>

   TaskRoleSpecs:

   * Flavor: ml.g1ie.large # Instance type (Flavor)

      RoleName: worker # Role name (RoleName)

      RoleReplicas: 1 # Number of roles (RoleReplicas)

      ...


```Plain Text
**task scheduling**
* ```yaml
...
tasks:
- name: hello_world                    # Node name  
  taskTemplateName: hello_world_temp   # Referenced task template name
...
```


**Complete pipeline YAML**

<span id="创建任务a串联任务b的线性工作流"></span>
## ```yaml

version: v1

kind: PipelineTemplate

<span id="define-node-sub-task-templates-in-the-workflow"></span>
# Define node (sub\-task) templates in the workflow

taskTemplates:


* name: hello_world_temp

   type: CustomTask

   spec:

   # Entry command    <span id="entry-command"></span>

   Entrypoint: echo "Hello World!"

   # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom    <span id="training-framework-supports-tensorflowps-pytorchddp-mpi-byteps-custom"></span>

   Framework: Custom

   # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field    <span id="image-url-use-this-field-when-using-byteplus-image-or-public-image-imageurl-takes-precedence-over-the-image-field"></span>

   ImageUrl: vemlp\-ap\-southeast\-1.cr.volces.com/preset\-images/python:3.7\-ubuntu20.04

   # Queue name    <span id="queue-name"></span>

   ResourceQueueName:

   # Instance configuration    <span id="instance-configuration"></span>

   TaskRoleSpecs:

   * Flavor: ml.g1ie.large # Instance type (Flavor)

      RoleName: worker # Role name (RoleName)

      RoleReplicas: 1 # Number of roles (RoleReplicas)


tasks:


* name: hello_world # Node name

   taskTemplateName: hello_world_temp # Referenced task template name


```Plain Text
Create a linear pipeline of Task A concatenating Task B

* **Define task template**
* ```yaml
...
taskTemplates:  
  - name: demo    
    type: CustomTask    
    spec:      
      Entrypoint: echo "Hello Pipeline!" 
      
      # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom
      Framework: Custom                  
      
      # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field
      ImageUrl: vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.7-ubuntu20.04      
      
      # Queue name
      ResourceQueueName: ldy-test-user0  
      
      # Instance configuration
      TaskRoleSpecs:                     
        - Flavor: ml.g1ie.large          # Instance type (Flavor)          
          RoleName: worker               # Role name (RoleName)     
          RoleReplicas: 1                # Number of roles (RoleReplicas)
...
```


**task scheduling**

Define the task templates referenced by each node, and the dependencies between nodes


* ```yaml

```



...

tasks:


* name: task_a

   taskTemplateName: demo # Reference the task configuration defined in 'demo'

* name: task_b

   taskTemplateName: demo

   dependencies: # Specify upstream dependencies

   * task_a # Depends on the completion of task_a

      ...


```Plain Text
**Complete pipeline YAML**

<span id="配置工作流输入参数，支持在子任务中引用工作流的输入"></span>
## ```yaml
version: v1 
kind: PipelineTemplate    

# Define node (sub-task) templates in the workflow
taskTemplates:
- name: demo  
  type: CustomTask  
  spec:    
    Entrypoint: echo "Hello Pipeline!" 
    
    # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom
    Framework: Custom                  
    
    # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field
    ImageUrl: vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.7-ubuntu20.04    
    
    # Queue name
    ResourceQueueName: ldy-test-user0  
    
    # Instance configuration
    TaskRoleSpecs:                     
    - Flavor: ml.g1ie.large            # Instance type (Flavor)      
      RoleName: worker                 # Role name (RoleName)      
      RoleReplicas: 1                  # Number of roles (RoleReplicas)

tasks:
- name: task_a                         # Node name  
  taskTemplateName: demo              # Referenced task template name

- name: task_b  
  taskTemplateName: demo  
  dependencies:                       # Specify upstream dependencies  
  - task_a                            # Depends on the completion of task_a
```


Configure pipeline input parameters to support referencing pipeline input in subtasks


* **Define global input**

* ```yaml

```



...

<span id="define-input-parameters-for-the-pipeline"></span>
# Define input parameters for the Pipeline

inputs:


* name: image_url # Parameter name

   type: string # Parameter type

   hint: Image URL # Parameter description

   # Default parameter value    <span id="default-parameter-value"></span>

   defaultValue: vemlp\-ap\-southeast\-1.cr.volces.com/preset\-images/python:3.7\-ubuntu20.04

* name: command

   type: string

   hint: Entry command # Parameter description

   ...


```Plain Text
**Define task template**
   Define input parameters in the task template
* ```yaml
...
taskTemplates:  
  ...  
  # Define input parameters for node (sub-task) templates in the workflow  
  inputs:  
  - name: resource_queue_name         # Parameter name    
    type: string                      # Parameter type    
    hint: Queue name                  # Parameter description    
    defaultValue: <Your Resource Queue Name>    # Default parameter value  
  
  - name: image_url  
    type: string     
    hint: Image URL                   # Parameter description  
  
  - name: command    
    type: string    
    hint: Entry command               # Parameter description  
  
  spec:    
    ...    
    Entrypoint: '{{inputs.command}}'              # Reference the input parameter named 'command' defined in the template    
    ImageUrl: '{{inputs.image_url}}'    
    ResourceQueueName: '{{inputs.resource_queue_name}}'    
    ...    
  ...  
...
```


**task scheduling**


* Define the task templates referenced by each node, and the dependencies between nodes

* And reference the global input parameters, pass in the input parameters required by the subtask template

* ```yaml

```



...

tasks:


* name: task_a

   taskTemplateName: task_demo

   inputs:

   * name: image_url

      value: '{{pipeline.inputs.image_url}}' # Reference the input parameter named image_url defined in the Pipeline

   * name: command

      value: '{{pipeline.inputs.command}}' # Undeclared input parameter; will use the default value defined in the template (e.g., resource_queue_name)

* name: task_b

   taskTemplateName: task_demo

   dependencies:

   * task_a

      inputs:

   * name: image_url

      value: '{{pipeline.inputs.image_url}}'

   * name: command

      value: echo "task b!" # Use a constant to override the template\-defined input parameter named command

   * name: resource_queue_name # Override the default value of the input parameter resource_queue_name defined in the template

      value: flow 0414

      ...


```Plain Text
**Complete pipeline YAML**

<span id="创建一个工作流，同时上传本地代码"></span>
## ```yaml
...
tasks:
- name: task_a                  
  taskTemplateName: task_demo 
  inputs:  
  - name: image_url    
    value: '{{pipeline.inputs.image_url}}'   # Reference the input parameter named 'image_url' defined in the Pipeline  
  
  - name: command    
    value: '{{pipeline.inputs.command}}'     # Undeclared input parameter; the default value defined in the template (e.g., resource_queue_name) will be used

- name: task_b  
  taskTemplateName: task_demo  
  dependencies:                
  - task_a                     
  
  inputs:  
  - name: image_url    
    value: '{{pipeline.inputs.image_url}}'  
  
  - name: command    
    value: echo "task b!"                    # Use a constant to override the template-defined input parameter named 'command'  
  
  - name: resource_queue_name               # Override the default value of the input parameter 'resource_queue_name' defined in the template  
    value: flow 0414  
...
```


Create a pipeline and upload local code at the same time


* **Define task template**

   Define the code upload configuration in the task template

* ```yaml

```



...

<span id="define-node-sub-task-templates-in-the-workflow"></span>
# Define node (sub\-task) templates in the workflow

taskTemplates:


* name: upload_code

   type: CustomTask

   spec:

   # Local path of the code to be uploaded.    <span id="local-path-of-the-code-to-be-uploaded"></span>

   # If it's a directory ending with '/', all contents under the directory will be uploaded to RemoteMountCodePath.    <span id="if-it-s-a-directory-ending-with-all-contents-under-the-directory-will-be-uploaded-to-remotemountcodepath"></span>

   # If it's a directory not ending with '/', the directory itself and all contents under it will be uploaded to RemoteMountCodePath.    <span id="if-it-s-a-directory-not-ending-with-the-directory-itself-and-all-contents-under-it-will-be-uploaded-to-remotemountcodepath"></span>

   UserCodePath: samples/pipeline/code/single_with_upload_code/

   # Use a previously uploaded code snapshot    <span id="use-a-previously-uploaded-code-snapshot"></span>

   # UserCodePath: tos://ml\-platform\-auto\-created\-required\-2100000050\-cn\-guilin\-boe/static/customtask/manifest/snapshot_jqsgdgcsc69nvzx8.manifest    <span id="usercodepath-tos-ml-platform-auto-created-required-2100000050-cn-guilin-boe-static-customtask-manifest-snapshot-jqsgdgcsc69nvzx8-manifest"></span>

   # Path after uploading the code, which will be used as the code mount path inside the container    <span id="path-after-uploading-the-code-which-will-be-used-as-the-code-mount-path-inside-the-container"></span>

   RemoteMountCodePath: "/root/code"

   ...

   ...

   ...


```Plain Text
**Complete pipeline YAML**

<span id="任务编排示例"></span>
## ```yaml
version: v1
kind: PipelineTemplate

# Define node (sub-task) templates in the workflow
taskTemplates:
- name: upload_code  
  type: CustomTask  
  spec:    
    # Local path of the code to be uploaded. 
    # If it's a directory ending with '/', all contents under the directory will be uploaded to RemoteMountCodePath.  
    # If it's a directory not ending with '/', the directory itself and all contents under it will be uploaded to RemoteMountCodePath  
    UserCodePath: run.sh    
    
    # Use a previously uploaded code snapshot  
    # UserCodePath: tos://ml-platform-auto-created-required-2100000050-cn-guilin-boe/static/customtask/manifest/snapshot_jqsgdgcsc69nvzx8.manifest    
    
    # Path after uploading the code, which will be used as the code mount path inside the container  
    RemoteMountCodePath: "/root/code"    
    
    # Access scope, supports Public / Queue / Private  
    AccessType: Public    
    
    # List of visible users. Uncomment the lines below to configure.  
    # Note: If the access scope is Private/Public, this list has no effect  
    # AccessUsers:    
    # - "username_a"    
    # - "username_b"    
    
    # Entry command  
    Entrypoint: cd /root/code && bash run.sh    
    
    # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom  
    Framework: Custom    
    
    # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field  
    ImageUrl: vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.7-ubuntu20.04    
    
    # Queue name  
    ResourceQueueName: <Your Resource Queue Name>    
    
    # Instance configuration  
    TaskRoleSpecs:    
    - Flavor: ml.c1.large              # Instance type (Flavor)      
      RoleName: worker                 # Role name (RoleName)      
      RoleReplicas: 1                  # Number of roles (RoleReplicas)

tasks:
- name: upload_code                    # Node name  
  taskTemplateName: upload_code        # Referenced task template name
```


Task Orchestration Example


* **Serial: Define a pipeline with three task nodes, which are executed sequentially**

* ```yaml

```



version: v1

kind: PipelineTemplate

<span id="define-node-sub-task-templates-in-the-workflow"></span>
# Define node (sub\-task) templates in the workflow

taskTemplates:


* name: demo type: CustomTask spec: ...

   tasks:

* name: task_a

   taskTemplateName: demo

* name: task_b taskTemplateName: demo dependencies:

   * task_a

* name: task_c taskTemplateName: demo dependencies:

   * task_b


<span id="R2fZKMsaE9"></span>
# +\-\-\-\-\-\-\-\-\-+

<span id="task-a"></span>
# | task_a |

<span id="OLy2UqmMaP"></span>
# +\-\-\-\-+\-\-\-\-+

<span id="hZPnTqBOxe"></span>
# |

<span id="v"></span>
# +\-\-\-\-v\-\-\-\-+

<span id="task-b"></span>
# | task_b |

<span id="DwU2wELK2p"></span>
# +\-\-\-\-+\-\-\-\-+

<span id="oDeLudndQg"></span>
# |

<span id="v"></span>
# +\-\-\-\-v\-\-\-\-+

<span id="task-c"></span>
# | task_c |

<span id="BEDtziKh3e"></span>
# +\-\-\-\-\-\-\-\-\-+

```Plain Text
**Parallel: Define a pipeline with three task nodes that execute in parallel**
* ```yaml
version: v1 
kind: PipelineTemplate    
# Define node (sub-task) templates in the workflow
taskTemplates:
- name: demo  type: CustomTask  spec:    ...
tasks:
- name: task_a             
  taskTemplateName: demo 
- name: task_b  taskTemplateName: demo           
- name: task_c  taskTemplateName: demo 
# +--------+   +--------+   +--------+
# | task_a |   | task_b |   | task_c |
# +--------+   +--------+   +--------+
```


**Diamond: Define a diamond pipeline with 4 nodes**

```yaml
version: v1 
kind: PipelineTemplate    
# Define node (sub-task) templates in the workflow
taskTemplates:
- name: demo  type: CustomTask  spec:    ...
tasks:
- name: task_a             
  taskTemplateName: demo 
- name: task_b  taskTemplateName: demo    
  dependencies:            
  - task_a                 
- name: task_c  taskTemplateName: demo  dependencies:            
  - task_a           
- name: task_d  taskTemplateName: demo  dependencies:            
  - task_b  - task_c          
#       +--------+   
#       | task_a |  
#       +--------+   
#        /      \
# +--------+   +--------+
# | task_b |   | task_c |
# +--------+   +--------+
#        \      /
#       +--------+   
#       | task_d |  
#       +--------+
```


<span id="创建一个-loop-算法工作流"></span>
## Create a loop algorithm pipeline

Pipeline supports three loop syntax:


* withSequence iterates over some numbers, which can be referenced by `{{item}}`

* withItems gets a list and executes each item

   * Can be a single value that can be referenced by `{{item}}`

   * Can be a json, can be referenced by `{{item.key}}`

* withParam reads and iterates through a JSON array, enabling dynamic generation from other steps in the pipeline.


<span id="loop-语法-1：withsequence"></span>
### Loop Syntax 1: withSequence


* **Task orchestration: execute hello\-world\-x5 5 times**


```yaml
...
tasks:  - name: hello-world-x5    taskTemplateName: print-message    inputs:      - name: message        value: '{\"hello world\":{{item}}}'    withSequence:      count: 5
...
```



* **Complete pipeline YAML**


```yaml
version: v1
kind: PipelineTemplate

# Define node (sub-task) templates in the workflow
taskTemplates:  
  - name: print-message    
    type: CustomTask    
    inputs:      
      - name: message        
        type: string    
    outputs:      
      - name: message        
        type: string        
        valueFrom:          
          file: /out    
    spec:      
      # Entry command
      Entrypoint: |
        echo  {{inputs.message}} | tee /out
      
      # Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom
      Framework: Custom
      
      # Image URL: use this field when using BytePlus image or public image; ImageUrl takes precedence over the Image field
      ImageUrl: vemlp-cn-beijing.cr.volces.com/preset-images/python:3.7
      
      # Queue name
      ResourceQueueName: <Your Resource Queue Name>
      
      # Instance configuration
      TaskRoleSpecs:        
        - Flavor: ml.c3i.large          # Instance type (Flavor)
          RoleName: worker              # Role name (RoleName)
          RoleReplicas: 1              # Number of roles (RoleReplicas)

tasks:  
  - name: hello-world-x5              # Node name  
    taskTemplateName: print-message   # Referenced task template name  
    inputs:      
      - name: message        
        value: '{\"hello world\":{{item}}}'    
    withSequence:      
      count: 5  

  - name: aggregate-output  
    taskTemplateName: print-message  
    dependencies:      
      - hello-world-x5  
    inputs:      
      - name: message        
        value: "{{tasks.hello-world-x5.outputs.message}}"
```


<span id="loop-语法-2：withitems"></span>
### Loop Syntax 2: withItems


* **Task Orchestration: Execute loop\-with\-items 4 times**


```yaml
...
tasks:  - name: loop-with-items    taskTemplateName: print-message    inputs:      - name: message        value: '{\"image\":\"{{item.image}}\",\"tag\":\"{{item.tag}}\"}'    withItems:      - '{ "image": "debian", "tag": "9.1" }' #item set 1      - '{ "image": "debian", "tag": "8.9" }' #item set 2      - '{ "image": "alpine", "tag": "3.6" }' #item set 3      - '{ "image": "ubuntu", "tag": "17.10" }' #item set 4
...
```



* **Complete pipeline YAML**


```yaml
version: v1
kind: PipelineTemplate
taskTemplates:  - name: print-message    type: CustomTask    inputs:      - name: message        type: string    outputs:      - name: message        type: string        valueFrom:          file: /out    spec:      Entrypoint: |
        echo  {{inputs.message}}  | tee /out
      Framework: Custom      ImageUrl: vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.7      ResourceQueueName: <Your Resource Queue Name>      TaskRoleSpecs:        - Flavor: ml.c3i.large          RoleName: worker          RoleReplicas: 1
tasks:  - name: loop-with-items    taskTemplateName: print-message    inputs:      - name: message        value: '{\"image\":\"{{item.image}}\",\"tag\":\"{{item.tag}}\"}'    withItems:      - '{ "image": "debian", "tag": "9.1" }' #item set 1      - '{ "image": "debian", "tag": "8.9" }' #item set 2      - '{ "image": "alpine", "tag": "3.6" }' #item set 3      - '{ "image": "ubuntu", "tag": "17.10" }' #item set 4  - name: aggregate-output    taskTemplateName: print-message    dependencies:      - loop-with-items    inputs:      - name: message        value: "{{tasks.loop-with-items.outputs.message}}"
```


<span id="loop-语法-3：withparam"></span>
### Loop Syntax 3: withParam


* **Task orchestration: The number of loop\-with\-param executions is determined by the length of the generated output.** 


```yaml
...
tasks:  - name: generate    taskTemplateName: gen-number-list  - name: loop-with-param    taskTemplateName: sleep-then-print-message    dependencies:      - generate    inputs:      - name: number        value: "{{item}}"      - name: message        value: '{\"number\":{{item}}}'    withParam: "{{tasks.generate.outputs.number-list}}"
...
```



* **Complete pipeline YAML**


```yaml
version: v1
kind: PipelineTemplate
taskTemplates:  - name: gen-number-list    type: CustomTask    outputs:      - name: number-list        type: string        valueFrom:          file: /out    spec:      Entrypoint: |
        echo "[5,6,7,8,9]"  > /out
      Framework: Custom      ImageUrl: vemlp-cn-beijing.cr.volces.com/preset-images/python:3.7      ResourceQueueName: <Your Resource Queue Name>      TaskRoleSpecs:        - Flavor: ml.c3i.large          RoleName: worker          RoleReplicas: 1  - name: sleep-then-print-message    type: CustomTask    inputs:      - name: number        type: int      - name: message        type: string    outputs:      - name: message        type: string        valueFrom:          file: /out    spec:      Entrypoint: |
        echo  {{inputs.message}} | tee /out
      Framework: Custom      ImageUrl: vemlp-cn-beijing.cr.volces.com/preset-images/python:3.7      ResourceQueueName: <Your Resource Queue Name>      TaskRoleSpecs:        - Flavor: ml.c3i.large          RoleName: worker          RoleReplicas: 1
tasks:  - name: generate    taskTemplateName: gen-number-list  - name: loop-with-param    taskTemplateName: sleep-then-print-message    dependencies:      - generate    inputs:      - name: number        value: "{{item}}"      - name: message        value: '{\"number\":{{item}}}'    withParam: "{{tasks.generate.outputs.number-list}}"  - name: aggregate-output    taskTemplateName: sleep-then-print-message    dependencies:      - loop-with-param    inputs:      - name: number        value: 0      - name: message        value: "{{tasks.loop-with-param.outputs.message}}"
```
