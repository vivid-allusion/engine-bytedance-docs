---
title: "AI profiling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/AI_Profiling"
---

When you deploy large language models (LLM) in a VKE cluster, you can analyze the AI profiling results of specified containers. This facilitates detection and optimization throughout the LLM life cycle, including training, inference, and optimization. This topic describes how to configure the AI profiling feature.

<span id="uPn4Giwd"></span>
## Background

With the rise of LLM, the requirements for performance detection and optimization in AI training and inference are rapidly growing. For LLM running on GPU nodes, online performance analysis of GPU containers is especially important. AI profiling supports non\-intrusive data collection and analysis by leveraging eBPF and dynamic process injection technologies. It is tailored for Kubernetes container scenarios and can perform online detection on container processes that run GPU tasks.

The following table describes the collection items that are supported by AI profiling.


|Collection item |Description |
|---|---|
|CUDA |The ** ** CUDA kernel functions. This item can be used for monitoring and analyzing the status of the underlying GPU resources for LLM, such as GPU busy time, distribution of GPU kernel functions, and timeline analysis (such as the analysis of a training step, including data loading, forward propagation, backward propagation, and optimizer update). |
|PyTorch |The PyTorch operators can be used for **accurately identifying model performance issues** and providing data support for optimizing model efficiency, accelerating training and inference, and reducing resource consumption. The following information is included:<br><br><br>* **Identify operator\-level performance issues for targeted optimization**: PyTorch models consist of many operators, such as convolution, matrix multiplication, and activation functions. The latency and resource usage significantly vary based on different operators.<br><br>* **Optimize hardware utilization to unleash computing potential**: The performance of AI tasks is limited by hardware (CPU/GPU) utilization, and the execution method of operators directly affects hardware efficiency.<br><br>* **Verify optimization results to quantify improvement potential**: Profiling can be used to verify the results, whether you manually optimize operators, such as rewriting CUDA extensions, or use PyTorch built\-in optimization tools, such as torch.compile, or upgrade hardware, such as upgrading from V100 to A100. |
|Python |The Python process call stack. As a dynamic language, Python has flexible and variable code execution paths, such as conditional branches and dynamic function calls. The call stack can anchor scattered performance data, such as latency and resource usage, to specific code locations. For complex AI systems, such as large model training and distributed inference, call stack analysis is required for solving performance issues across modules and hardware. For example:<br><br><br>* **Inefficient code identification**: The call stack records the calling relationships of functions and operators. Combined with latency data, it can directly locate the specific location of inefficient code or the source of redundant calls.<br><br>* **Abnormality identification**: LLMs often contain multiple layers of nested function calls, where modules such as the model layer, loss function, optimizer, and data loader are intertwined. By restoring the call sequence, they can identify and locate abnormal branches.<br><br>* **Optimization basis**: The depth and complexity of the call stack directly reflect whether the code design is reasonable. By identifying inefficient code and anomalies, the call stack can provide a basis for simplifying redundant traces and modularizing code. |


<span id="TYS2e0Sl"></span>
## Usage limits

Containers for which you want to configure AI profiling need to meet the following environment and version requirements.


|Requirement categories |Environment requirements |
|---|---|
|Basic environment |* glibc version 2.17 and later.<br><br>* libstdc++ version 6.0.19 and later.<br><br>* Python 3.7 and later, with pip installed. |
|Additional requirements for PyTorch |* glibc 2.28 and later.<br><br>* libstdc++ 6.0.25 and later. |
|Toolchain |* g++ version 8 and later. |
|Add\-on version |* PyTorch: 1.13, 2.0, 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 2.7, and 2.8.<br><br>* Python: 3.7, 3.8, 3.9, 3.10, 3.11, 3.12, and 3.13.<br><br>* CUDA: 11.2, 11.3, 11.4, 11.5, 11.6, 11.7, 11.8, 12.0, 12.1, 12.2, 12.3, 12.4, 12.5, 12.6, 12.8, 12.9, and 13.0. |


<span id="mqjBVs1m"></span>
## Prerequisites

TOS has been activated, and a TOS bucket has been created in the same region as the target VKE cluster. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

<span id="PNGzDpta"></span>
## Procedure

<span id="WgO9n1zc"></span>
### Step 1: Configure diagnosis


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **AI Profiling**. On the page that appears, click **Diagnosis settings**.

5. Select the created TOS bucket and configure the subdirectory. The TOS bucket and directory are used to store data collected by AI profiling.

   
   |Parameters |Description |
   |---|---|
   |Bucket name |Select the created TOS bucket from the drop\-down list. |
   |Subdirectory |Specify the path where the packet capture results are saved in the TOS bucket. If this parameter is not specified, the path is `/`. |
   

6. Click **Confirm**.


<span id="bAwcoJOP"></span>
### Step 2: Create a diagnosis task


1. Click **Create diagnosis job** and configure the task details.

   
   |Parameters |Description |
   |---|---|
   |Namespace |Select the namespace where the diagnosis task target is located. |
   |Pods |Select the target pod of the packet capture task. |
   |Container |Select the target container for the packet capture task. |
   |Collection item |Configure the collection items of the collection target. Valid values:<br><br><br>* **cuda**: the CUDA kernel function. The data of the target container can be collected only if it uses a GPU.<br><br>* **pytorch**: the PyTorch operator<br><br>* **python**: the Python process call stack |
   |Collection duration |Specify the detection duration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you set the detection duration to 60 seconds or less. AI profiling collects data in real time. If it collects too much data, the memory and disk may be insufficient.</div><br> |
   

2. Click **Confirm**.


<span id="IJH0fsza"></span>
## Validating results


1. After the diagnosis task is configured, the system starts diagnosing. When the task state changes to **Finish**, it indicates that the diagnosis task is complete.

2. Click the task name to go to the task details page. Click **Download** in the **Diagnosis result** section to download the AI profiling diagnostic result file to your on\-premises computer. You can upload the profiling file to the [Perfetto online tool](https://ui.perfetto.dev/) for visualized analysis.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2810e585ab8ce2accd4f5526bf18f2e9.png) </span>
