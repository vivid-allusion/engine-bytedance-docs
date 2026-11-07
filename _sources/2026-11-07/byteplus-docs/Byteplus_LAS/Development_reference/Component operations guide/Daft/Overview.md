---
title: "Overview"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Overview"
---

<span id="af9fe3e6"></span>
## Introduction to Daft

DAFT is the world's first **distributed computing engine natively supporting multimodal data processing**, breaking the traditional ETL paradigm and offering:

**Unified multimodal data abstraction + Python/Rust native API + distributed execution engine** as a three\-in\-one solution, enabling seamless transition from raw data to AI features.

Daft is positioned to provide end\-to\-end processing capabilities for enterprise\-level multimodal data lakes. It eliminates the dependence of traditional tools on single data types, seamlessly integrating dozens of data formats such as text, images, video, audio, JSON, Parquet, HuggingFace Dataset, and more, automating the entire process from data ingestion, cleaning, and transformation to analysis and modeling. Whether it is product images and user reviews on e\-commerce platforms or video and point cloud data in intelligent driving, Daft can aggregate scattered multimodal information into structured "data assets," providing a consistent data processing foundation for subsequent AI training and business analysis.

<span id="79ac3f9b"></span>
## Daft technical advantages

Daft originates from a design philosophy focused on multimodal data processing, supports native multimodal data types, helps users handle petabyte\-scale multimodal data, seamlessly integrates with existing machine learning systems, and delivers top\-tier data processing performance.


1. **Native multimodal processing**: Within a single unified framework, by supporting native multimodal data types such as image, embedding, and tensor, it offers built\-in operations like image decoding and vector similarity calculation, avoiding lengthy workflows found in traditional solutions.

2. **Heterogeneous resource scheduling**: Daft can automatically allocate optimal heterogeneous resources based on the computational characteristics of tasks, achieving seamless coordination of CPU and GPU computing tasks within the same workflow, thereby maximizing resource utilization and significantly improving overall computational performance.

3. **Rust\-powered performance**: Leveraging a Rust kernel, it provides vectorized execution and asynchronous I/O capabilities, processing the same queries with less memory and supporting petabyte\-scale data processing.

4. **Seamless ML ecosystem integration**: Seamlessly integrates existing machine learning (ML) workloads, providing compatible interfaces for workloads such as PyTorch, NumPy, Pandas, and HuggingFace, making it easy to connect with existing systems.

5. **Deep data lake collaboration**: Supports multiple cloud storage media (such as S3, BytePlus TOS, and more), seamlessly connects to modern data lake formats (such as Apache® Iceberg, Hudi, Delta Lake, and more), offers deep integration with the Lance format for AI data lakes, and supports enterprise\-grade catalogs (such as Unity, AWS Glue, and more).

> Apache Iceberg, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


6. **Python UDF data processing capability:**  Utilizes zero\-copy capability powered by Apache® Arrow, enabling direct processing of multimodal data within UDFs, eliminating data movement overhead and improving processing speed.


```Python
@daft.udf(return_dtype=daft.DataType.python())
def crop_images(images, crops, padding=0):
    cropped = []
    for img, crop in zip(images, crops):
        x1, x2, y1, y2 = crop
        cropped_img = img[x1:x2 + padding, y1:y2 + padding]
        cropped.append(cropped_img)
    return cropped

df = df.with_column(
    "cropped",
    crop_images(df["image"], df["crop"], padding=1),
)
df.show(2)
```



7. **Out\-of\-the\-box reliability**: Intelligent memory management prevents OOM errors, reasonable default values avoid complex configurations, allowing users to focus on their business and providing an out\-of\-the\-box experience.


<span id="12b2929b"></span>
## Daft application scenarios

<span id="72d62dbe"></span>
### Text generation

Traditional engines (such as Pandas) are inefficient when handling large\-scale text data and structured data fusion, making data preparation for applications such as RAG more complex. Spark cannot perform heterogeneous scheduling of CPU/GPU resources, resulting in uneven resource utilization efficiency for text processing tasks. Daft **natively supports multimodal data processing**, and by leveraging Daft's **built\-in embedding types** and embedding functions, efficiently schedules CPU operators and GPU operators to the appropriate resources, flexibly configures the resources required for different types of operators, and achieves **efficient GPU utilization**. Its **built\-in Rust kernel** delivers high\-performance data processing, enabling business personnel to focus on business process development without expending significant effort on complex data processing chains.

