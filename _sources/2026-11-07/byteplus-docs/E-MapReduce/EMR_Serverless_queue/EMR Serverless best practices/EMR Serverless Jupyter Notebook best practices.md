---
title: "EMR Serverless Jupyter Notebook best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Jupyter_Notebook_best_practices"
---

Jupyter Notebook is an open\-source interactive development tool that allows you to write and execute code instantly in a web interface and view results in real time. For more information, refer to the [official Jupyter documentation](https://jupyter.org/).

Jupyter supports integration with multiple kernels. This article describes how to build an efficient development environment for interacting with EMR Serverless Spark using a self\-hosted Jupyter instance.

<span id="cfde2bce"></span>
## Deploy Jupyter

<span id="71fa7631"></span>
### Install Jupyter Notebook

```Python
pip3 install 'jupyter_server>=2.14.0' 'notebook>=7.2.0'
```


<span id="6edd0f33"></span>
### Start Jupyter Notebook

```C++
export KERNEL_USERNAME=notebook
export KERNEL_LAUNCH_TIMEOUT=300
export KERNEL_EXTRA_SPARK_OPTS="--conf serverless.spark.access.key={your_access_key} --conf serverless.spark.secret.key={your_secret_key} --conf las.execute.queuename={your_emr_queue}  --conf spark.dynamicAllocation.maxExecutors=50"

jupyter notebook --ip 0.0.0.0 --port {jupyter_port} --allow-root --gateway-url=http://{jupyter_gateway_endpoint} --GatewayClient.auth_token={jupyter_gateway_token}
```


The parameters involved are explained as follows:


|Parameter |Required |Note ||
|---|---|---|---|
|KERNEL_USERNAME |Yes |Set to "notebook"; no changes needed ||
|KERNEL_LAUNCH_TIMEOUT |Yes |Kernel startup timeout ||
|KERNEL_EXTRA_SPARK_OPTS |Yes |Used to set additional parameters. **Supports EMR Serverless parameters and Spark open\-source parameters (refer to**[常见参数](https://docs.byteplus.com/docs/undefined/6854fb250079c10520e58096#47e6f08d) **)** . The format is `--conf k1=v1 --conf k2=v2`. The following parameters can be set:<br><br><br>* `serverless.spark.access.key`: Required. Your account Access Key<br><br>* `serverless.spark.secret.key`: Required. Your account Secret Key<br><br>* `las.execute.queuename`: EMR Serverless queue name<br><br>* `spark.dynamicAllocation.minExecutors`: Minimum number of executors, default is 1<br><br>* `spark.dynamicAllocation.initialExecutors`: Initial number of executors, default is 1<br><br>* `spark.dynamicAllocation.maxExecutors`: Maximum number of executors, default is 30 ||
|jupyter_port |Yes |Specify the port number to start ||
|jupyter_gateway_endpoint |Yes |Jupyter gateway service address, refer to the following:<br><br><br>* endpoint：[https://notebook-eg.emr.ap-southeast-1.bytepluses.com](https://docs.byteplus.com/docs/E-MapReduce/109085) ||
|jupyter_gateway_token |Yes |Jupyter gateway token, provided by EMR Serverless ||


After the Notebook is started, you can see the following log information:

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
### (Optional) Configure internal endpoint


* Create an endpoint


Private network \- Private connection \- Endpoint \- Create endpoint \- Select service name to add \- Verify \- Configure private network \- Do not enable DNS name.


* Select available service: `notebook-eg-clb`

* Private network & subnet: It is recommended to use the same private network and subnet as the ECS node where the Jupyter Server is located.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8709dc08c6bb4625b476bab0da82a111~tplv-goo7wpa0wc-image.image" width="3132px" /></div>



* View endpoint domain name:


This is the `jupyter_gateway_endpoint` configured when starting the Jupyter Server.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e84ec6e506b24fa5992c450315f1b8ee~tplv-goo7wpa0wc-image.image" width="2636px" /></div>



* Security group inbound rules: Must be open to the ECS node where the Jupyter Server is deployed.


<span id="b4116105"></span>
### Common parameters


|Parameter type |Parameter key |Note |Default value |
|---|---|---|---|
|**Driver related** |`spark.driver.memory` |Driver heap memory size |12g |
||`spark.driver.memoryOverhead` |Driver off\-heap memory size |4g |
||`spark.driver.cores` |Number of CPU cores for the driver program |4 |
||`spark.driver.maxResultSize` |Maximum size of results returned by the driver |3g |
||`spark.driver.extraJavaOptions` |Driver JVM parameters | |
|**Executor related** |`spark.executor.cores` |Number of CPU cores per Executor |4 |
||`spark.executor.memory` |Memory size per Executor |12g |
||`spark.executor.memoryOverhead` |Off\-heap memory size per Executor |4g |
||`spark.executor.instances` |Number of Executor instances (dynamic allocation is enabled by default, so this parameter does not need to be set) |1 |
|**Dynamic allocation related** |`spark.dynamicAllocation.enabled` |Enable dynamic allocation |true |
||`spark.dynamicAllocation.minExecutors` |Minimum number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum number of Executors |30 |
|**File read parallelism** |`spark.sql.files.maxPartitionBytes` |File size for each Map task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operations |200 |
|**AQE** |`spark.sql.adaptive.enabled` |Adaptive execution switch, includes automatic adjustment of parallelism and optimizations for resolving data skew |true |
||`spark.sql.adaptive.maxNumPostShufflePartitions` |Maximum dynamic parallelism; for tasks with large shuffle volumes, increasing this value can reduce the data processed by each task, for example, 1024 |500 |
||`spark.sql.adaptive.minNumPostShufflePartitions` |Lower limit for the number of shuffle partitions dynamically adjusted by AQE |5 |
|**Other open\-source Spark parameters** |[Please refer to the official documentation](https://spark.apache.org/docs/latest/configuration.html) |||
|**EMR Serverless parameters** |`serverless.spark.access.key` |Your account Access Key | |
||`serverless.spark.secret.key` |Your account Secret Key | |
||`serverless.spark.tos.bucket` |Specify a TOS bucket to upload your local jar files. When the Spark task starts, it will load jar files from this TOS bucket. If your files already exist in the TOS bucket, this parameter can be left blank | |
||`spark.jars` |Comma\-separated jar file paths. Spark will load these jar files at runtime. Both local files and TOS files are supported. | |
||`spark.archives` |Comma\-separated archive files, which will be loaded into the Spark runtime working directory. Both local files and TOS files are supported. | |
||`spark.files` |Comma\-separated other files, which will be loaded into the Spark runtime working directory. Both local files and TOS files are supported. | |


<span id="3287cded"></span>
## Jupyter submits EMR Serverless Spark tasks

<span id="4e078f24"></span>
### Start EMR Serverless Spark Kernel


1. On the home page, click [View] \-\> [Open JupyterLab] to access Jupyter.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f794e6fcb574c35b96ba2b4d472bd27~tplv-goo7wpa0wc-image.image" width="1716px" /></div>



2. Create a new `EMR Serverless Spark Kernel`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de00fb81bd194e65a22b6b3140f333ee~tplv-goo7wpa0wc-image.image" width="1241px" /></div>



3. Status confirmation: You can confirm whether it has started by checking the status button in the upper right corner.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/616ee96125eb47da9c45dfd12b3208d3~tplv-goo7wpa0wc-image.image" width="1910px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the status changes to Idle, it indicates a successful startup. You can now execute interactive queries.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84b8bb2028ca441ca5d4e6b9549739fc~tplv-goo7wpa0wc-image.image" width="1623px" /></div>


<span id="ad094800"></span>
### Use PySpark for interactive queries

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using PySpark, the following system variables are already initialized by default. Do not modify: spark, sc, sql.</div>


```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder.enableHiveSupport().getOrCreate()
sc = spark.sparkContext
sql = spark.sql
```



1. Query database and table information.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/446a3516ae6b41b8a992ebba3daaf0f7~tplv-goo7wpa0wc-image.image" width="858px" /></div>



2. Read and write tables.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700efb6e4b684a058b963993a64799c4~tplv-goo7wpa0wc-image.image" width="1088px" /></div>



3. Query the `EMR Serverless Spark` task corresponding to the current kernel session.


```Python
spark.conf.get("spark.app.id")
```


In the returned result `bq-500785400`, `500785400` is the `EMR Serverless` task ID. Go to **EMR Console \> Job Management \> Serverless Jobs**, search for [Instance ID] to find the corresponding task. You can view the task log, `Spark UI`, and other information.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4231ef5e6de43e2bc09dab6f9b22810~tplv-goo7wpa0wc-image.image" width="769px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bffbf5e34f54b4f85902044ceb4f3b3~tplv-goo7wpa0wc-image.image" width="1889px" /></div>
