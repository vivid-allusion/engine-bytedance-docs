---
title: "Performance"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Performance"
---

Efficient data loading and processing are key to improving overall training efficiency in large\-scale machine learning or deep learning projects. This article analyzes and compares the performance of various tools (TOS PyTorch Connector, TOS Python SDK, s3torchconnector) using TOS intranet domain and TOS accelerator in data loading scenarios, aiming to provide users with optimization guidance for data access strategies.

<span id="b96ce1e4"></span>
## Test description

Test scenario: Using TOS intranet domain and TOS accelerator respectively, simulate machine learning dataset loading scenarios with PyTorch to compare the end\-to\-end maximum reading performance.

Test data: used 2,000,000 images, averaging 120 KB each, totaling about 220 GB.

Test environment: Volcengine ecs.g3ine.24xlarge, 96C/384G, 144 Gbps intranet bandwidth.

<span id="bea7cde6"></span>
## Performance test

<span id="c2a2e84d"></span>
### Test parameters


|**Parameter** |**Value/configuration** |**Description** |
|---|---|---|
|batch_size |256 |Each data batch processes 256 samples. |
|num_workers |32 |Uses 32 worker processes to load data in parallel. |
|transform |```Python```<br>```def transform(item):```<br>```    data = item.read()```<br>```    # do operation```<br>```    return item.key, item.size```<br> |Data was not preprocessed, only read. |
|Application layer protocol |HTTP + persistent connection. |\- |


<span id="62befd1c"></span>
### **Dataset construction**


|**Installation package** |**Dataset** |**Description** |
|---|---|---|
|TOS PyTorch Connector |* TosMapDataset<br><br>* TosIterableDataset |tostorchconnector standard dataset, preloading enabled, concurrency 32. |
|Python SDK |* TosMapDataset<br><br>* TosIterableDataset |tostorchconnector integrates the Python SDK, allowing switching to use the Python SDK to build standard datasets. |
|s3torchconnector |* S3MapDataset<br><br>* S3IterableDataset |s3torchconnector standard dataset. |


<span id="c4061caa"></span>
### Test results


|**Installation package** |**dataset** |**TOS intranet domain latency** |**TOS intranet domain QPS** |**TOS Accelerator duration** |**TOS Accelerator QPS** |
|---|---|---|---|---|---|
|TOS PyTorch Connector<br><br> |TosMapDataset.from_urls<br><br> |123 seconds |16248 |49 seconds<br><br> |40993 |
||TosIterableDataset.from_urls |120 seconds |16668 |82 seconds |24261 |
||TosMapDataset.from_prefix<br><br> |274 seconds<br><br> |7273<br><br> |258 seconds |7718<br><br> |
||TosIterableDataset.from_prefix |168 seconds |11912 |164 seconds |12175 |
|Python SDK |TosMapDataset.from_urls<br><br> |2295 seconds<br><br> |868 |2324 seconds |858 |
||TosIterableDataset.from_urls |1374 seconds |1454 |1702 seconds |1175 |
||TosMapDataset.from_prefix<br><br> |2305 seconds<br><br> |865<br><br> |1856 seconds |1073 |
||TosIterableDataset.from_prefix |1365 seconds |1464 |1391 seconds |1436 |
|s3torchconnector |S3MapDataset.from_objects |2043 seconds |975 |680 seconds |2931 |
||S3IterableDataset.from_objects |1334 seconds |1498 |900 seconds |2222 |
||S3MapDataset.from_prefix |2477 seconds |804 |2210 seconds |901.12 |
||S3IterableDataset.from_prefix |1619 seconds |1234 |1272 seconds |1572 |


<span id="37ae63a0"></span>
## **Data analysis**

According to test results, TOS PyTorch Connector significantly outperforms Python SDK and s3torchconnector in data loading performance, with higher QPS and shorter data loading time.

<span id="563db069"></span>
### **In an intranet domain environment**

In the `from_urls` scenario, TosMapDataset’s QPS is about 20 times that of the Python SDK solution, and TosIterableDataset’s is about 12 times; in the `from_prefix` scenario, QPS also improves by approximately 8 times. Compared with s3torchconnector, TosIterableDataset.from_urls’ QPS is about 10 times that of S3IterableDataset.from_objects.

<span id="0781e316"></span>
### **After enabling the TOS accelerator**

Under various loading methods, TOS PyTorch Connector’s QPS increases across the board, with the `from_urls` method showing the most notable improvement of about 2 times; in contrast, the `from_prefix` method improves by only about 1 time, indicating the accelerator optimizes precise concurrent loading based on URL lists better.

<span id="923734ce"></span>
## **Test summary**

Using TOS PyTorch Connector in Python projects enables efficient streaming access to TOS objects, greatly improving data read/write performance in large\-scale training scenarios. To further optimize performance, you can combine the accelerator with TOS PyTorch Connector for training.
