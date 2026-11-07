---
title: "Milvus vector retrieval performance test guide"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_vector_retrieval_performance_test_guide"
---

This topic explains how to use VectorDBBench to perform vector retrieval performance tests on a Milvus for VectorDB instance on Volcano Engine. The content covers test environment preparation, instance configuration, tool installation, test execution, and result verification to help you reproduce specified test scenarios in your own environment and establish a unified performance baseline.

<span id="t4WNENuH"></span>
## Applicable scenarios


* Evaluate Milvus’s retrieval throughput, response latency, and recall rate under large\-scale vector datasets.

* Reproduce specified performance test scenarios using unified datasets, index parameters, and concurrency configurations.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">We recommend that you perform tests in cloud environments within mainland China to minimize the impact of network conditions, client specifications, and data download sources on test results.</div>


* <div data-tips="true" data-tips-type="default">BytePlus Milvus for VectorDB currently does not support mainland China regions. We recommend that you use Volcano Engine Milvus for VectorDB to perform tests.</div>



<span id="ytbni69I"></span>
## Prerequisites


* A Milvus for VectorDB Dedicated instance has been created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance). To ensure comparable test results, configure the instance specifications as shown in the table below.

   
   |**Node type** |**CU type** |**Specification** |**Monthly subscription price (CNY)**  |**Description** |
   |---|---|---|---|---|
   |Metadata service |\- |1 Core 2 GiB |117 |\- |
   |Proxy |\- |8 cores 8 GiB |800 |\- |
   |Data node |\- |2 Core 4 GiB |234 |\- |
   |Index node |Capacity |Pooling nodes |Pay\-as\-you\-go |\- |
   |Query node |Capacity |48 Cores 48 GiB |5904 |Milvus for VectorDB uses a read\-write separation architecture and supports flexible scaling. Ensure sufficient Query Node resources based on query load and recall targets. |
   |Total price |\- |\- |7055 + pooling node<br><br>pay\-as\-you\-go |\- |
   

* The instance parameters have been adjusted. For more information, see [Modify instance configuration](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_the_instance_configuration). The instance parameters to adjust are shown in the following table.

   
   |**Parameter** |**Recommended value** |**Default value** |**Description** |
   |---|---|---|---|
   |dataCoord.sealPolicy.channel.growingSegmentsMemSize |65536 MB |4096 MB |Adjust the memory sealing threshold for growing segments. |
   |dataCoord.segment.diskSegmentMaxSize |1024000 MB |2048 MB |Adjust the maximum size of the disk segment. |
   |dataCoord.segment.maxSize |1024000 MB |2048 MB |Adjust the maximum size of a single segment. |
   |dataCoord.segment.maxBinlogFileNumber |2048 |32 |Adjust the maximum number of automatically sealed binlog files. |
   |queryNode.segcore.interimIndex.enableIndex |false |true |Control whether the growing segment builds an index. |
   |queryNode.mmap.growingMmapEnabled |true |false |Control whether to enable mmap for growing segments. |
   |queryNode.scheduler.maxReadConcurrentRatio |0.3 |1 |Concurrency multiplier for read tasks (search/query). |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">These parameters apply to scenarios involving large\-scale batch data import and pursuit of optimal retrieval performance; they reduce the impact of premature Segment sealing or insufficient write buffer on performance test results.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After modifying the parameters, wait for the instance to recover to Running status before continuing with subsequent tests.   </div>
   

