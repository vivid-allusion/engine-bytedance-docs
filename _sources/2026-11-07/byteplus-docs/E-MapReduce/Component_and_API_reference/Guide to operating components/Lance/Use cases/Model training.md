---
title: "Model training"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Model_training"
---

<span id="ac3d30a3"></span>
## Scenario description

In the complete workflow of data preprocessing, data that has undergone cleaning, labeling, and augmentation ultimately flows into the model training stage. Model training can be mainly divided into two categories based on specific scenarios and requirements: base model training and fine\-tuning training.

Base model training typically uses large\-scale, diverse datasets, with data volumes often reaching the TB or even PB level. This training mode requires the use of specialized distributed training platforms, leveraging the parallel computing capabilities of multiple machines and multiple GPUs to complete the process. The training platform must possess the following key capabilities: First, it should support efficient storage and fast access to large\-scale data, usually through distributed file systems (such as HDFS) or object storage (such as S3); second, it must have robust data preprocessing capabilities, including data loading, format conversion, and feature extraction; finally, it needs to support seamless integration with distributed training frameworks (such as TensorFlow and PyTorch).

In contrast, fine\-tuning training is usually based on a pre\-trained base model and performs targeted optimization using a smaller\-scale dataset. For these training scenarios, the requirements for the data platform are reflected in two key capabilities: first, efficient dataset loading, which must support fast reading of various data formats (such as CSV, JSON, and Parquet) as well as parallel processing of data loading; second, comprehensive data shuffling capabilities, including random shuffle and distributed shuffle, to ensure uniform data distribution and stable training. Additionally, the data platform must support advanced features such as data augmentation and data splitting to meet the needs of different training scenarios.

In practical applications, the data platform must flexibly configure data processing strategies according to the characteristics of different training scenarios. For base model training, batch processing is typically required to ensure data processing throughput; for fine\-tuning training, more emphasis is placed on real\-time data processing and response speed to enable rapid iterative optimization of model performance.

<span id="5654cf6e"></span>
## Current solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d44a0a5675e3400aadea811a1c2b6730~tplv-goo7wpa0wc-image.image) </span>

The common data formats for fine\-tuning models are Parquet or WebDataset for image datasets, and jsonl for text datasets.

When training data using the PyTorch Dataloader interface, all of this data is loaded into memory and shuffled.

The data is then sent to the GPU for training according to the model's batch size.

<span id="37faee41"></span>
## Lance solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/669a1dd897244dd49bc66f0dde9ae155~tplv-goo7wpa0wc-image.image) </span>

Lance can integrate with the PyTorch Dataloader, and by using Lance data with the random iteration algorithm provided by the PyTorch Dataloader, shuffle operations can be performed directly.

<span id="a0de0309"></span>
## Solution comparison


|**Dimension** |**Current solution** |**Lance solution** |
|---|---|---|
|Data loading |* Data must be loaded into memory before training can begin. |* Training can begin as soon as RowId allocation is completed. |
|Data randomness |* Randomness is limited to a single node and cannot achieve full dataset randomness unless the entire dataset can be loaded on a single machine. |* Global shuffle, independent of single node resources. |
|Memory consumption |* High memory consumption, as the entire dataset must be loaded into memory. |* Low memory consumption, only the batch size occupies memory. |
|GPU utilization |* During the loading phase, the GPU remains idle. |* The IO phase is distributed throughout the training process, so there is no prolonged GPU waiting time. |
|Storage medium |* Typically stored on local disks; special adaptation is required to use object storage. |* Seamless switching between local and object storage modes. |


<span id="b92e811f"></span>
## Sample code

Reference[Train a CLIP multimodal model using the Lance data format](https://docs.byteplus.com/docs/E-MapReduce/109335)
