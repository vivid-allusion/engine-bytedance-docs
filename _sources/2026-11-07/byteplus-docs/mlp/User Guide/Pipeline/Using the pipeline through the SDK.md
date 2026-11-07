---
title: "Using the pipeline through the SDK"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Using_the_pipeline_through_the_SDK"
---

<span id="安装"></span>
# install

You need to install python 3.6 and above in advance.

```bash
wget https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/python_sdk_installer/volcengine_ml_platform-1.1.0b2-py3-none-any.whl
pip3 install volcengine_ml_platform-1.1.0b2-py3-none-any.whl
```


<span id="配置-ak-sk"></span>
# Configure AK/SK

Before officially using the SDK, you need to complete the local configuration of the AK/SK of the BytePlus account to verify the identity when using the SDK to access the Machine Learning Platform.


1. Log in to the BytePlus console and go to [Key Management] to view the AK/SK of the current account.

   1. If the current account is a sub account, an IAM policy for `AccessKeyFullAccess`is required.


Please replace < your access key \> and < your secret access key \> in the following methods with a real AK/SK

<span id="方法一（通过配置文件配置）："></span>
## Method 1 (through the configuration file):

```bash
mkdir -p $HOME/.volc
cat <<EOF > $HOME/.volc/credentials
[default]
access_key_id     = <your access key>
secret_access_key = <your secret access key>
EOFcat <<EOF > $HOME/.volc/config
[default]
region       = cn-beijing  # enter the arear, currently only supporting cn-beijing
EOF
```


<span id="方法二（通过代码配置）："></span>
## Method 2 (through code configuration):

```python
import volcengine_ml_platform as vemlp
vemlp.init(
    ak='<your access key>',
    sk='<your secret access key>',
    region='ap-southeast-1',
)
```


<span id="方法三（通过环境变量配置）："></span>
## Method 3 (through environment variables):

<span id="sdk-usage"></span>
# ```bash

export VOLC_ACCESSKEY=''

export VOLC_SECRETKEY=''

export VOLC_REGION=ap\-southeast\-1

```Plain Text
SDK Usage
<span id="pipeline"></span>
## Pipeline
```python
class volcengine_ml_platform.pipeline.Pipeline(
    *, 
    id: Optional[str] = None, 
    name: Optional[str] = None, 
    version_id: Optional[str] = None, 
    version_number: Optional[int] = None, 
    description: Optional[str] = None, 
    pipeline_template: Optional[PipelineTemplate] = None, 
    user_id: Optional[str] = None, 
    account_id: Optional[str] = None, 
    create_time: Optional[str] = None, 
    update_time: Optional[str] = None, 
    extra: Optional[Dict[str, str]] = None,
)
```


<span id="functions"></span>
### Functions

<span id="classmethod-get-id-optional-str-none-name-optional-str-none-pipeline"></span>
#### classmethod get(id: Optional[str] = None, name: Optional[str] = None) \-\> Pipeline

Get the latest configuration of the pipeline by id or name


* **Parameters**

   * **id** \- Pipeline id

   * **name** \- Pipeline name

* **Example**


<span id="classmethod-load-filename-str-type-str-yaml-name-optional-str-none-description-optional-str-none-pipeline"></span>
#### ```python

> from volcengine_ml_platform.pipeline import Pipeline

> p = Pipeline.get(id='pipeline_id')

> print(p)

> p = Pipeline.get(name='pipeline_name')

> print(p)


```Plain Text
classmethod load(filename: str, *, type: str = 'yaml', name: Optional[str] = None, description: Optional[str] = None) -> Pipeline
Loading Pipeline via Configuration File

* **Parameters**
   * **Filename** - the file path to load
   * **Type** - the type of file to load, currently only yaml is supported
   * **Name** - Pipeline name
   * **Description** - Pipeline description
* **Example**

<span id="create"></span>
#### ```python
>>> from volcengine_ml_platform.pipeline import Pipeline
>>> Pipeline.load(...)
>>> Pipeline.load(..., name='pipeline_name', description='pipeline_description')
```


create()

Create Pipeline


* **Example**


<span id="exists-bool"></span>
#### ```python

> from volcengine_ml_platform.pipeline import Pipeline

