---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/yarn_basic_usage"
---

<span id="_1-通过-rm-页面查看信息"></span>
## 1 Viewing information through the RM page

<span id="_1-1-使用前提"></span>
### 1.1 Prerequisites


1. To access the link, the ECS ID instance of the emr\-master\-1\-1 node must be bound to an Elastic Public IP. For details, see: [Bind a public IP](https://www.volcengine.com/docs/6401/68687)

2. In **Quickly configure server ports**, add the source address and corresponding port to the allowlist to continue accessing.

3. The username and password required for access can be set and viewed in "User management."


<span id="_1-2-访问入口"></span>
### 1.2 Access entry


1. Go to the **Cluster management \> Cluster list \> [specific cluster name]**  page to enter the cluster details.

2. In the navigation bar, click **Access link**, click **YARN UI access link**, and log in to **YARN ResourceManager WebUI** to view information.


<span id="_1-3-集群总览信息"></span>
### 1.3 Cluster overview information

Includes statistics on the number of apps in different states, statistics on the number of nodes in different states in the cluster, and resource statistics.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2f4bca056f441caeba776502326a7ca4) </span>

<span id="_1-4-集群节点信息"></span>
### 1.4 Cluster node information

Select the Nodes Tab in the upper left corner to view detailed information about cluster nodes.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_51883abadf9ff1f724d0f68bd29cfb90) </span>

<span id="_1-5-集群调度器-队列信息"></span>
### 1.5 Cluster scheduler & queue information

Select the Scheduler Tab in the upper left corner to view detailed information about cluster queues, displayed in a tree structure, as well as cluster scheduler event information.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_df9009314a1017f786d1693b70c9d9d7) </span>

<span id="_1-6-集群作业信息"></span>
### 1.6 Cluster job information

Select the Applications Tab in the upper left corner to view detailed job information.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3c3da0a11c608920e45d9e083ae0c6ac) </span>

<span id="_2-使用-yarn-命令行"></span>
## 2 Using YARN command line

After connecting remotely to the ECS ID instance of the emr\-master\-1\-1 node and entering the Yarn file directory, you can view the following information.

<span id="_2-1-yarn-application"></span>
### 2.1 Yarn application

**View job information. You can filter the results by job status and job type.** 

```Plain
yarn application -list [-appStates <States>] [-appTypes <Types>]
```


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3012b11a7d38e141ff46bf23348f6e06) </span>

**View jobs with a specified status**

```Plain
yarn application -status <ApplicationId>
```


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ba1fe05c25c9847fb28179c05c411ea5) </span>

**Kill a specified job**

```Plain
yarn application -kill <ApplicationId>
```


<span id="_2-2-yarn-logs"></span>
### 2.2 Yarn logs

**View application logs**

```Plain
yarn logs -applicationId <application ID> [-appOwner <AppOwner>] [-containerId <ContainerId>] [-nodeAddress <NodeAddress>]
```


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0d4b7b02c6b973e84a11d5a431a9bfcc) </span>

<span id="_2-3-yarn-jar"></span>
### 2.3 Yarn jar

**Generally used to run test or modified JAR files.** 

```Plain
格式：yarn jar [jarName] [mainClass] args
示例：yarn jar hadoop-mapreduce-client-jobclient-3.3.4-ve-1-tests.jar  TestDFSIO -write -nrFiles 1 -size 1GB -resFile out.out
```
