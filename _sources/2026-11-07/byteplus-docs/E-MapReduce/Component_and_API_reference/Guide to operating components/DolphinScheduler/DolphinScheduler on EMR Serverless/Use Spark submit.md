---
title: "Use Spark submit"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Using_Spark_submit"
---

This article describes how to use DolphinScheduler to integrate with EMR\-Serverless and use the `spark-submit` \*\*\*\* command to submit EMR\-Serverless Spark jobs.

<span id="2b22d893"></span>
# Configure Spark\-submit

<span id="e8d3dddb"></span>
## Log in to the Worker (ECS) node

Refer to the following content to remotely log in to the worker\-server node of DolphinScheduler in the EMR cluster, and install the toolkit in the corresponding node instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">All nodes of the Worker\-server need to install the corresponding toolkit.</div>



1. Log in and go to the service list of the EMR cluster to view the worker\-server node of DolphinScheduler.

2. Click the corresponding node. After being redirected to the ECS instance page, remotely log in to the ECS instance. After logging in, refer to the following content to download and install the Spark submit toolkit.


<span id="61976917"></span>
## Download and install the toolkit

The following is an example command for downloading and installing the toolkit.

```Bash
#!/bin/bash

set -ex

# Default value
DEFAULT_REGION="cn-beijing"
DEFAULT_VERSION="1.0.0.5"
SERVERLESS_SPARK_HOME="/opt/emr/serverless_spark"

# Check parameter count
if [ "$#" -lt 3 ]; then
    echo "please input param: <access-key> <secret-key> <bucket> [region]"
    exit 1
fi

# Get parameters
ACCESS_KEY=$1
SECRET_KEY=$2
BUCKET=$3
REGION=${4:-$DEFAULT_REGION}  # Use the default value if region is not provided

mkdir -p "$SERVERLESS_SPARK_HOME"

# Switch to installation directory
cd "$SERVERLESS_SPARK_HOME"

# Define download link and file name
FILE_NAME="serverless-spark-submit-${DEFAULT_VERSION}.tar.gz"
URL="https://serverless-spark.tos-cn-beijing.ivolces.com/spark/submit/emr.spark.serverless_spark_submit_${DEFAULT_VERSION}.tar.gz"
INSTALL_DIR="$SERVERLESS_SPARK_HOME/serverless-spark-submit-${DEFAULT_VERSION}"

mkdir -p "$INSTALL_DIR"

# Download file
if wget -O "$FILE_NAME" "$URL"; then
    echo "Download successful."
else
    echo "Download failed."
    exit 1
fi

# Extract file
if tar -xzf "$FILE_NAME" -C "$INSTALL_DIR"; then
    echo "Extraction successful."
else
    echo "Extraction failed."
    exit 1
fi

# Configure environment variables
echo "export SERVERLESS_SDK_HOME=${INSTALL_DIR}" >> /etc/profile

# Define configuration file path
CONF_FILE="${INSTALL_DIR}/conf/spark-defaults.conf"

# Clear file content
> "$CONF_FILE"

# Append content to configuration file
cat <<EOL >> "$CONF_FILE"
spark.app.name=serverless-spark-task
serverless.spark.endpoint=https://emr-serverless.cn-beijing.volcengineapi.com
serverless.spark.service=emr_serverless
serverless.spark.access.key=$ACCESS_KEY
serverless.spark.secret.key=$SECRET_KEY
serverless.spark.tos.bucket=$BUCKET
serverless.spark.region=$REGION
EOL

chown -R dolphinscheduler:dolphinscheduler $SERVERLESS_SPARK_HOME

echo "Please run 'source /etc/profile' to make the changes effective."
```


The key steps and parameter Note are as follows.


1. Set default values.

   
   |Key parameters |Parameter notes |
   |---|---|
   |DEFAULT_VERSION |This is set to the latest version of the current Spark submit tool. In the example, it is set to the current latest version: `1.0.0.5`. |
   