> Pipeline(name='pipeline_name', description='pipeline_description').create()

> Pipeline.load(...).create()


```Plain Text
exists() -> bool
Determine if the pipeline already exists

* **Example**

<span id="update-upload-code-progress-bar-bool-false-upload-code-timeout-int-3600-upload-code-copy-links-bool-false-upload-code-retain-links-bool-false"></span>
#### ```python
>>> from volcengine_ml_platform.pipeline import Pipeline
>>> Pipeline(id='pipeline_id').exists()
>>> Pipeline(name='pipeline_name').exists()
>>> Pipeline(id='pipeline_id', name='pipeline_name').exists()
>>> Pipeline.load(...).exists()
```


update(upload_code_progress_bar: bool = False, upload_code_timeout: int = 3600, upload_code_copy_links: bool = False, upload_code_retain_links: bool = False)

Update Pipeline Configuration


* **Parameters**

   * **upload_code_progress_bar** \- Whether the upload code shows a progress bar, not by default

   * **upload_code_timeout** \- Upload code timeout, default 1h (3600s)

   * **upload_code_copy_links** \- When a linked file is encountered, upload a copy of the file executed by the link (if the link fails, the upload will fail)

   * **upload_code_retain_links** \- When encountering a linked file, upload the linked file intact (if the link points to a file that does not exist in the mirror environment, an error may be reported at runtime)

* **Example**


<span id="launch-launch-name-optional-str-none-inputs-optional-union-dict-str-str-list-inputinstance-none-fail-fast-bool-false-str"></span>
#### ```python

> from volcengine_ml_platform.pipeline import Pipeline

> Pipeline(id='pipeline_id').update()

> Pipeline(name='pipeline_name').update()

> Pipeline.load(...).update()


```Plain Text
launch(launch_name: Optional[str] = None, inputs: Optional[Union[Dict[str, str], List[InputInstance]]] = None, fail_fast: bool = False) -> str
Run Pipeline, if `Pipeline.pipeline_template is None `run the latest configuration in the cloud, otherwise run the local configuration

* **Parameters**
   * **launch_name** - Run instance name, if not passed, automatically according to `{Pipeline.name} _ {random 5 chars} `format automatically generated
   * **Inputs** - Pipeline defines the required input parameters
* **Example**

<span id="update-and-launch-launch-name-optional-str-none-inputs-optional-union-dict-str-str-list-inputinstance-none-fail-fast-bool-false-upload-code-progress-bar-bool-false-upload-code-timeout-int-3600-upload-code-copy-links-bool-false-upload-code-retain-links-bool-false-→-str"></span>
#### ```python
>>> from volcengine_ml_platform.pipeline import Pipeline
>>> Pipeline.get(id='pipeline_id').launch()
>>> Pipeline.get(name='pipeline_name').launch()
>>> Pipeline.load(...).launch()
```


update_and_launch(launch_name: Optional[str] = None, inputs: Optional[Union[Dict[str, str], List[InputInstance]]] = None, fail_fast: bool = False, upload_code_progress_bar: bool = False, upload_code_timeout: int = 3600, upload_code_copy_links: bool = False, upload_code_retain_links: bool = False)→ str

Update and Run Pipeline


* **Parameters**

   * **launch_name** \- Run instance name, if not passed, automatically according to `{Pipeline.name} _ {random 5 chars}`format automatically generated

   * **Inputs** \- Pipeline defines the required input parameters

   * **upload_code_progress_bar** \- Whether the upload code shows a progress bar, not by default

   * **upload_code_timeout** \- Upload code timeout, default 1h (3600s)

   * **upload_code_copy_links** \- When a linked file is encountered, upload a copy of the file executed by the link (if the link fails, the upload will fail)

   * **upload_code_retain_links** \- When encountering a linked file, upload the linked file intact (if the link points to a file that does not exist in the mirror environment, an error may be reported at runtime)

* **Example**


<span id="show-axis-str-y"></span>
#### ```python

> from volcengine_ml_platform.pipeline import Pipeline

> Pipeline.get(id='pipeline_id').update_and_launch()

> Pipeline.get(name='pipeline_name').update_and_launch()

> Pipeline.load(...).update_and_launch()


