---
title: "Image retrieval solution"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_retrieval_solution"
---

The AI data lake service provides efficient multimodal data processing capabilities. Its image retrieval pipeline, based on the Daft distributed computing framework and LAS image processing operators, is designed to help users efficiently extract high\-quality feature vectors from massive volumes of raw image data. This solution can convert image data of various formats into a unified image vector dataset that meets modern retrieval application standards, laying a solid foundation for building advanced image retrieval and multimodal applications.

<span id="efa63b0a"></span>
## **Background information**

With the explosive growth of digital content, images have become one of the core media for information transmission. Traditional image search methods based on tags (Tags) or metadata (Metadata) rely heavily on manual annotation, which is not only costly but also cannot capture the deep semantic content of images, making it difficult to achieve precise similarity search.

The core of modern applications such as image\-based search and similarity recommendation is **semantic retrieval**, that is, matching based on an understanding of the image content itself. This relies on converting images into mathematical representations that capture their semantic meaning—**feature vectors (Embeddings)** . However, building an efficient image vectorization workflow faces many challenges:


* **Input standardization**: Massive image data varies greatly in size, resolution, aspect ratio, and format. Directly processing such data can impact model efficiency and the consistency of feature extraction.

* **High\-quality feature extraction**: Advanced vision models (such as Vision Transformer) are required to extract high\-dimensional vectors from images that accurately capture rich semantics such as content, style, and texture.

* **Scalable processing efficiency**: Image processing is a compute\-intensive task. When dealing with millions, tens of millions, or even hundreds of millions of images, high\-performance distributed processing and GPU acceleration capabilities are essential.


The LAS image retrieval pipeline solution is specifically designed to address the above challenges, providing an end\-to\-end automated workflow from image preprocessing to vectorized output.

<span id="267d27c3"></span>
## **Applicable scenarios**


* **Image retrieval systems**: Suitable for building large\-scale image retrieval (search by image) systems, enabling fast and accurate similar image search and product recommendation through image vectorization.

* **Cross\-modal retrieval**: Suitable for cross\-modal retrieval applications such as image\-text matching, searching for text by image, and searching for images by text. The generated image vectors can be used to calculate similarity with text vectors in the same semantic space.

* **Content review and clustering**: Suitable for scenarios such as image deduplication, clustering of similar content, and copyright image recognition, enabling efficient analysis of large volumes of images through vector similarity.


<span id="d7257651"></span>
## **Key features**


* **End\-to\-end processing workflow**: Supports the complete pipeline from raw images to final vector features, covering two core steps: image normalization and resampling, and feature vectorization.

* **Efficient image preprocessing**: Integrates professional image resampling operators, supports multiple interpolation methods, and can standardize image size and resolution in batches to provide standardized input for feature extraction.

* **Advanced image vectorization**: Based on advanced vision Transformer models such as DINOv2\-Large, extracts high\-quality, highly discriminative image feature vectors.

* **Flexible storage formats**: Supports multiple image input formats (URL, Base64, binary) and outputs standardized vector data for direct use by downstream applications.

* **Distributed processing capability**: Leveraging the parallel scheduling mechanism provided by Daft, enables high\-performance processing and vectorization of large\-scale image data.

* **GPU acceleration support**: The image feature extraction process supports GPU acceleration, which can improve the processing efficiency of large\-scale image data by up to tenfold.

* **Multimodal compatibility**: The generated image vectors are compatible with the vector spaces of mainstream text models and can be directly used for multimodal applications such as image\-text matching.


<span id="6772e8b5"></span>
## **Prerequisites**


