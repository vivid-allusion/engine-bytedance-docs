---
title: "EMR Serverless Jupyter Notebook Best Practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Jupyter_Notebook_Best_Practices"
---

Jupyter Notebook is an open source interactive power builder that allows you to write and executable code in real time in a web interface and view the results in real time. For more information, please refer to the [official Jupyter documentation ](https://jupyter.org/).

Jupyter supports integration with multiple kernels. This article describes how to build an efficient development environment that interacts with EMR Serverless Spark.

<span id="cfde2bce"></span>
## Deploy Jupyter

<span id="71fa7631"></span>
### Install Jupyter Notebook

```Python
pip3 install 'jupyter_server>=2.14.0' 'notebook>=7.2.0'
```


<span id="6edd0f33"></span>
### Launch Jupyter Notebook

```C++
export KERNEL_USERNAME=notebook
export KERNEL_LAUNCH_TIMEOUT=300
export KERNEL_EXTRA_SPARK_OPTS="--conf serverless.spark.access.key={your_access_key} --conf serverless.spark.secret.key={your_secret_key} --conf las.execute.queuename={your_emr_queue}  --conf spark.dynamicAllocation.maxExecutors=50"

jupyter notebook --ip 0.0.0.0 --port {jupyter_port} --allow-root --gateway-url=http://{jupyter_gateway_endpoint} --GatewayClient.auth_token={jupyter_gateway_token}
```


The parameters involved are described as follows:


|parameter |Is it required? |explain ||
|---|---|---|---|
|KERNEL_USERNAME |Yes |Write it as "notebook", no need to change it. ||
|KERNEL_LAUNCH_TIMEOUT |Yes |Kernel startup timeout ||
|KERNEL_EXTRA_SPARK_OPTS |Yes |Used to set additional parameters, **support EMR Serverless parameters and Spark open source parameters (refer to** [常见参数](https://docs.byteplus.com/docs/undefined/6854fb250079c10520e58096#47e6f08d) **)**  , the setting format is `--conf k1 = v1 --conf k2 = v2`, the filling parameters are as follows:<br><br><br>* `Serverless.spark.access.key`: Required, your account Access Key<br><br>* `Serverless.spark.secret.key`: Required, your account Secret Key<br><br>* `Las.execut.queuename`: EMR Serverless queue name<br><br>* `spark.dynamicAllocation.minExecutors`: minimum number of executors, default 1<br><br>* `spark.dynamicAllocation.initialExecutors`: Number of executors initialized, default 1<br><br>* `spark.dynamicAllocation.maxExecutors`: Maximum number of executors, default 30 ||
|jupyter_port |Yes |Specify the port number for startup ||
|jupyter_gateway_endpoint |Yes |Jupyter gateway service address, refer to the following:<br><br><br>* endpoint：https://notebook\-eg.emr.ap\-southeast\-1.bytepluses.com ||
|jupyter_gateway_token |Yes |Jupyter Gateway Token, provided by EMR Serverless ||


After the notebook starts, you can see the following log information:

```Shell
[I 2025-05-22 20:11:54.327 ServerApp] jupyter_lsp | extension was successfully linked.
[I 2025-05-22 20:11:54.330 ServerApp] jupyter_server_terminals | extension was successfully linked.
[I 2025-05-22 20:11:54.333 ServerApp] jupyterlab | extension was successfully linked.
[I 2025-05-22 20:11:54.337 ServerApp] notebook | extension was successfully linked.
[I 2025-05-22 20:11:54.507 ServerApp] notebook_shim | extension was successfully linked.
[I 2025-05-22 20:11:54.519 ServerApp] notebook_shim | extension was successfully loaded.
[I 2025-05-22 20:11:54.521 ServerApp] jupyter_lsp | extension was successfully loaded.
[I 2025-05-22 20:11:54.522 ServerApp] jupyter_server_terminals | extension was successfully loaded.
[I 2025-05-22 20:11:54.523 LabApp] JupyterLab extension loaded from /usr/local/lib/python3.10/site-packages/jupyterlab
[I 2025-05-22 20:11:54.523 LabApp] JupyterLab application directory is /usr/local/share/jupyter/lab
[I 2025-05-22 20:11:54.524 LabApp] Extension Manager is 'pypi'.
[I 2025-05-22 20:11:54.547 ServerApp] jupyterlab | extension was successfully loaded.
[I 2025-05-22 20:11:54.549 ServerApp] notebook | extension was successfully loaded.
[I 2025-05-22 20:11:54.550 ServerApp] Serving notebooks from local directory: /root
[I 2025-05-22 20:11:54.550 ServerApp] Jupyter Server 2.16.0 is running at:
[I 2025-05-22 20:11:54.550 ServerApp] http://localhost:8123/tree?token=e978588f8f0a685013be07d1c110af0f246e2b3b3f101784
[I 2025-05-22 20:11:54.550 ServerApp]     http://127.0.0.1:8123/tree?token=e978588f8f0a685013be07d1c110af0f246e2b3b3f101784
[I 2025-05-22 20:11:54.550 ServerApp] Kernels will be managed by the Gateway server running at:
[I 2025-05-22 20:11:54.550 ServerApp] http://115.190.41.195:80
[I 2025-05-22 20:11:54.550 ServerApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 2025-05-22 20:11:54.553 ServerApp] 
    
    To access the server, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/jpserver-403812-open.html
    Or copy and paste one of these URLs:
        http://localhost:8123/tree?token=e978588f8f0a685013be07d1c110af0f246e2b3b3f101784
        http://127.0.0.1:8123/tree?token=e978588f8f0a685013be07d1c110af0f246e2b3b3f101784
Refresh (1 sec) http://localhost:8123/tree?token=
e978588f8f0a685013be07d1c110af0f246e2b3b3f101784

This page should redirect you to a Jupyter application. If it doesn't, click
here to go to Jupyter.
```


<span id="d1dca0f0"></span>
### (Optional) Configure Intranet Endpoints


* Create end point node


Private network \- private connection \- end point node \- create end point node \- select service name add \- verify \- configure private network \- do not enable DNS name.


* Select available services: `notebook-egg-clb`.

* Private Networks & Subnets: The same private networks and subnets as the ECS node where the Jupyter Server is located are recommended.

* View end point node domains:


The `jupyter_gateway_endpoint`configured for Jupyter Server at startup.


* Security Group Direction Rule: Requires to be open to ECS nodes deployed by Jupyter Server.


<span id="b4116105"></span>
### common parameters


|Parameter type |Parameter key |explain |default value |
|---|---|---|---|
|**Driver related** |`spark.driver.memory` |Driver Heap Memory Size |12g |
||`spark.driver.memoryOverhead` |Driver out\-of\-heap memory size |4g |
||`spark.driver.cores` |Number of CPU Cores for Drivers |4 |
||`spark.driver.maxResultSize` |The maximum size of the result returned by the driver |3g |
||`spark.driver.extraJavaOptions` |Driver JVM parameters | |
|**Executor related** |`spark.executor.cores` |CPU Cores per Executor |4 |
||`spark.executor.memory` |Memory size per Executor |12g |
||`spark.executor.memoryOverhead` |Out\-of\-heap memory size per Executor |4g |
||`spark.executor.instances` |Number of Executor instances (dynamic is enabled by default, no need to set this parameter) |1 |
|**dynamic correlation** |`spark.dynamicAllocation.enabled` |Whether to turn on dynamic |true |
||`spark.dynamicAllocation.minExecutors` |Minimum Number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum Number of Executors |30 |
|**file read parallelism** |`spark.sql.files.maxPartitionBytes` |Map the file size of a single task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operation |200 |
|**AQE** |`spark.sql.adaptive.enabled` |Adaptive execution switch, including automatic adjustment of parallelism, solution skewed data and other optimizations |true |
||`spark.sql.adaptive.maxNumPostShufflePartitions` |Dynamic maximum parallelism, for tasks with a large amount of shuffle, appropriate increase can reduce the amount of data per task, such as 1024 |500 |
||`spark.sql.adaptive.minNumPostShufflePartitions` |AQE Lower limit when dynamically adjusting the number of shuffle partitions |5 |
|**Other open\-source Spark parameters** |[Please refer to the official website](https://spark.apache.org/docs/latest/configuration.html) |||
|**EMR Serverless Parameters** |`serverless.spark.access.key` |Your Account Access Key | |
||`serverless.spark.secret.key` |Your Account Secret Key | |
||`serverless.spark.tos.bucket` |Specify a TOS bucket to upload your local jar files to, from which the Spark task will load when it starts. If your file already exists in the TOS bucket, this parameter cannot be filled in | |
||`spark.jars` |Comma\-delimited jar file paths that will be loaded by the Spark runtime, either local or tos files | |
||`spark.archives` |Comma\-delimited archive files will be loaded into the working directory of the Spark runtime, either local or tos files | |
||`spark.files` |Other files separated by commas will be loaded into the working directory of the Spark runtime, either local or tos files | |


<span id="3287cded"></span>
## Jupyter submits EMR Serverless Spark task

<span id="4e078f24"></span>
### Launch EMR Serverless Spark Kernel


1. Click [View] \- \> [Open JupyterLab] on the homepage to visit Jupyter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d99cc9cee2e2433fb00b282cb9739bf2~tplv-goo7wpa0wc-image.image) </span>


2. Create a new `EMR Serverless Spark Kernel`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de00fb81bd194e65a22b6b3140f333ee~tplv-goo7wpa0wc-image.image" width="1241px" /></div>



3. Start status confirmation: You can confirm whether to start through the status button in the upper right corner.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/616ee96125eb47da9c45dfd12b3208d3~tplv-goo7wpa0wc-image.image" width="1910px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the state changes to Idle, the startup is successful, and interactive queries can be executed.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84b8bb2028ca441ca5d4e6b9549739fc~tplv-goo7wpa0wc-image.image" width="1623px" /></div>


<span id="ad094800"></span>
### Interactive Queries with PySpark

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using PySpark, the following system variables are initialized by default and should not be modified: spark, sc, and sql.</div>


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.enableHiveSupport().getOrCreate()
sc = spark.sparkContext
sql = spark.sql
```



1. Query database & table information.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/446a3516ae6b41b8a992ebba3daaf0f7~tplv-goo7wpa0wc-image.image" width="858px" /></div>



2. Read and write table.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700efb6e4b684a058b963993a64799c4~tplv-goo7wpa0wc-image.image" width="1088px" /></div>



3. Query the `EMR Serverless Spark`task corresponding to the current kernel session.


```Python
spark.conf.get("spark.app.id")
```


Return results `bq-500785400`in the `500785400`is the `EMR Serverless`task ID, enter the **EMR console \> job management \> Serverless job** , search for [instance ID] to get the corresponding task, you can view the task log, `Spark UI`and other content.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4231ef5e6de43e2bc09dab6f9b22810~tplv-goo7wpa0wc-image.image" width="769px" /></div>
