---
title: "Lance overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Lance_overview"
---

<span id="53b4007e"></span>
## What is Lance

Lance is a modern columnar data format designed specifically for large\-scale AI datasets. It is similar to Parquet, but deeply optimized for the storage and access of multimodal data, such as images, videos, audio, point clouds, and traditional tabular data. Lance supports POSIX\-compliant Linux file systems and mainstream cloud object storage (Volcano Engine TOS), making it an ideal foundation for building a unified AI data lake.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa5a3bd4cd694a8b9d8a130427d6a908~tplv-goo7wpa0wc-image.image) </span>

The core of the Lance format lies in its efficient file structure, which consists of three logical layers:


1. **File format layer**: A proprietary underlying storage format, capable of efficiently storing and randomly accessing large\-scale, multimodal data.

2. **Data lake format layer**: Similar to Apache Iceberg, it provides robust data lake management features, such as atomic transactions and multi\-version control. It is primarily accessed by offline engines, does not support streaming engine writes, and is currently not applicable to AI scenarios.

3. **Application layer**: Lance supports multiple integration methods. It can be operated with standalone SDKs, such as PyLance, or through distributed engines, such as Spark and Ray, for reading and writing Lance data. It can even be used as a vector database via the lancedb interface.


<span id="d38e5d27"></span>
## What can Lance do

<span id="127271af"></span>
### Main features

The main functions of Lance include:


* **High\-performance random access**: For individual data entries, the take operation is more than ten times faster than Parquet.

* **Vector search**: Indexing supports millisecond\-level nearest neighbor lookup and combines scalar queries with vector search.

* **Zero\-copy and automatic version control**: Data versions are managed automatically, and built\-in zero\-copy logic reduces redundancy.

* **Ecosystem integration**: Apache Arrow, DuckDB, and more are under development.


<span id="3a89b5f9"></span>
### **Core challenges addressed (AI dataset challenges)** 

In traditional AI/ML workflows, dataset management faces many challenges, such as:


* **Version confusion**: Changes to training data are difficult to track, resulting in non\-reproducible model training outcomes.

* **Inefficient access**: For large\-scale datasets, especially those containing vectors or multimedia files, random access and query performance are poor.

* **Fragmented ecosystem**: Data preprocessing, model training, and vector search typically require different tools and data formats, increasing system complexity and data redundancy.


Lance addresses these issues by providing a unified platform, with core capabilities including:


* **Unified management of multimodal data**: Stores unstructured data (such as images) and structured data (such as metadata and labels) in the same table.

* **Efficient data version control**: Automatically records every data change to ensure experiment reproducibility.

* **High\-performance query and search**: Supports data filtering and vector similarity search.


<span id="301e357a"></span>
## Core features


* **Zero\-copy, index\-free data access**: Uses zero\-copy technology when reading data to avoid unnecessary data duplication, significantly improving I/O efficiency. Its unique format design enables random access performance that is 100 times faster than Parquet, without relying on additional indexes.

* **Dataset version control and reproducibility**: Every data write, update, or delete operation automatically generates a new, immutable dataset version.

* **Seamless integration with the ecosystem**: Lance is fully compatible with the Apache Arrow memory format, allowing easy data exchange with mainstream data science tools such as Pandas, DuckDB, and Polars. It also supports integration with large\-scale distributed computing engines such as Spark and Ray.


<span id="693f0f15"></span>
## Architecture overview

<span id="3962b6f1"></span>
### **Internal structure of the Lance format**

A Lance dataset is represented as a directory in storage, mainly containing:


* `data/` directory: Stores actual data files (`.lance` files).

* `_versions/` directory: Stores the metadata manifest for each version (`manifest` files), recording which data files are included in that version.

* `_transactions/` directory: Used to ensure atomicity of write operations.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc073ea391164353a9a66177b55bb386~tplv-goo7wpa0wc-image.image" width="615px" /></div>


<span id="854d57d6"></span>
### **Data read and write process**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bc630280aa641cdaf51a7aefb2f6f1f~tplv-goo7wpa0wc-image.image" width="3804px" /></div>


<span id="15127fee"></span>
## How to use

For usage instructions, please see [Quick Start](https://docs.byteplus.com/docs/E-MapReduce/109326).

&nbsp;
