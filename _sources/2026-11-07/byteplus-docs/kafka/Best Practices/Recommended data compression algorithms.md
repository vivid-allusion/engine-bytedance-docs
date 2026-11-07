---
title: "Recommended data compression algorithms"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/recommended-data-compression-algorithms"
---

Data compression can reduce network transmission traffic for I/O loads and disk storage space. This topic describes the recommended compression algorithms.

<span id="0545a99a"></span>
## Recommended compression algorithm

Kafka instances of version 2.\* and later support the ZSTD compression format, which has excellent compression ratio, efficiency, and CPU performance. Therefore, we strongly recommend using the ZSTD compression format.

<span id="20c190b5"></span>
## Analysis of compression algorithms

Currently, Kafka supports four compression algorithms, namely ZSTD, GZIP, Snappy, and LZ4.

To evaluate the effectiveness of a compression algorithm, two main metrics are used: compression ratio and compression/decompression throughput. In actual use of Kafka, the performance comparison of the four algorithms is as follows:


* Compression Ratio: ZSTD \> LZ4 \> GZIP \> Snappy

* Throughput: ZSTD \> LZ4 \> Snappy \> GZIP


Thus, the recommended order of the four compression algorithms under normal circumstances is: ZSTD \> LZ4 \> GZIP \> Snappy.

After long\-term observation of operating status, this order is suitable for most business scenarios. However, different data types may affect the performance of compression algorithms. Therefore, users sensitive to CPU metrics are advised to prioritize ZSTD and adjust the compression algorithm based on actual performance.
