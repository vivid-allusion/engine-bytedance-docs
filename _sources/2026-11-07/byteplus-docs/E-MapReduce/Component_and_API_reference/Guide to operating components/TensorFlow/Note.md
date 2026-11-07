---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/tensorflow_note"
---

The EMR DataScientist cluster is a distributed training solution for Volcano Engine E\-MapReduce (EMR). By using ByteDance's self\-developed Primus training scheduling framework, you can easily perform distributed TensorFlow training tasks on YARN clusters.

Since Primus itself is a general\-purpose multi\-role distributed training scheduling framework, by configuring various training roles, Primus can support multiple built\-in distributed strategies in TensorFlow, such as Parameter Server.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17437f1c4c9f58a956679374f151139f.png) </span>

As shown in the figure above, the lifecycle of a Primus training job mainly consists of two phases: the **submission phase** and the **running phase**.


1. Submission phase:

   In the submission phase, you only need to prepare the Primus training configuration and the required training resources, such as training scripts. After you send the submission command, the Primus Client first uploads the specified training resources to HDFS, and then officially submits a distributed task to the YARN Cluster.

2. Running phase:

   After the Primus training job is successfully submitted, it enters the running phase.

   In this phase, Primus starts initializing the configured training roles, which includes requesting YARN Containers, downloading training resources, and finally executing the command specified for each role in the Primus training configuration. After all training roles are successfully started, the Primus training job begins to monitor all roles. When all roles meet the exit conditions defined in the Primus training configuration, the Primus training job exits successfully.
