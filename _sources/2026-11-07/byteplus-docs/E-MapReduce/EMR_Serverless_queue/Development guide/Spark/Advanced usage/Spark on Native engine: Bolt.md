---
title: "Spark on Native engine: Bolt"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sq_spark_on_native_engine"
---

<span id="296b8ced"></span>
# Introduction to Bolt

The Bolt engine is ByteDance's open\-source, next\-generation native execution engine, providing a unified, high\-performance, and scalable computational foundation for enterprise\-level data analytics scenarios. It is not a dedicated acceleration component designed solely for Spark, but is instead engineered with the goal of "adapting to any framework, running on any hardware, and connecting to any data source." Bolt can be flexibly integrated with mainstream computing frameworks such as Spark, Presto, and Flink, delivering consistent native acceleration capabilities for diverse data platforms. Through a unified interface and pluggable architecture, the Bolt engine helps customers ensure open compatibility while further unlocking the value of underlying computing power, achieving higher performance, lower resource consumption, and greater ecosystem extensibility.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When users utilize Bolt acceleration, they pay the corresponding acceleration fees based on the actual CUH consumed by their jobs. For detailed billing rules, see <a href="https://docs.byteplus.com/docs/E-MapReduce/Billing_for_Bolt">Bolt acceleration engine pricing details</a>.</div>


<span id="82f1c5b1"></span>
## **Design philosophy: moving from "M × N" to "M + N"** 

Traditional big data platforms often face complex adaptation challenges brought by the parallel evolution of multiple engines, data sources, hardware, and features. Each addition of an execution engine, a type of data source, or a capability enhancement incurs extra development, maintenance, and optimization costs, ultimately resulting in "M × N" complexity amplification.

The core design philosophy of Bolt is to converge this multidimensional adaptation complexity as much as possible through unified native execution and acceleration capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5956bb7474ce4cf4b7b4a078c09f1e16~tplv-goo7wpa0wc-image.image) </span>


* It connects to the physical execution plan of upper\-layer engines through an integration layer.

* At the underlying level, it provides unified operator capabilities, resource management, and execution optimization, thereby retaining existing Spark compatibility while consolidating performance optimizations into a unified native execution layer. For customers, this means that there is no need to change their existing Spark usage, and they can achieve higher performance, lower resource consumption, and greater extensibility within their current system.


<span id="d27a5715"></span>
## **Technical optimization: unlocking execution potential by "seeking common ground while preserving differences"** 

Bolt's technical approach can be summarized as "seeking common ground while preserving differences."


*  **“Seeking commonality”** : This refers to unified optimization around the shared performance bottlenecks in the underlying execution of different engines, aiming to maximize the efficiency of CPU, memory, disk, and other resource usage.

*  **“Preserving differences”** : This means respecting the inherent differences between engines and operators in row\-based and column\-based processing, avoiding the introduction of additional overhead in pursuit of uniformity.


Based on this philosophy, Bolt has focused on continuous optimization in the following areas.

<span id="b554853a"></span>
### **Runtime adaptive decision\-making**

Dynamically selecting the most suitable execution strategy based on actual runtime data, such as making adjustments in sorting, HashBuild, and HashJoin scenarios by considering data characteristics, partition skew, and memory usage, thereby reducing performance loss caused by fixed thresholds.

<span id="9776eb72"></span>
### **Hot path optimization**

Targeted optimization of common hot paths in big data execution, including IO, expression evaluation, and comparison paths. For example, improving throughput in spill scenarios through asynchronous IO, and optimizing hot paths of key operators such as Sort, Agg, and Join via JIT/CodeGen.

&nbsp;

&nbsp;

<span id="a649cdb9"></span>
### **Reduce row\-column conversion overhead**

For critical paths in complex queries such as Sort, Window, Shuffle, and Spill, Bolt reduces unnecessary row\-column conversions through operator fusion, RowBasedSpill, RowBasedShuffle, and other methods, further enhancing overall execution efficiency.

&nbsp;

&nbsp;

&nbsp;

<span id="80c5d552"></span>
### **Unified underlying resource management capabilities**

Unified abstraction of CPU, memory, disk, and other resource management capabilities at the underlying layer provides stable and scalable native execution capabilities for upper\-layer Spark, and lays the foundation for subsequent adaptation to more scenarios and hardware types.

Compared to simply pursuing a fixed execution path, Bolt places greater emphasis on selecting the most suitable execution method under real production workloads, which is also a key reason it continues to deliver performance gains in complex SQL scenarios.

<span id="a21eda2b"></span>
## **Application practice: ByteDance large\-scale production benefits and benchmark**

Bolt has been continuously deployed in multiple production scenarios within ByteDance and at several external customers, and has been validated on engines such as Spark, Presto, and Flink. Currently, Bolt has achieved 100% coverage of PrestoSQL tasks and approximately 85% coverage of SparkSQL tasks within ByteDance.

Taking the Spark scenario as an example, the Java runtime within ByteDance has undergone long\-term optimization based on the open\-source Spark on Java, resulting in an overall performance improvement of 2 to 3 times compared to the open\-source version. On this basis, Spark on Bolt can further deliver approximately 1.5x performance improvement. For the PrestoSQL scenario, full coverage has been achieved, with a performance gain of approximately 2x, demonstrating Bolt's continuous optimization capability in large\-scale production environments.

In terms of standard benchmark testing, in the out\-of\-the\-box TPC\-DS SF1000 test based on Vanilla Spark 3.5 + Gluten + Bolt Backend, Bolt further reduces average execution time by 22% compared to the open\-source Velox backend, with a TPCDS acceleration ratio of 1.22x, highlighting its differentiated advantages over open\-source acceleration engine solutions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b59823662e114198a60fef860a40c21d~tplv-goo7wpa0wc-image.image" width="538px" /></div>


<span id="67644a5d"></span>
# Bolt integration

<span id="3ebc0e74"></span>
## EMR Serverless deeply integrates the Bolt engine

Volcengine EMR Serverless has deeply integrated the Bolt Native Engine, allowing customers to obtain native acceleration capabilities within the existing Serverless Spark system without modifying their original Spark usage habits. For different business scenarios, customers can select the engine runtime as needed during task execution. While maintaining compatibility with original Spark SQL and stability of business workflows, they can smoothly switch to Spark on Bolt to further unlock computing performance and resource efficiency in complex SQL scenarios.

<span id="881ff87e"></span>
## **Open\-source community and ecosystem**

Bolt has been officially open\-sourced to the community (open\-source repository: https://github.com/bytedance/bolt) and continues to enhance its ecosystem capabilities in multi\-framework, multi\-data source, and heterogeneous hardware directions. For enterprise customers, there is no need to perform complex integration themselves. They can obtain the deeply integrated Bolt acceleration capability out of the box directly through Volcengine EMR Serverless, further improving performance and resource efficiency in SQL scenarios while maintaining compatibility with the original Spark ecosystem.
