---
title: "Mixed text and image layout"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mixed_text_and_image_layout"
---

<span id="87feac99"></span>
## Scenario description

A web page typically consists of a large block of text description and several embedded images and videos. When scraping a web page, the text is usually extracted and constructed as a dataset, then the image hyperlinks are parsed and the image links are scraped separately to build a new image dataset.

Therefore, a web page corresponds to one text and N images (the same applies to videos, but here the scenario is simplified to images only).

In general, the text dataset is used for data operations in NLP tasks, while the image dataset is used for data processing in CV tasks.

However, certain training tasks require a mixed layout of the entire web page's text and images for training. At this point, it is necessary to associate the text dataset and image dataset using docID and output the results.

<span id="de610593"></span>
## Current solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d0bb379d4d4bc29c304efc3f3fd5ac~tplv-goo7wpa0wc-image.image) </span>

The image dataset is generally stored using Webdataset, and computation is performed using the Spark engine.


1. First, a sampling and filtering operation is performed on the image dataset.

2. Then, the image dataset is aggregated by docID.

3. Finally, a join operation is performed with the text dataset to complete the data merging.


<span id="8911fd28"></span>
## Lance solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b4081e6a3d84e1daca527395e96697e~tplv-goo7wpa0wc-image.image) </span>

Similar to the traditional data workflow, computation still uses Spark, but the image dataset is stored in Lance format.


1. Sampling + AGG + Join do not retrieve the Image content; only the RowId in Lance is used as a reference.

2. After the join is completed, the output structure is (docID, TEXT, List).

3. Finally, a value replacement step is added. This step is essentially a LookUp process, where the Image field is located using RowId and replaced accordingly.


<span id="7993e964"></span>
## Solution comparison


|Dimension |Current solution |Lance solution |
|---|---|---|
|Filtering + sampling |Requires streaming all data and then filtering, **<ins>resulting in severe IO amplification</ins>** |* Columnar storage allows skipping irrelevant row data using meta information |
|Aggregation + join |* The Image field resides in memory, occupying Spark resources and easily causing **<ins>memory OOM</ins>**, resulting in task retries<br><br>* The Image field undergoes shuffle operations, occupying large amounts of disk storage and network bandwidth, and may cause **<ins>IO failures</ins>**, resulting in task retries or failures<br><br>* Aggregation plus join results in two Shuffle operations in total, causing memory and IO issues to multiply. |* Only RowId is passed, which is of Long type and consistent with ordinary fields, so there are no memory or IO issues. |
|Replacement value |This step does not exist. |* Sink step, streaming operation: after processing each image, it can be written out in a streaming manner, with no memory issues.<br><br>* PyLance has an object storage backpressure mechanism, can retry individual requests, controls retry granularity, and prevents triggering Spark Task, Stage, or Job retries. |