2. Enter parameters.

   Enter the authentication account AK/SK information, the TOS bucket name for job storage, region, and other information as prompted. The next steps will automatically populate the required parameter values based on the input parameters here.

   
   |Key parameters |Parameter notes |
   |---|---|
   |`access-key`&`secret-key` |BytePlusAccount`AK` and `SK` |
   |`bucket` |BytePlusTOS's bucket name |
   |`region` |Default is `cn-beijing`, others include (`cn-shanghai`, `cn-guangzhou`, `ap-southeast-1`) |
   

3. Define the download link and file name.

   
   |Key parameters |Parameter notes |
   |---|---|
   |`URL` |The URL is the download link for the toolkit. If your machine is already connected to the internal Volcano Engine network, you can use the internal domain name for the download (URL) address. Otherwise, use the external domain name.<br><br><br>* Internal domain name: `serverless-spark.tos-cn-beijing.ivolces.com`<br><br>* External domain name: `serverless-spark.tos-cn-beijing.volces.com` |
   

4. After the script is executed, all deployment artifacts are located in the $SERVERLESS_SPARK_HOME directory and belong to the dolphinscheduler user.


<span id="4bb8ce6d"></span>
## Verify installation results

When spark\-submit submits a local job, the job will be automatically uploaded to TOS. You can refer to the following content to run a demo job locally to verify whether the Spark submit toolkit is installed correctly.


1. Create a test file: demo.py. An example of the test file content is as follows.

   ```Python
   from pyspark.sql import SparkSession
   # Create SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   spark.sql("select 1").show()
   spark.stop()
   ```
   

