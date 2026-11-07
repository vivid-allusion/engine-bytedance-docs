---
title: "Application scenarios"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Application_scenarios"
---

This topic describes the business scenarios suitable for Elastic File Storage (EFS).

<span id="PmvEmAiw"></span>
## Intelligent driving

Centralizes PB\-level sensor data (images/point clouds); supports efficient annotation, model training, and simulation validation for massive datasets; accelerates algorithm iteration.


* Data collection: Raw files usually reach hundreds of PBs. If low\-cost storage is required, TOS is recommended.

* Data processing: During data processing, the temporary data generated can usually reach about 10 PB. In this case, EFS is recommended for higher access performance. The data flow capability provided by EFS enables seamless data flow between file storage and object storage. It can continuously move raw files and extracted/annotated data to achieve optimal cost performance.

* Model training: The amount of GPU data supported by the training framework and the number of GPU cards available in a cluster from cloud providers are limited. Therefore, training clusters often need to be split into multiple ones. Correspondingly, multiple high performance storage clusters are required; and each cluster requires tens to hundreds of GBps throughput. In this case, vePFS is recommended due to the total capacity across clusters reaching tens to hundreds of PB.

* Software simulation: Storage requirements at this stage are modest, usually at hundreds of TBs scale. However, performance is still required. In this case, EFS is recommended. Its data flow capability can achieve optimal cost performance.

* Log storage: Model training generates a large number of random write logs. In this case, EFS is recommended.


<span id="XhsuwDRQ"></span>
## Integrated training and inference

EFS breaks down traditional barriers between training (model learns data and generates parameters) and inference (model predicts based on the parameters). By integrating software and hardware, dynamic resource scheduling, and opening up data pipelines, EFS realizes efficient lifecycle collaboration.


* Significant inference demand fluctuation: Peak and off\-peak traffic on live streaming platforms can differ more than 10 times. This may lead to resource waste during off\-peak times.

* Diverse training tasks: In addition to large\-scale pre\-training, there are also lightweight tasks such as fine\-tuning (adapting with small datasets for specific scenarios) and incremental training (updating models with new data). These tasks share resources with inference.

* Disconnected data pipelines: Training outputs (model files) must be delivered to inference, while inference results (such as user feedback and prediction errors) should loop back to training. These pipelines are lengthy and complex to manage.


By sharing the same high\-performance persistent file storage (EFS), high\-performance read and write capability are obtained; resource sharing and second\-level mounting are achieved.

<span id="XhsuwDRQ"></span>
## Traditional shared file storage business requirements

Teams can collaborate efficiently by sharing files; precise permissions over control can be achieved to ensure security; high performance supports smoothly accessing large files like design and rendering.

&nbsp;
