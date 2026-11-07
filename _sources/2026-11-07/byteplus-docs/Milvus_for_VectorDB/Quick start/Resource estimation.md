---
title: "Resource estimation"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Resource_estimation"
---

Before using Milvus for VectorDB, you should reasonably estimate the required computing resources to ensure system stability and optimize costs. Milvus for VectorDB offers a resource calculator that helps you estimate the required resources based on the provided experimental data, including vector count, vector dimension, and index type, and adjust according to test results during deployment.

<span id="BLp1t6WV"></span>
# Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region where you want to estimate resources.

3. In the left navigation bar, click **Resource calculator**.

4. On the **Resource calculator** page, configure the following parameters. The **Resource** panel on the right shows resource requirements in real time based on your configuration.

   
   |Parameter |Description |
   |---|---|
   |Engine version |Select **2.5** or **2.6** according to your needs. |
   |Type |Select **Capacity** or **Performance** based on your business requirements. |
   |Vector count |The vector count directly determines the index size and the amount of data to traverse during queries. The larger the quantity, the more storage space required. It also increases the computational complexity during index building and querying, which may result in longer processing times and higher hardware requirements. Valid values: 1~10,000. Unit: million. |
   |Vector dimension |Vector dimension affects the complexity and accuracy of the index. High\-dimensional vectors increase index complexity because each vector requires more computing resources to compare similarity in high\-dimensional space. This not only increases storage costs but also reduces query speed, especially without effective dimensionality reduction or quantization strategies. |
   |Index type |Index type is a key factor that determines resource requirements and query performance. Different index algorithms have varying demands for Memory, CPU, and query time. Supported index types are as follows:<br><br><br>* FLAT: provides the highest query accuracy. Due to exact matching, query speed is sacrificed, and performance may be unsatisfactory, especially on large\-scale datasets. Suitable for scenarios with relatively small data volumes, such as tens of millions pieces, and strict requirements on query accuracy but low requirements on query speeds.<br><br>* SCANN: an efficient approximate nearest neighbor search index structure suitable for large\-scale datasets needing fast retrieval but with lower accuracy requirements. It balances speed and resource consumption by focusing on maximum inner product search through search space pruning and quantization techniques.<br><br>* HNSW: a graph\-based index that offers extremely high query efficiency, especially in high\-dimensional data spaces. However, it demands more computing resources and memory, fitting scenarios that require the fastest query speed and sufficient resources, especially when handling high\-dimensional data.<br><br>* IVF_FLAT: offers a balance between accuracy and query speed, suitable for most scenarios. It reduces computational complexity through quantization, significantly improving query performance compared to the FLAT index, while keeping resource consumption relatively low. Suitable for scenarios aiming to balance query performance and resource costs with large data volumes.<br><br>* IVFSQ8: accelerates retrieval by using quantization technology, suitable for resource\-constrained scenarios that require high recall rates, especially for large\-scale datasets. Compared to HNSW, its query accuracy may decrease.<br><br>* DISKANN: a disk\-based approximate nearest neighbor search technology designed for efficient and fast retrieval of large\-scale datasets. It uses the Vamana graph algorithm to achieve efficient vector indexing and retrieval under limited memory conditions, suitable for handling ultra\-large high\-dimensional data.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This index type is available only when the <strong>Type</strong> of the node is set to <strong>Capacity</strong>.   </div><br>    |
   |with_raw_data |Specifies whether to store the raw data in the index. Valid values: True or False. If your system is mainly used for fast approximate search and does not require frequent access to the raw data, set it to False. Otherwise, set it to True.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only available when <strong>Index type</strong> is set to <strong>SCANN</strong>.</div><br> |
   |M |Determines the number of neighbors per node. A larger value increases recall and accuracy of the index but also raises index construction time and memory usage. A smaller value speeds up index construction and reduces memory usage but may sacrifice some accuracy. The recommended initial value is lg(N), where N is the total vector count and can be fine\-tuned based on actual query performance. For example, you can try setting it to 16, 32, or 64, observe the results, and adjust accordingly.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only available when the <strong>Index type</strong> is set to <strong>HNSW</strong>.</div><br> |
   |nlist |Determines the number of subspaces (clusters) to divide the vector space into. Larger values increase index accuracy and recall but raise the time required to build the index and the computation cost during queries. Smaller values reduce index complexity but may lower accuracy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only available when <strong>Index type</strong> is set to <strong>IVF_FLAT</strong> or <strong>IVFSQ8</strong>.</div><br> |
   |Scalar field |When you enable this parameter, you can set the average size of data rows to help the indexing system optimize memory, storage, and shard planning, as well as improve query performance. |
   |Segment size |The maximum data capacity in a segment. Valid values:<br><br><br>* 512 MB: recommended for query nodes with 4~8 GB memory.<br><br>* 1024 MB: recommended for query nodes with 8~16 GB memory (default value).<br><br>* 2048 MB: recommended for query nodes with more than 16 GB memory. |
   

5. (Optional) Click **Create instance** as needed. The system redirects to the **Create instance** page and automatically configures the instance specifications based on the generated resource requirements. You only need to configure the remaining parameters to complete the instance creation. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your configured data volume is too large, you cannot initiate instance creation directly based on resource requirements on the <strong>Resource calculator</strong> page. You can <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001558">contact us</a> to discuss the best deployment practices.   </div>