2. Run the demo. Usually, you can configure parameters such as the task name and the main class to execute the task when using Submit Job. For a full description of all parameters, see the [提交参数](https://docs.byteplus.com/docs/E-MapReduce/Using_Spark_submit#09bacf0d) section below.

   * The demo.py file is on the local machine:

      ```Bash
      ${SERVERLESS_SDK_HOME}/bin/spark-submit --tos-endpoint tos-cn-beijing.ivolces.com --properties-file ${SERVERLESS_SDK_HOME}/conf/spark-defaults.conf ${path}/demo.py 
      ```
      

   * The demo.py file has been stored in TOS:

      ```Shell
      ${SERVERLESS_SDK_HOME}/bin/spark-submit --properties-file ${SERVERLESS_SDK_HOME}/conf/spark-defaults.conf tos://${bucket}/${path}/demo.py
      ```
      

3. Check the submission log to verify whether the toolkit can be used normally.

&nbsp;


<span id="9b8e8e8a"></span>
# Create a Serverless Spark job

The following describes the core operations for creating common types of jobs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The submission methods for pyspark and spark jar are consistent, with slight differences in submission parameters. For details, refer to the <a href="https://docs.byteplus.com/docs/E-MapReduce/Using_Spark_submit#09bacf0d">提交参数</a> section below.</div>


* <div data-tips="true" data-tips-type="warning">The Submit Job can be stored in tos or in the DolphinScheduler resource center. These two options differ slightly in the submission parameters.</div>


* <div data-tips="true" data-tips-type="warning">To avoid interference from any existing Spark environments, Spark conf is explicitly specified in this document.</div>



<span id="b8ed648f"></span>
## Scenario 1: Shell Task

<span id="0eec37bc"></span>
### Submit local job


* Operation entry/example:

   * Submit in ECS instance:

      ```JSON
      ${SERVERLESS_SDK_HOME}/bin/spark-submit --tos-endpoint tos-cn-beijing.ivolces.com --properties-file ${SERVERLESS_SDK_HOME}/conf/spark-defaults.conf ${path}/demo.py
      ```
      

   * Submit in DolphinSchedule interface:

&nbsp;


<span id="6642b332"></span>
### Submit job from resource center


* Configuration Note: When submitting a job in this way, you do not need to care about the path of the execution file.

* Operation entry:


<span id="4b6e9179"></span>
### TOS job submission


* Configuration Note: Set the job path to the TOS address

* Operation entry/example:

   * Submit in ECS instance:

      ```JSON
      ${SERVERLESS_SDK_HOME}/bin/spark-submit --tos-endpoint tos-cn-beijing.ivolces.com --properties-file ${SERVERLESS_SDK_HOME}/conf/spark-defaults.conf tos://${tos path}/demo.py
      ```
      

   * Submit in DolphinSchedule interface:

&nbsp;


<span id="bd1ac632"></span>
## Scenario 2: Spark task

<span id="bed608d5"></span>
### Preparation

Before submitting a Spark task, you need to configure whether to use SPARK1 or SPARK2.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Dolphin (up to version 3.1.9) Spark Task still requires selecting SPARK1 or SPARK2, meaning that the underlying system will use <code>${SPARK_HOME1}/bin/spark-submit</code> or <code>${SPARK_HOME2}/bin/spark-submit</code> to submit the job. Therefore, you need to pre\-configure <code>SPARK_HOME1</code> or <code>SPARK_HOME2</code> in <code>/etc/profile</code> so that Serverless spark\-submit can be used correctly.</div>


For example, to use SPARK1, the configuration example is as follows.

```Shell
// 使用 SPARK1
echo "SPARK_HOME1=${SERVERLESS_SDK_HOME}" >> /etc/profile
```


<span id="fda7c158"></span>
### Submit Job


1. Upload the job file to the resource center.

2. Create a job.

&nbsp;


<span id="39dcf871"></span>
## Scenario 3: PySpark task

<span id="4a47fe46"></span>
### Recommended parameter settings

Submitting jobs using spark\-defaults.conf can be cumbersome. To submit jobs with different ak/sk or other parameters, you can explicitly specify parameters, for example:

```Bash
${SERVERLESS_SDK_HOME}/bin/spark-submit --access-key-id ${AK} --access-key-secret ${SK} --files ${file1,file2,file3} ...
```


<span id="4e8c4b6c"></span>
### Local SQL job submission


* Task file example: pyspark_demo_sql.py

   ```Python
   from pyspark.sql import SparkSession
   
   # Create SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   spark.sql("select 1").show()
   
   spark.stop()
   ```
   

* Submit task

   ```Bash
   spark-submit \
     --conf spark.executor.memory=4g \
     tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py
   ```
   


<span id="2d9125dd"></span>
### TOS job submission


* Job file example

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dca8d53755b64864a7339ff1c41737b0~tplv-goo7wpa0wc-image.image" name="pyspark_demo_tos.py">pyspark_demo_tos.py</Attachment>
   

* Submit task

   ```Bash
   spark-submit \
     --conf spark.executor.memory=4g \
     --files tos://emr-qa/lei/demo/spark/rel.txt \
     tos://emr-qa/lei/demo/spark/pyspark_demo_tos.py \
     --inputFile tos://emr-qa/lei/demo/spark/rel.txt --outputFile tos://emr-qa/lei/lei_db/people_table_1.csv
   ```
   


<span id="47995e97"></span>
# Cancel Dolphin task

When canceling a dolphin task, to simultaneously cancel the remote EMR Serverless task, you need to configure [DolphinScheduler shell kill application practices](https://docs.byteplus.com/docs/E-MapReduce/DolphinScheduler_shell_kill_application_practices).

<span id="097da933"></span>
# Refer to the appendix: task parameter Note


* You can configure global task parameters in the toolkit's spark\-defaults.conf.

* You can also explicitly specify parameters when submitting a job. These parameters are job\-level and take precedence over the configuration in spark\-defaults.conf.

* For the list of supported parameters and detailed parameter Note, see [Parameter description](https://docs.byteplus.com/docs/E-MapReduce/Spark-submit_tool_usage_instructions#7b130b83).
