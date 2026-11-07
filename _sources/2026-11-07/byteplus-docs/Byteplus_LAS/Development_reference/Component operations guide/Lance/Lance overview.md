---
title: "Lance overview"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Lance_overview"
---

<span id="bsyqe2Ue84"></span>
## What is Lance

Lance is a modern columnar data format specifically designed for large\-scale AI datasets. It is similar to Parquet, but is deeply optimized for the storage and access of multimodal data, such as images, videos, audio, point clouds, and traditional tabular data. Lance supports POSIX\-compatible Linux file systems and mainstream cloud object storage (BytePlus TOS), making it an ideal foundation for building a unified AI data lake.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b14e0f31777340f0acdee85599a0e5cd~tplv-goo7wpa0wc-image.image) </span>

The core of the Lance format lies in its efficient file structure, which consists of three logical layers:


1. **File format layer**: A proprietary underlying storage format that efficiently stores and enables random access to large\-scale, multimodal data.

2. **Data lake format layer**: Similar to Apache® Iceberg, it provides robust data lake management features, such as atomic transactions and multi\-version control. It is primarily accessed by offline engines, does not support write operations from streaming engines, and is currently not applicable to AI scenarios.

> Apache Iceberg, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


3. **Application layer**: Lance supports multiple integration methods. It can be operated with a standalone SDK, such as PyLance, or used with distributed engines like Spark and Ray to read and write Lance data. It can even be used as a vector database via the lancedb interface.


<span id="X4gGxlVfGW"></span>
## What can Lance do

<span id="er19tOuldR"></span>
### Main features

The main capabilities of Lance include:


* **High\-performance random access**: For individual data entries, the take operation is more than 10 times faster than Parquet.

* **Vector search**: Indexing supports millisecond\-level nearest neighbor search and combines scalar queries with vector search.

* **Zero\-copy and automatic version control**: Automatically manages data versions and uses built\-in zero\-copy logic to reduce redundancy.

* **Ecosystem integration**: Apache® Arrow, DuckDB, and more are under development.

> Apache Arrow, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


<span id="ekJTtI8RSy"></span>
### **Core challenges addressed (AI dataset challenges)** 

In traditional AI/ML workflows, dataset management faces many challenges, such as:


* **Version confusion**: Changes to training data are difficult to track, resulting in unreproducible model training outcomes.

* **Inefficient access**: For large\-scale datasets, especially those containing vectors or multimedia files, random access and query performance are poor.

* **Fragmented ecosystem**: Data preprocessing, model training, and vector search often require different tools and data formats, increasing system complexity and data redundancy.


Lance addresses these issues by providing a unified platform, with core capabilities including:


* **Unified management of multimodal data**: Stores unstructured data (such as images) and structured data (such as metadata and labels) in the same table.

* **Efficient data version control**: Automatically records every data change to ensure experiment reproducibility.

* **High\-performance query and search**: Supports data filtering and vector similarity search.


<span id="RWbhjJYCMH"></span>
## Core features


* **Zero\-copy, index\-free data access**: Uses zero\-copy technology when reading data to avoid unnecessary data duplication, significantly improving I/O efficiency. Its unique format design enables random access performance that is 100 times faster than Parquet, without relying on additional indexes.

* **Dataset version control and reproducibility**: Every data write, update, or delete operation automatically generates a new, immutable dataset version.

* **Seamless integration with the ecosystem**: Lance is fully compatible with the Apache Arrow memory format, enabling easy data exchange with mainstream data science tools such as Pandas, DuckDB, and Polars, and also supports integration with large\-scale distributed computing engines like Spark and Ray.


<span id="UYqoQP9zfE"></span>
## Architecture overview

<span id="xBqt9PJ5qN"></span>
### **Internal structure of the Lance format**

A Lance dataset is represented as a directory in storage, mainly containing:


* `data/` directory: Stores actual data files (`.lance` files).

* `_versions/` directory: Stores the metadata manifest for each version (`manifest` files), recording which data files are included in that version.

* `_transactions/` directory: Ensures atomicity of write operations.

* `_deletions/`directory: Stores deletion files (deletion vectors) to track deleted rows without rewriting data files.

* The `_indices/` directory: After creating an index for Lance data, the index files are stored in this directory, with each index stored in a separate UUID subdirectory.


<span id="SxlL0jqq01"></span>
### **Data reading and writing process**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bdedea7f2b14d81880192ffebc9d458~tplv-goo7wpa0wc-image.image) </span>

<span id="ZSs5RlVuzl"></span>
## How to use

For usage instructions, see [Quick start](https://docs.byteplus.com/docs/Byteplus_LAS/Lance_Quick_start).

&nbsp;
