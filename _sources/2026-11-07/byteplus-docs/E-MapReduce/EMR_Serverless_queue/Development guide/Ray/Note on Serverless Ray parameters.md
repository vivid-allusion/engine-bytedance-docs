---
title: "Note on Serverless Ray parameters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Note_on_Serverless_Ray_parameters"
---


|Parameter name |Example |Description |
|---|---|---|
|serverless.ray.entrypoint.bundle.path |tos://some\-bucket/demo.zip |Code ZIP package TOS address |
|serverless.ray.entrypoint.cmd |python test.py |Code entry point |
|serverless.ray.image |emr\-serverless\-online\-cn\-beijing.cr.volces.com/emr\-serverless\-ray/ray:2.30.0\-cu11.8.0\-py3.11\-ubuntu20.04\-233 |Ray image |
|serverless.ray.version |2.30.0 |Ray version of the image |
|serverless.customized.image.enabled |true |Whether to use a custom image. Set to true when using an image from the customer's account |
|serverless.ray.runtime.env.json |{"pip":["requests==2.26.0","pendulum==2.1.2","s3fs"],"env_vars":{"counter_name":"test_counter"}} |ray runtime env |
|serverless.ray.head.cpu |4 |Head CPU resource limit |
|serverless.ray.head.memory |16Gi |Head memory resource limit |
|serverless.ray.head.gpu.amount |1 |Head GPU resource limit, available when using GPU queue |
|serverless.ray.head.gpu.vendor |nvidia.com |Head GPU vendor, available when using GPU queue |
|serverless.ray.worker.cpu |4 |Worker CPU resource limit |
|serverless.ray.worker.memory |16Gi |Worker memory resource limit |
|serverless.ray.worker.gpu.amount |1 |Worker GPU resource limit, available when using GPU queue |
|serverless.ray.worker.gpu.vendor |nvidia.com |Worker GPU vendor, available when using GPU queue |
|serverless.ray.worker.replicas |1 |Number of workers. Initial number of workers when autoscaling is enabled |
|serverless.ray.enable.autoscaling |true |Whether to enable autoscaling |
|serverless.ray.worker.min.replicas |1 |Minimum number of workers for autoscaling |
|serverless.ray.worker.max.replicas |10 |Maximum number of workers for autoscaling |
|serverless.ray.autoscaler.options.idle.timeout.seconds |60 |Idle timeout threshold for autoscaler |
|serverless.ray.autoscaler.options.cpu |500m |Autoscaler CPU resource limit. Default is 500m, usually does not need to be changed |
|serverless.ray.autoscaler.options.memory |512Mi |Autoscaler memory resource limit. Default is 512Mi, usually does not need to be changed |
|serverless.ray.head.pod.env |[{"name":"ENV_K1","value":"ENV_V1"}] |Head environment variables |
|serverless.ray.worker.pod.env |[{"name":"ENV_K1","value":"ENV_V1"}] |Worker environment variables |
|serverless.ray.burst.vci |true |Whether to allow bursting to VCI. If enabled, pay\-as\-you\-go billing will be used. It is recommended to contact the Volcano EMR team when using this option |
|serverless.ray.node.selector |some\-node\-label |Ray node selection. It is recommended to contact the Volcano EMR team when using this option |
|serverless.ray.toleration |some\-node\-toleration |Ray taint toleration. It is recommended to contact the Volcano EMR team when using this option |