```Plain Text
show(axis: str = 'y')
Print Pipeline DAG

* **Parameters**
   * **Axis** - print axes, `x `landscape, `y `portrait
* **Example**

<span id="dump-output-path-str-type-str-yaml"></span>
#### ```python
>>> Pipeline.get(id='pipeline_id').show()
"""
+ - - - - - - - - - - - - - - - - -+
'  linear_pipeline_with_two_tasks  '
'                                  '
' +------------------------------+ '
' |            task_a            | '
' +------------------------------+ '
'   |                              '
'   |                              '
'   v                              '
' +------------------------------+ '
' |            task_b            | '
' +------------------------------+ '
'                                  '
+ - - - - - - - - - - - - - - - - -+
"""
>>> Pipeline.get(id='pipeline_id').show(axis='x')
"""
+ - - - - - - - - - - - - - - - - - - - - - - - - - - -+
'            linear_pipeline_with_two_tasks            '
'                                                      '
' +--------+                                +--------+ '
' | task_a | -----------------------------> | task_b | '
' +--------+                                +--------+ '
'                                                      '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - -+
"""
```


dump(output_path: str = '.', \*, type: str = 'yaml')

Export Pipeline to File


* **Parameters**

   * **output_path** \- Export file path, if the path is a directory, it will automatically generate `{pipeline.name} _ {yyyyMMdd_hhmmss}. {type}`files

   * **Type** \- export file format, currently only supports yaml

* **Example**


<span id="pipelineinstance"></span>
## ```python

> from volcengine_ml_platform.pipeline import Pipeline

> Pipeline.get(id='pipeline_id').dump()

> Pipeline.get(name='pipeline_name').dump()

> Pipeline.load(...).dump()


```Plain Text
PipelineInstance
```python
class volcengine_ml_platform.pipeline.PipelineInstance(
    *, 
    id: Optional[str], 
    name: Optional[str], 
    pipeline_id: Optional[str], 
    pipeline_version_id: Optional[str], 
    pipeline_template: Optional[PipelineTemplate] = None, 
    global_inputs: Optional[List[InputInstance]] = None, 
    global_outputs: Optional[List[OutputInstance]] = None, 
    state: Optional[str] = None, 
    launch_time: Optional[str] = None, 
    finish_time: Optional[str] = None, 
    diag_info: Optional[str] = None, 
    trigger: Optional[str] = None, 
    user_id: Optional[str] = None, 
    account_id: Optional[str] = None, 
    create_time: Optional[str] = None, 
    update_time: Optional[str] = None, 
    extra: Optional[Dict[str, str]] = None,
)
```


<span id="functions"></span>
### **Functions**

<span id="classmethod-get-id-str-pipelineinstance"></span>
#### classmethod get(id: str) \-\> PipelineInstance

Get the information of the pipeline instance by id


* **Parameters**

   * **Id** \- Pipeline instance id

* **Example**


<span id="dump-output-path-str-type-str-yaml"></span>
#### ```python

> from volcengine_ml_platform.pipeline import PipelineInstance

> PipelineInstance.get('pipeline_instance_id')


```Plain Text
dump(output_path: str = '.', *, type: str = 'yaml')
Get the information of the pipeline instance by id

* **Parameters**
   * **output_path** - Export file path, if the path is a directory, it will automatically generate `{pipeline.name} _ {yyyyMMdd_hhmmss}. {type} `files
   * **Type** - export file format, currently only supports yaml
* **Example**
   ```python
   >>> from volcengine_ml_platform.pipeline import PipelineInstance
   >>> PipelineInstance.get('pipeline_instance_id').dump()
   >>> PipelineInstance.get('pipeline_instance_id').dump('pipeline.yaml')