* Created an Elastic Compute Service (ECS) instance to serve as the test client for VectorDBBench. For specific procedures, refer to [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The client specification directly affects performance testing capability. To avoid the client becoming a performance bottleneck, use <strong>ecs.g4al.16xlarge</strong> or a higher specification and select the Debian 12 operating system.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To reduce network latency impact on test results, deploy the ECS and Milvus instance in the same VPC and availability zone.   </div>
   


<span id="Pk2J9iUD"></span>
## Precautions

Test results may be affected by network environment, client performance, instance resource status, background tasks, and system load. For technical support, contact the [BytePlus technical support team](https://www.byteplus.com/en/contact/product).

<span id="o3NhMiCJ"></span>
## Procedure


1. Log on to ECS and prepare the Python virtual environment.

   After logging in to ECS, execute the following command to install Python virtual environment dependencies and create a test environment.

   ```Bash
   sudo apt update
   sudo apt install python3.11-venv
   python -m venv .test
   source .test/bin/activate
   ```
   

2. Download and install VectorDBBench.

   Run the following command to download VectorDBBench source code and install dependencies.

   ```Bash
   pip install vectordb-bench
   ```
   

3. Configure the dataset download source.

   Modify the dataset download source as needed based on the ECS region:

   * Regions in mainland China: we recommend that you switch to Aliyun OSS data source to improve download speed and stability.

      ```Bash
      export DATASET_SOURCE=AliyunOSS
      export DEFAULT_DATASET_URL="assets.zilliz.com.cn/benchmark/"
      ```
      

   * Regions outside mainland China: No modification needed.

4. Run performance tests.

   Download the `run_bench.sh` script provided by Volcengine; the script content is as follows.

   ```Bash
   #!/usr/bin/env bash
   
   set -euo pipefail
   usage() {
       cat <<EOF
   Usage:
     $0 <uri> <username> <password>
   Optional environment variables:
     CLUSTER_ENDPOINT       REST endpoint. Defaults to <uri>.
     TOKEN                  Bearer token. Defaults to <username>:<password>.
   EOF
   }
   if [[ $# -ne 3 ]]; then
       usage
       exit 1
   fi
   URI="$1"
   USERNAME="$2"
   PASSWORD="$3"
   CLUSTER_ENDPOINT="${CLUSTER_ENDPOINT:-${URI%/}}"
   CLUSTER_ENDPOINT="${CLUSTER_ENDPOINT%/}"
   TOKEN="${TOKEN:-${USERNAME}:${PASSWORD}}"
   command -v vectordbbench >/dev/null || {
       echo "vectordbbench not found in PATH" >&2
       exit 127
   }
   command -v curl >/dev/null || {
       echo "curl not found in PATH" >&2
       exit 127
   }
   alter_properties() {
       sleep 30
       echo "[$(date '+%F %T')] start alter_properties for VDBBench"
       curl --fail-with-body --show-error --silent \
           --request POST \
           --url "${CLUSTER_ENDPOINT}/v2/vectordb/collections/alter_properties" \
           --header "Authorization: Bearer ${TOKEN}" \
           --header "Request-Timeout: 5" \
           --header "Content-Type: application/json" \
           -d "{
       \"collectionName\": \"VDBBench\",
       \"properties\": {
           \"knowhere.enable_thp\": true,
           \"knowhere.enable_prefetch\": true
       }
   }"
       echo
       echo "[$(date '+%F %T')] alter_properties finished"
   }
   alter_properties &
   ALTER_PID=$!
   BENCH_RC=0
   vectordbbench milvusdiskann \
       --case-type Performance768D10M \
       --k 100 \
       --num-concurrency 1,10,25,50,100,150,200,250,300,350,400 \
       --uri ${URI} \
       --user-name ${USERNAME} \
       --password ${PASSWORD} \
       --search-list 260 \
       --replica-number 1 \
       --num-shards 1  || BENCH_RC=$?
   CURL_RC=0
   wait "${ALTER_PID}" || CURL_RC=$?
   if [[ "${CURL_RC}" -ne 0 ]]; then
       echo "alter_properties failed with exit code ${CURL_RC}" >&2
   fi
   if [[ "${BENCH_RC}" -ne 0 ]]; then
       exit "${BENCH_RC}"
   fi
   exit "${CURL_RC}"
   ```
   

   Execute the following command to start the performance test.

   ```Bash
   ./run_bench.sh <uri> <username> <password>
   #Replace the Milvus instance address, username, and password in the command with actual information. Example: ./run_bench.sh http://milvus-test.ivolces.com:19530 admin 'bytedance'.
   ```
   

5. Repeat the same test scenario.

   If data import and data loading are complete, add the `--skip-drop-old` and `--skip-load` parameters to the command to skip deleting old collections, reimporting data, and reloading data, thereby shortening test preparation time. The command example is as follows.

   ```Bash
   vectordbbench milvusdiskann \
       --case-type Performance768D10M \
       --k 100 \
       --num-concurrency 1,10,25,50,100,150,200,250,300,350,400 \
       --uri '${URI}' \
       --user-name '${USERNAME}' \
       --password '${PASSWORD}' \
       --search-list 260 \
       --replica-number 1 \
       --num-shards 1 \
       --skip-drop-old \
       --skip-load
   ```
   

6. Veryfy the results.

   After the test is complete, view the VectorDBBench output results and summarize key performance indicators according to different concurrency configurations.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that you focus on the following indicators:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">QPS: evaluate the system’s throughput under different concurrency levels.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Response latency: focus on the average, P95, and P99 indicators to assess response stability.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Recall rate: evaluate whether the retrieval accuracy meets business requirements.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To reduce the impact of environmental differences on test conclusions, keep the following conditions consistent when comparing results:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Milvus instance specifications and number of nodes.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Dataset, data size, and test scenarios.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">ECS client specifications, VPC, availability zone, and network link.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Whether to skip preparation steps such as data import and data loading.   </div>
