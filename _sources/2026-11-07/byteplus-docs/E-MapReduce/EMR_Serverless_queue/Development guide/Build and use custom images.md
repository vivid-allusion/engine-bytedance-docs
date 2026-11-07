---
title: "Build and use custom images"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Build_and_use_custom_images"
---

## Build images

### Region note

The currently supported regions are as follows.

|Chinese name |English name |
|---|---|
|North China |cn\-beijing |
|East China |cn\-shanghai |
|South China |cn\-guangzhou |
|Asia Pacific Southeast (Johor) |ap\-southeast\-1 |

### Base image \- Spark

When using, replace `{region}` with the English name of your region. Refer to the **region note**.

|Image name |Size |Other note |
|---|---|---|
|emr\-serverless\-online\-{region}.cr.volces.com/public/spark:3.5.1\-py3.12\-ubuntu20.04\-1005 |4.82GiB |* Spark version: 3.5.1<br><br>* Python：3.12<br><br>* Hadoop version: 3.3.4<br><br>* Operating system: Ubuntu 20.04 |

### Base image \- Ray

When using, replace `{region}` with the English name of your region. Refer to the region **note**.

|Ray version |Image name |Size |Dependency package note |
|---|---|---|---|
|2.33.0 |emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.33.0\-cu11.8.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |6.67GiB |Java 8Hadoop 3.3.4 |
||emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.33.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |1.75GiB |Java 8Hadoop 3.3.4 |
|2.30.0 |emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.30.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |1.76GiB |Java 8Hadoop 3.3.4 |
||emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.30.0\-cu11.8.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |6.67GiB |Java 8Hadoop 3.3.4 |
||emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.30.0\-cu12.1.0\-py3.11\-ubuntu20.04\-211\-1.5.0 |6.66GiB |Java 8Hadoop 3.3.4 |
|2.22.0 |emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.22.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |1.66GiB |Java 8Hadoop 3.3.4 |
||emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.22.0\-cu11.8.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |6.56GiB |Java 8Hadoop 3.3.4 |
|2.9.3 |emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.9.3\-py3.9\-ubuntu20.04\-1.2.0 |1.66GiB |Java 8Hadoop 3.3.4 |
||emr\-vke\-public\-{region}.cr.volces.com/emr/ray:2.9.3\-cu11.8.0\-py3.9\-ubuntu20.04\-1.2.0 |6.56GiB |Java 8Hadoop 3.3.4 |

For other Ray base images, see: [Ray image list](https://docs.byteplus.com/docs/E-MapReduce/Ray_image_list).

### Build custom images

Build custom images based on the above EMR Serverless base images, then upload them to your private repository.

For example, suppose the Dockerfile content is as follows:

```SQL
FROM emr-serverless-online-cn-beijing.cr.volces.com/public/spark:3.5.1-ubuntu20.04-python3.10-1180

RUN apt-get update -y
RUN apt-get install build-essential -y
RUN pip install fasttext==0.9.3 -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip install fasttext-langdetect==1.0.5 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

Use the following command to build a custom image:

```SQL
docker build -f Dockerfile -t {私有镜像仓库域名}/test/spark:3.5.1-ubuntu20.04-python3.10-1180 .
```

Then upload it to the user's image repository.

```SQL
docker push {私有镜像仓库域名}/test/spark:3.5.1-ubuntu20.04-python3.10-1180
```

## Use custom images

### Spark job parameters

* EMR Serverless Console \- Job Management \- Submit Job.

```SQL
-- Enable custom images
set serverless.customized.image.enabled=true;
-- Set customer's private image
set spark.kubernetes.container.image={客户自定义镜像};
```

* PySpark job.

```Bash
# Use custom images
'serverless.customized.image.enabled': 'true',
'spark.kubernetes.container.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:xxx'
```

### Ray job parameters

* EMR Serverless Console \> Job Management \> Submit Job.

```Bash
# Use custom images
set serverless.customized.image.enabled=true;
set serverless.ray.image=emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:xxx;
```

* python Submit Job.

```Bash
# Use custom images
'serverless.customized.image.enabled': 'true',
'serverless.ray.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:xxx'
```