```


<span id="show-axis-str-y"></span>
#### show(axis: str = 'y')

Get the information of the pipeline instance by id


* **Parameters**

   * **Axis** \- print axes, `x`landscape, `y`portrait

* **Example**

   ```python
   >>> from volcengine_ml_platform.pipeline import PipelineInstance
   >>> PipelineInstance.get('pipeline_instance_id').show()
   + - - - - - - - - - - - - - - - - - - - -+
   '  linear_pipeline_with_two_tasks_sasnf  '
   '                                        '
   ' +------------------------------------+ '
   ' |          task_a(Finished)          | '
   ' +------------------------------------+ '
   '   |                                    '
   '   |                                    '
   '   v                                    '
   ' +------------------------------------+ '
   ' |          task_b(Running)           | '
   ' +------------------------------------+ '
   '                                        '+ - - - - - - - - - - - - - - - - - - - -+
   ```
   


<span id="示例代码"></span>
# sample code

Please replace < Your Resource Queue Name \> below with a real queue name.

<span id="通过-yaml-运行工作流"></span>
## Run the pipeline through Yaml

<span id="创建并运行一个简单的工作流"></span>
### Create and run a simple pipeline


* YAML file can refer to: [Define pipelines with YAML](https://docs.byteplus.com/docs/mlp/Define_pipelines_with_YAML)

* The Python code example is as follows:


```python
import os
import sys
from volcengine_ml_platform.pipeline import Pipeline
yaml_file_path = "<your yaml file path>"pipeline_name = "<your pipeline name>"def main():
    pipeline = Pipeline.load(yaml_file_path, name=pipeline_name)
    
    # Create a pipeline if not exists    # If load after create, the pipeline is empty    if not pipeline.exists():
        pipeline.create()
        
    pipeline_instance_id = pipeline.launch()
    print(f"Pipeline Id: {pipeline.id}")
    print(f"Pipeline Instance Id: {pipeline_instance_id}")
    
if __name__ == "__main__":
    main()
```


<span id="创建一个简单的工作流，同时上传本地代码"></span>
### Create a simple pipeline while uploading local code


* YAML file can be referred to: [Define pipelines with YAML](https://docs.byteplus.com/docs/mlp/Define_pipelines_with_YAML)

* Prepare a `run.sh`file in the same directory as the python script


```python
#!/usr/bin/env bash
set -x
pwd
ls
env
```


<span id="配置工作流输入参数，支持在子任务中引用工作流的输入"></span>
### Configure pipeline input parameters to support referencing pipeline input in subtasks


* YAML file can refer to: [Define pipelines with YAML](https://docs.byteplus.com/docs/mlp/Define_pipelines_with_YAML)

* The Python code example is as follows:


```python
import os
import sys
from volcengine_ml_platform.pipeline import Pipeline
yaml_file_path = "<your yaml file path>"pipeline_name = "<your pipeline name>"def main():
    pipeline = Pipeline.load(yaml_file_path, name=pipeline_name)
    
    # Create a pipeline if not exists    # If load after create, the pipeline is empty    if not pipeline.exists():
        pipeline.create()
        
    inputs = {"command": "echo 'hello pipeline'"}
        
    pipeline_instance_id = pipeline.launch(inputs=inputs)
    print(f"Pipeline Id: {pipeline.id}")
    print(f"Pipeline Instance Id: {pipeline_instance_id}")
    
if __name__ == "__main__":
    main()
```


<span id="导出-yaml"></span>
## Export Yaml

<span id="导出一个工作流的最新配置"></span>
### Export the latest configuration of a pipeline

```python
import os
import sys
from volcengine_ml_platform.pipeline import Pipeline
pipeline_name = "<your pipeline name>"export_file_name = "<your export file name>"def main():
    pipeline = Pipeline.get(name=pipeline_name)
    if export_file_name:
        os.makedirs(os.path.dirname(export_file_name), exist_ok=True)
        pipeline.dump(export_file_name, type='yaml')
    else:
        pipeline.dump(type='yaml')
if __name__ == "__main__":
    main()
```


<span id="导出一个工作流实例的配置"></span>
### Export the configuration of a pipeline instance

```python
import os
import sys
from volcengine_ml_platform.pipeline import PipelineInstance
pipeline_instance_id = "<your pipeline instance id>"export_file_name = "<your export file name>"    
def main():
    pipeline_instance = PipelineInstance.get(pipeline_instance_id)
    if export_file_name:
        os.makedirs(os.path.dirname(export_file_name), exist_ok=True)
        pipeline_instance.dump(export_file_name, type='yaml')
    else:
        pipeline_instance.dump(type='yaml')
if __name__ == "__main__":
    main()
```
