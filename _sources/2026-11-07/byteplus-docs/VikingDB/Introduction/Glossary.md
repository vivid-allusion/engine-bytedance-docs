---
title: "Glossary"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Glossary"
---

<span id="Glossary"></span>
# Glossary

<span id="4ab06cdb"></span>
# Collection

A collection in VikingDB is equivalent to a table in a relational database. VikingDB stores raw data in collections. You can create multiple collections, and store the vector data of different business applications in different collections for easy management.

<span id="26441b26"></span>
# Index

Indexing is the process of efficient data organization. It accelerates vector similarity search by grouping and sorting the raw data in a vector database based on the specified indexing algorithm and data structure. It boosts the efficiency and accuracy of similarity search, enabling fast candidate filtering in vector databases.

<span id="962f4554"></span>
# Subindex

Subindexing is a data partitioning method within an index. You can divide a collection into multiple partitions by a specific scalar field and create subindexes for these partitions. Retrieval performed on one subindex does not affect retrieval on another. This way, hybrid retrieval can be performed within subindexes to reduce filtering frequency and improve retrieval performance. For example, you can divide a collection into subindexes by country ID and then search for data by a specific subindex without needing to set filters, which improves search performance.

<span id="751e7f0e"></span>
# ANN

Approximate nearest neighbor (ANN) is an algorithm that obtains the nearest neighbors from a large number of samples by sacrificing accuracy for time and space. It accelerates the nearest neighbor search by building an approximate nearest neighbor search mechanism, and quickly finds the data points closest to the given query point without computing or comparing all data points.

As an efficient nearest neighbor search algorithm, ANN quickly finds the nearest neighbors in a high\-dimensional space. It features fast searching speed, efficient memory usage, and great scalability. However, it has limited precision and is sensitive to parameters.

<span id="ebe92859"></span>
# KNN

K\-nearest neighbors (KNN) is a common classification and regression algorithm used for supervised learning. It finds the nearest K data points by calculating the distance between all data points in a collection and the given data point, and then performs classification or regression on the K data points based on their tags.

KNN algorithm is suitable for small collections. It is simple, easy\-to\-use, robust, and scalable, but it is computationally intensive, requires significant storage space, and is sensitive to data distribution.

<span id="7d78aa71"></span>
# HNSW

Hierarchical navigable small world (HNSW) is a graph\-based algorithm that performs ANN search in high\-dimensional spaces. It constructs a hierarchical graph structure to accelerate searching for the nearest neighbors, and is applicable to scenarios with high efficiency requirements.

In this hierarchical structure, each node represents a set of points, with closer nodes connected by edges. HNSW graphs are variants of KNN graphs. Each point in the hierarchical structure is connected to its K nearest neighbors. By reducing the number of nodes to be accessed, HNSW finds the nearest neighbors fast without calculating or comparing all data points.

HNSW algorithm features fast searching speed, efficient memory usage, and great scalability, and supports dynamic updates. However, it is sensitive to parameters and data distribution. Parameter tuning is required.

<span id="4a1b2948"></span>
# Flat index

A flat index stores vectors in their raw form without compressing them. Flat indexes leverage brute\-force search to traverse all vectors in a vector database and calculate the distance between each vector in the database and the target vector. Search by a flat index is slow, but is highly efficient when the searched dataset is small.

Flat indexes provide a 100% recall, without data training or parameter configuration. Unlike other types of indexes that use disk space when being saved as files, flat indexes do not occupy additional disk space. Therefore, this index type is suitable for small collections and scenarios requiring a 100% recall.

<span id="995aeff8"></span>
# Vector field

A vector field stores vector data in a database. In VikingDB, each vector can be represented as a vector field that contains the value of each dimension of the vector. A vector is a set of ordered coordinates. Vector fields simplify the storage and management of vector data, making it easy for vector retrieval and analysis.

<span id="e70a73bc"></span>
# Scalar field

A scalar field stores a scalar in a database. Scalars are quantities that have only magnitude and no direction, such as temperature, weight, and length. Unlike a vector field, which contains multiple values, a scalar field usually contains only one value. In VikingDB, scalar fields typically store data that is independent of the vector data, such as the author of the text.

<span id="be7596dc"></span>
# K\-nearest neighbor search

A K\-nearest neighbor search retrieves vectors by calculating the similarity between vectors based on a vector space model. It builds a time\- and space\-efficient data structure for vectors in a given collection based on a distance metric such as inner product and Euclidean distance so that the K\-nearest vectors to a query vector can be retrieved quickly.

<span id="df4b3798"></span>
# Hybrid dense\-sparse vector retrieval

Hybrid dense\-sparse vector retrieval combines the advantages of dense and sparse vector retrieval. It characterizes both dense and sparse vectors, and simultaneously searches two vector spaces to retrieve a batch of relevant documents. It not only leverages the advantages of dense vector retrieval in handling complex semantic relationships, but also benefits from the high efficiency of sparse vector retrieval. It effectively achieves high\-precision and high\-efficiency in retrieval tasks.

<span id="500b08da"></span>
# Scalar sorting retrieval

Scalar sorting retrieval is a feature provided by VikingDB that allows you to search for data based on scalar values. In a vector database, each data point can have one or more associated scalar values. You can retrieve relevant data based on these scalar values, such as retrieving documents based on author characteristics.

<span id="cf7652e5"></span>
# Scalar filtering retrieval

Scalar filtering retrieval is a feature provided by VikingDB that allows you to search for data using both vector and scalar retrieval capabilities. Vector retrieval is performed to search for similar vectors, while scalar retrieval is performed to match the scalar values of a vector.

<span id="626bad45"></span>
# **Multimodal retrieval**

This operation allows you to search for raw multimodal data. You can search for text by using a text query. When you search for data by text, VikingDB measures the distance between text segments to determine and return their similarity. This feature applies to scenarios such as duplicate detection, text search and matching, and Q&A.
