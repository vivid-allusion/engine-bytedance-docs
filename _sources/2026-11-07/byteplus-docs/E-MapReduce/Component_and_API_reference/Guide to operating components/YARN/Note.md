---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/yarn_note"
---

<span id="概述"></span>
# Overview

YARN (Yet Another Resource Negotiator) is the resource management system for Hadoop clusters and a core component of the Hadoop ecosystem. It is primarily responsible for resource management, job scheduling, and monitoring within Hadoop clusters.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c669a20b3de98ea2a9fc4c9214f3d392) </span>

The information about YARN components is as follows:


* ResourceManager: A global resource manager responsible for cluster resource management and scheduling, allocating resources for jobs running on YARN.

* NodeManager: Responsible for node resource management, monitoring, and job execution. It periodically reports the resource usage of this node and the running status of each Container to RM, and also receives and processes various requests from AM, such as starting or stopping Containers.

* ApplicationMaster: Each job submitted by a user contains an AM. Its main functions are:

   * Negotiating with the RM scheduler to obtain resources, represented by Containers.

   * Further allocating the obtained Containers to internal tasks.

   * Communicating with NM to start or stop tasks.

   * Monitoring the running status of all tasks, and reapplying for resources to restart tasks when task execution fails.

* Container: The resource abstraction in YARN, encapsulating multidimensional resources on a node, such as CPU, memory, and more.

* YARN Client: Responsible for submitting jobs.