<span id="1c8778d2"></span>
### Image processing

In scenarios such as image classification, style transfer, or AIGC (such as Stable Diffusion), Daft can manage distributed preprocessing and model inference pipelines. Daft's **heterogeneous scheduling** capability enables different types of CPU/GPU operators, such as resolution adjustment, feature extraction, and label generation, to be scheduled to the appropriate resources. By leveraging **stream computing** capability, GPU utilization is improved, significantly increasing image processing and generation throughput. **Built\-in image types and image processing functions** enable efficient image processing.

<span id="fe250ad9"></span>
### Video processing

Conventional video processing requires splitting videos into frames for individual processing, resulting in a cumbersome workflow and difficulty maintaining temporal consistency. Daft, based on a native multimodal AI data lake architecture, directly supports processing multimodal data such as audio and video without additional conversion steps. As a distributed engine with **Rust as its core**, Daft efficiently handles the parallel computing demands of video data, maintaining data integrity while ensuring processing speed, making it especially suitable for preprocessing large\-scale video datasets for AI training.

<span id="938c5a99"></span>
### Autonomous driving

Autonomous driving systems face challenges in integrating multi\-source heterogeneous data (such as point clouds, images, and sensor data), and traditional engines like Spark struggle to provide unified processing. Daft supports **seamless integration of multimodal data**, including images and text, audio and video, and point clouds, and is specifically designed to address complex data processing scenarios. This engine was developed in response to Lyft's real\-world data processing needs, enabling efficient handling of real\-time data streams in autonomous driving, achieving **elastic scaling** and engineering deployment of multimodal data, while balancing cost control and high\-performance output. Daft supports **seamless integration with PyTorch**, allowing processed data to be directly incorporated into autonomous driving model training, improving the efficiency of autonomous driving model training.

<span id="bee1728e"></span>
### Embodied intelligence

Embodied intelligence requires processing multimodal data streams such as video, tactile, and motion, and traditional data processing tools struggle to meet the complex requirements of multimodal data. As an AI\-native multimodal data processing platform, Daft can interface with various data sources for embodied scenarios, such as HDF5, LeRobot, and mcap, providing a unified data processing middleware for embodied intelligence. Its **distributed architecture** supports complex data preprocessing and feature engineering, enabling robotic systems to more efficiently integrate visual, tactile, position, and other sensory data, improving the accuracy and responsiveness of environmental interactions.

<span id="cc684f58"></span>
## Daft**Quick start**

The following demonstrates how to use Daft to query image files in a TOS path, filter out images that do not meet the requirements, and finally use a UDF to generate a sample with a red mark for images containing red occlusion.

```Python
import daft
import numpy as np
import PIL.Image
from PIL import ImageFilter 

IO_CONFIG = daft.io.IOConfig(s3=daft.io.S3Config(anonymous=True))  # Use anonymous S3 access
# Load image data
df = daft.from_glob_path(
    "s3://daft-public-data/open-images/validation-images/*",
    io_config=IO_CONFIG,
)

# Filter out oversized images
df = df.where(df["size"] < 300000)

df = df.select("path")
df = df.with_column("image", df["path"].url.download(io_config=IO_CONFIG))
df = df.with_column("image", df["image"].image.decode())

def magic_red_detector(img: np.ndarray) -> PIL.Image.Image:
    """Gets a new image which is a mask covering all 'red' areas in the image."""
    img = PIL.Image.fromarray(img)
    lower = np.array([245, 100, 100])
    upper = np.array([10, 255, 255])
    lower_hue, upper_hue = lower[0, np.newaxis, np.newaxis], upper[0, np.newaxis, np.newaxis]
    lower_saturation_intensity, upper_saturation_intensity = (
        lower[1:, np.newaxis, np.newaxis],
        upper[1:, np.newaxis, np.newaxis],
    )
    hsv = img.convert("HSV")
    hsv = np.asarray(hsv).T
    mask = np.all(
        (hsv[1:, ...] >= lower_saturation_intensity) & (hsv[1:, ...] <= upper_saturation_intensity), axis=0
    ) & ((hsv[0, ...] >= lower_hue) | (hsv[0, ...] <= upper_hue))
    img = PIL.Image.fromarray(mask.T)
    img = img.filter(ImageFilter.ModeFilter(size=5))
    return img

df = df.with_column(
    "red_mask",
    df["image"].apply(magic_red_detector, return_dtype=daft.DataType.python()),
)
df.show()
```