* Registered and [Byteplus account](https://www.Byteplus.com/). To log in to the for the first time, complete and [real-name verification](https://console.byteplus.com/user/authentication/) in advance.

* Enabled and [AI Data Lake Service product](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

* Created and general queue and compute queue.

* Created and development machine.

* Uploaded the original images to the specified bucket in and Object Storage (TOS).


<span id="8da1a87b"></span>
## **How it works**

This solution adopts a two\-stage pipeline architecture, consisting of two core steps: **image preprocessing** and **image vectorization**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e98570a072a54b7caed201ed1c0717a3~tplv-goo7wpa0wc-image.image) </span>

<span id="14679bf3"></span>
### **Core processing workflow**


|Stage |Function description |Detailed explanation |Operator list |
|---|---|---|---|
|**Image resampling** |Standardize image size, resolution, and format to normalize image input. |Adjust input images of different sizes and resolutions to a standardized size suitable for visual model input (such as 224x224 pixels), and perform resampling using the high\-quality lanczos method. |ImageResample |
|**Image vectorization** |Extract high\-dimensional image feature vectors using advanced visual models. |With the help of pre\-trained Vision Transformer models such as DINOv2\-Large, extract high\-dimensional feature vectors (such as 1024 dimensions) that represent the global semantics of the standardized images. |ImageViTEmbedding |


<span id="d656efa0"></span>
### Case demonstration

After the pipeline runs, a structured dataset is generated, which includes the location of the original image, its unique identifier, the path to the standardized/resampled image, and the generated high\-dimensional feature vector:


|image_id |image_tos_path |resampled_image_tos_path |image_embedding (Feature Vector) |
|---|---|---|---|
|1 |tos://.../test_image/1.png |tos://.../resample_image/1_resample.png |[0.0119, \-0.0407, \-0.0320, ...] (1024 dimensions) |
|10 |tos://.../test_image/10.png |tos://.../resample_image/10_resample.png |[0.0072, \-0.0637, \-0.0245, ...] (1024 dimensions) |
|11 |tos://.../test_image/11.png |tos://.../resample_image/11_resample.png |[\-0.0042, \-0.0214, \-0.0077, ...] (1024 dimensions) |
|12 |tos://.../test_image/12.png |tos://.../resample_image/12_resample.png |[\-0.0374, 0.0204, \-0.0034, ...] (1024 dimensions) |
|13 |tos://.../test_image/13.png |tos://.../resample_image/13_resample.png |[\-0.0177, \-0.0294, \-0.0456, ...] (1024 dimensions) |
|14 |tos://.../test_image/14.png |tos://.../resample_image/14_resample.png |[\-0.0214, \-0.0406, \-0.0510, ...] (1024 dimensions) |
|15 |tos://.../test_image/15.png |tos://.../resample_image/15_resample.png |[\-0.0094, \-0.0334, \-0.0482, ...] (1024 dimensions) |
|16 |tos://.../test_image/16.png |tos://.../resample_image/16_resample.png |[0.0033, \-0.0347, \-0.0520, ...] (1024 dimensions) |
|17 |tos://.../test_image/17.png |tos://.../resample_image/17_resample.png |[\-0.0119, \-0.0439, \-0.0630, ...] (1024 dimensions) |
|18 |tos://.../test_image/18.png |tos://.../resample_image/18_resample.png |[\-0.0109, \-0.0371, 0.0124, ...] (1024 dimensions) |
|19 |tos://.../test_image/19.png |tos://.../resample_image/19_resample.png |[\-0.0062, \-0.0085, \-0.0566, ...] (1024 dimensions) |
|2 |tos://.../test_image/2.png |tos://.../resample_image/2_resample.png |[\-0.0152, \-0.0316, \-0.0306, ...] (1024 dimensions) |
|20 |tos://.../test_image/20.png |tos://.../resample_image/20_resample.png |[0.0025, \-0.0325, \-0.0477, ...] (1024 dimensions) |
|3 |tos://.../test_image/3.png |tos://.../resample_image/3_resample.png |[\-0.0236, \-0.0017, \-0.0299, ...] (1024 dimensions) |
|4 |tos://.../test_image/4.png |tos://.../resample_image/4_resample.png |[\-0.0461, \-0.0657, 0.0395, ...] (1024 dimensions) |
|5 |tos://.../test_image/5.png |tos://.../resample_image/5_resample.png |[\-0.0125, \-0.0032, \-0.0459, ...] (1024 dimensions) |
|6 |tos://.../test_image/6.png |tos://.../resample_image/6_resample.png |[0.0016, 0.0033, \-0.0614, ...] (1024 dimensions) |
|7 |tos://.../test_image/7.png |tos://.../resample_image/7_resample.png |[\-0.0086, \-0.0223, \-0.0530, ...] (1024 dimensions) |
|8 |tos://.../test_image/8.png |tos://.../resample_image/8_resample.png |[\-0.0287, \-0.0412, \-0.0445, ...] (1024 dimensions) |
|9 |tos://.../test_image/9.png |tos://.../resample_image/9_resample.png |[0.0209, \-0.0530, \-0.0639, ...] (1024 dimensions) |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6739613e187d484d9eaa5c9bc125e6fb~tplv-goo7wpa0wc-image.image" width="1682px" /></div>


<span id="262c053f"></span>
## **Operation procedure**

<span id="bffefc4c"></span>
### **Step 1: Development and debugging**


1. On the development machine of the AI Data Lake Service, write a Python script to define and execute the image processing pipeline. This script uses the Daft framework to chain LAS image processing operators, implementing the entire process from loading images to outputting vectors.


**Code reference**

The following is the complete pipeline implementation code, demonstrating how to load image data from TOS and perform resampling and vectorization in sequence.

```Python
from __future__ import annotations

import logging

import daft
from daft import col
from daft.las.functions.image.embedding.image_vit_embedding import ImageViTEmbedding
from daft.las.functions.image.image_resample import ImageResample
from daft.las.functions.udf import las_udf
from daft.las.io.tos import TOSConfig

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s",
    handlers=[
        logging.StreamHandler(),
    ],
)

logger = logging.getLogger(__name__)

def run_pipeline(input_tos_dir: str):
    input_s3_dir = input_tos_dir.replace("tos://", "s3://", 1)
    tos_config = TOSConfig.from_env()
    IO_CONFIG = daft.io.IOConfig(s3=tos_config.to_s3_config())
    model_path = "/opt/las/models"
    logger.info("图像检索pipeline开始运行...")
    
    df = daft.from_glob_path(
        f"{input_s3_dir}/*.png",
        io_config=IO_CONFIG,
    )
    
    df = df.with_column(
        "image_tos_path",
        col("path").str.replace("s3://", "tos://")
    )
    df = df.with_column(
        "image_id",
        col("path").str.split("/").list.get(-1).str.replace(".png", "")
    )
    df = df.select("image_tos_path", "image_id")
    
    logger.info("图像文件加载完成: %d 条记录", df.count_rows())
    
    logger.info("开始图像重采样...")
    df = df.with_column(
        "resampled_image",
        las_udf(
            ImageResample,
            construct_args={
                "image_suffix": ".png",
                "tos_dir": "tos://tos_bucket/image_retrieval/resample_image/",
                "local_dir": "",
                "image_src_type": "image_url",
                "target_size": [224, 224],
                "target_dpi": [72, 72],
                "method": "lanczos",
            },
            num_gpus=0,
            batch_size=32,
            concurrency=1,
        )(col("image_tos_path")),
    )
    df.collect()
    logger.info("图像重采样完成: %d 条记录", df.count_rows())
    
    logger.info("开始图像向量化...")
    df = df.with_column(
        "image_embedding",
        las_udf(
            ImageViTEmbedding,
            construct_args={
                "image_src_type": "image_base64",
                "dtype": "float32",
                "batch_size": 32,
                "model_path": model_path,
                "model_name": "facebook/dinov2-large",
                "use_cls_token_embedding": True,
                "rank": 0,
            },
            num_gpus=1,
            batch_size=32,
            concurrency=1,
        )(col("resampled_image")["base64"]),
    )
    df.collect()
    logger.info("图像向量化完成: %d 条记录", df.count_rows())
    
    df = df.with_column(
        "resampled_image_tos_path",
        col("resampled_image")["image_path"]
    )
    df = df.exclude("resampled_image")
    df.show()

if __name__ == "__main__":
    input_tos_dir = "tos://tos_bucket/image_retrieval/test_image"
    run_pipeline(input_tos_dir)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Code asset</strong>: The complete pipeline script can be downloaded here: <a href="https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/experience_center/image_retrieval/image_retrieval_pipeline_show.py">image_retrieval_pipeline_show.py</a>.</div>



2. Check the processing results and adjust the pipeline script based on the results to meet image processing requirements.


After executing the pipeline, you will obtain a Daft DataFrame containing the image identifier, original path, resampled path, and image feature vector.

**Sample log output:** 

```Bash
2025-08-21 07:30:10,INFO - 图像检索 Pipeline 开始运行...
2025-08-21 07:30:12,INFO - 图像文件加载完成: 150 条记录
2025-08-21 07:30:13,INFO - 开始图像重采样...
2025-08-21 07:31:05,INFO - 图像重采样完成: 150 条记录
2025-08-21 07:31:06,INFO - 开始图像向量化...
2025-08-21 07:32:30,INFO - 图像向量化完成: 150 条记录
2025-08-21 07:32:31,INFO - Pipeline 执行完毕，最终结果如下：
```


**Sample output data (** **`df.show()`**  **):** 


|image_tos_path |image_id |image_embedding |resampled_image_tos_path |
|---|---|---|---|
|tos://.../test_image/cat_01.png |cat_01 |[0.135, \-0.244, ... (1024 dims)] |tos://.../resample_image/cat_01.png |
|tos://.../test_image/dog_01.png |dog_01 |[\-0.087, 0.512, ... (1024 dims)] |tos://.../resample_image/dog_01.png |
|tos://.../test_image/car_01.png |car_01 |[0.641, 0.098, ... (1024 dims)] |tos://.../resample_image/car_01.png |
|... |... |... |... |


<span id="9b4109af"></span>
### **Step 2: Full\-scale task deployment**

After debugging the processing pipeline on the development machine, you can save it as a custom image and create batch tasks in **AI Data Lake Service \-\> Task Management**. With this task, you can perform large\-scale, automated vectorization processing on millions of images stored in TOS, producing data for upper\-layer retrieval applications.
