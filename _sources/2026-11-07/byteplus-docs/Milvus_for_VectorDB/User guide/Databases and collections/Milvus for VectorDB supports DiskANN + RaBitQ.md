---
title: "Milvus for VectorDB supports DiskANN + RaBitQ"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_for_VectorDB_supports_DiskANN_and_RaBitQ"
---

Milvus for VectorDB now supports DiskANN + RaBitQ. DiskANN + RaBitQ is a brand new index implementation, not a simple overlay of RaBitQ quantization on native DiskANN. This topic describes the implementation, compatibility design, parameter explanation, and usage examples of DiskANN + RaBitQ in Milvus, suitable for application scenarios that require balancing cost efficiency and system performance during large\-scale vector search.

## Background

Milvus currently supports two DiskANN implementations, distinguished by the `legacy` parameter:

* New DiskANN (recommend): `legacy = false` (default). Supports two quantization methods, PQ and RaBitQ, differentiated by the `quant_type` parameter.

* Old DiskANN: `legacy = true`. Supports only PQ quantization.

## Compatibility Notes

### Upgrade Compatibility

#### IndexMeta Mechanism

In Milvus for VectorDB, index data includes not only the index files serialized by Knowhere but also an IndexMeta metadata stored in ETCD. IndexMeta example in the old DiskANN version:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a6d4cdf0f0c3b7c6839ba173f55d13b.png)Among them, `ParamsJSON` and `Index.UserParams` are the original parameters passed by the user through the SDK, while `Index.IndexParams` are the final index parameters internally processed by Milvus for VectorDB.

### Backup and Recovery Compatibility

When using the [milvus-backup](https://github.com/zilliztech/milvus-backup) tool for backup and recovery:

* The tool does not back up index files; it only backs up IndexMeta.

* During recovery, use the `--rebuild_index` parameter to reconstruct the index based on IndexMeta.

```Bash
# create backups
./milvus-backup create -n test_backup

# recover and rebuild index
./milvus-backup restore -n test_backup -s _recover --rebuild_index
```

## Precautions

### Upgrade Precautions

* Since compatibility logic exists in both Proxy and index nodes, when creating a new index using the new version of DiskANN, ensure the versions of Proxy and index nodes are both greater than or equal to 5.11.1.

* Existing old version DiskANN indexes remain unaffected after upgrading.

* If there is an unfinished old version DiskANN index build task during the upgrade, the build will continue using the old version DiskANN index after upgrading.

### User Code Migration Precautions

#### DiskANN Index

* By default, creating an index uses the new version DiskANN + RaBitQ. Old parameters applicable only to PQ will be ignored without errors; the index can still be created successfully. For the complete parameters of the new DiskANN, refer to [Common Parameters Overview (SDK Parameter Names)](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_for_VectorDB_supports_DiskANN_and_RaBitQ#gBKcGW4T).

* No changes needed for other interfaces.

#### AUTOINDEX

* When creating an index, for capacity nodes, the index type **AUTOINDEX** defaults to DiskANN + RaBitQ. The default parameters are as follows.

   ```JSON
   {
     "search_list_size": "100",
     "max_degree": "56",
     "metric_type": "COSINE"
   }
   ```

* For existing **AUTOINDEX** index types before migration:

   * If search parameters (such as `ef_search`) are configured in `milvus.yaml`, this configuration will become invalid after migration, possibly affecting recall, QPS, and other metrics.

   * If the **AUTOINDEX** configuration in `milvus.yaml` is not modified, usage remains unchanged.

## Parameter description

Parameters use underscore naming in the SDK, for example, `max_degree`. Parameters use PascalCase naming in the configuration file `milvus.yaml`, for example, `MaxDegree`.

### Common Parameters Overview (SDK parameter names)

|**parameter category** |**Applicable quantization** |**Parameter name** |Type |Value range |**Default value** |**Description** |
|---|---|---|---|---|---|---|
|build |RaBitQ/PQ |store_strategy |String |* DISK<br><br>* MEMORY |MEMORY |DiskANN index mode. |
|build |RaBitQ/PQ |quant_type |String |* RABITQ<br><br>* PQ |RaBitQ |Specify the quantization method; this is ineffective when `legacy` is `true`. Keeping the default value is recommended in most cases. |
|build |RaBitQ/PQ |distance_strategy |String |* QUANT THEN MORE BITS<br><br>* FULL<br><br>* SINGLE QUANT<br><br>* QUANT THEN FULL<br><br><br> |QUANT THEN MORE BITS |Specify the query computation strategy. Keeping the default value is recommended in most cases.<br><br><br>* `FULL` means full\-precision search.<br><br>* `SINGLE QUANT` means quantized search.<br><br>* `QUANT THEN FULL` means quantized search + full\-precision optimization.<br><br>* `QUANT THEN MORE BITS` means 1\-bit RabitQ search + 4\-bit RaBitQ optimization.<br><br><br>> **warning**<br><br><br>> When `quant_type` is `PQ`, it falls back to `SINGLE QUANT` mode.<br> |
|build |RaBitQ/PQ |num_threads |Int |[2, int_max] |2 |Number of concurrent threads for index building. |
|build |RaBitQ/PQ |legacy |String |* "false"<br><br>* "true" |"false" |Enable legacy DiskANN. It is recommended to keep the default value in most cases. If you want to keep consistent with open\-source Milvus when creating an index on Volcengine Vector Database Milvus for VectorDB, set it to `"true"`. |
|build |RaBitQ/PQ |max_degree |Int |[1, 2048] |48 |The maximum number of neighbors per node in the graph. |
|build |RaBitQ/PQ |build_dram_budget_gb |Int |[0, int_max] |0 |Total memory allowed for the index; if insufficient memory, subgraph building will be used. `0` means adaptive. |
|build |RaBitQ/PQ |search_cache_budget_gb_ratio |Float |[0.0, 0.3) |0.1 |Query cache to original data size ratio. |
|build |RaBitQ |rabitq_centers |Int |[1, int_max] |64 |RaBitQ number of cluster centers. It is recommended to keep the default value in most scenarios. |
|build |PQ |pq_code_budget_gb_ratio |Float |(0.0, 0.25] |0.125 |Ratio of the total vector size (GB) to the space allocated for storing PQ codes. |
|build/query |RaBitQ/PQ |search_list_size |Int |[1, int_max] |128 |Candidate set length of the graph. The meaning of `search_list_size` differs between construction and querying:<br><br><br>* During construction: the larger the `search_list_size`, the higher the graph quality.<br><br>* During querying: the larger the `search_list_size`, the higher the recall rate and the lower the QPS. |
|Query |RaBitQ/PQ |beam_width_ratio |Int |[1, max(128/CPU number, 16)] |4 |The ratio between the maximum number of I/O requests per search iteration and the number of CPU cores. |

### milvus.yaml Configuration Example

```YAML
DiskIndex:
  Legacy: "false"
  MaxDegree: 56
  SearchListSize: 100
  PQCodeBudgetGBRatio: 0.125
  BuildNumThreadsRatio: 1
  SearchCacheBudgetGBRatio: 0.1
```

Parameters passed via API have higher priority than those in the configuration file. If you do not set the above fields in the `params` parameter of the create_index API, Milvus for VectorDB uses the values from the configuration file. The configuration file applies at the cluster level.

When the `Legacy` parameter is set to `false`, the new DiskANN is enabled by default. If you want to maintain consistency with open\-source Milvus when creating a new index on BytePlus Milvus for VectorDB, set `Legacy` to `true`.

## Index Building Example

<Tabs>
**Python**

### ```Python
from pymilvus import Collection, connections

# 1. Connect
connections.connect(uri="http://localhost:19530",  token="user:password")

# 2. Create Collection and write data
# ...

# 3. Specify Collection
col = Collection("collection_name")

# 4. Set index parameters
index_params = {
    'metric_type': 'COSINE',
    'index_type': 'DISKANN',
    'params': {'max_degree': 48, 'store_strategy': 'MEMORY',
               'quant_type': 'RABITQ', 'distance_strategy': 'QUANT THEN MORE BITS', 'search_list_size': 200}}

# 5. Create index
col.create_index(field_name="vector_field_name", index_params=index_params,
                 index_name="index_nmae", timeout=None)

# 6. Load
col.load()

# 7. Query
vector_field = 'vector'
expr = None
k = 100
search_param = {'metric_type': 'COSINE', 'params': {'search_list_size': 200, 'use_cloud_search': True}}
query = [1,2,3]

res = col.search(
    data=[query],
    anns_field=vector_field,
    param=search_param,
    limit=k,
    expr=expr,
)
```



</Tab>
<Tab zoneid="Ab9uIXMEv3" title="Go">
<TabTitle>Go</TabTitle>

<span id="J2YR3n43"></span>
### ```Go
package main

import (
        "context"
        "fmt"
        "log"
        "github.com/milvus-io/milvus/client/v2/milvusclient"
        "github.com/milvus-io/milvus/client/v2/entity"
        "github.com/milvus-io/milvus/client/v2/index"
)

func main() {
        // -------------------------- 1. Basic configuration parameters --------------------------
        // Milvus service address (default port 19530, modify according to your deployment)
        milvusAddr := "xxxxx"
        // Collection name (fixed as VDBBench)
        collectionName := "VDBBench"
        // Index name (fixed as vector_idx)
        indexName := "vector_idx"
        // Vector field name (replace with the actual vector field name in the Collection, e.g., "embedding" or "vec")
        vectorFieldName := "vector"

        // -------------------------- 2. Connect to Milvus service --------------------------
        ctx, cancel := context.WithCancel(context.Background())
        defer cancel()
        // Create gRPC client (Milvus recommends gRPC protocol)
        c, err := milvusclient.New(ctx, &milvusclient.ClientConfig{Address: milvusAddr, Username: "xxxx", Password:"xxxx"})
        if err != nil {
                log.Fatalf("连接 Milvus 失败: %v", err)
        }
        // Close client connection at the end of the function
        fmt.Println("✅ 成功连接 Milvus")

        // -------------------------- 3. Step 1: release index (release collection load) --------------------------
        // "Release index" in Milvus essentially means releasing the collection load status (index depends on collection load)
        fmt.Println("\n📌 开始释放索引/集合...")
        err = c.ReleaseCollection(ctx, milvusclient.NewReleaseCollectionOption(collectionName))
        if err != nil {
                log.Fatalf("释放索引失败: %v", err)
        }
        fmt.Println("✅ 成功释放索引")

        // -------------------------- 4. Step 2: delete index --------------------------
        fmt.Println("\n📌 开始删除索引...")
        err = c.DropIndex(ctx, milvusclient.NewDropIndexOption(collectionName, indexName))
        if err != nil {
                log.Fatalf("删除索引失败: %v", err)
        }
        fmt.Println("✅ 成功删除索引 vector_idx")

        // -------------------------- 5. Step 3: create DISKANN index --------------------------
        fmt.Println("\n📌 开始创建 DISKANN 索引...")
        // construct DISKANN index parameters (core parameter max_degree=48, supplement with necessary default parameters)
        index := index.NewDiskANNIndex(entity.L2)
        option := milvusclient.NewCreateIndexOption(collectionName, vectorFieldName, index)
        option.WithExtraParam("store_strategy", "DISK")
        option.WithExtraParam("max_degree", 128)
        indexTask, err := c.CreateIndex(ctx, option)
        if err != nil {
                log.Fatalf("创建 DISKANN 索引失败: %v", err)
        }
        err = indexTask.Await(ctx)
        if err != nil {
                log.Fatalf("创建失败: %v", err)
        }
        fmt.Println("✅ 成功创建 DISKANN 索引（max_degree=48）")

        // -------------------------- 6. Step 4: load index (load collection) --------------------------
        fmt.Println("\n📌 开始加载索引/集合...")
        // load collection (index loads with the collection)
        loadTask, err := c.LoadCollection(ctx, milvusclient.NewLoadCollectionOption(collectionName))
        if err != nil {
                log.Fatalf("加载索引失败: %v", err)
        }
        err = loadTask.Await(ctx)
        if err != nil {
                log.Fatalf("加载失败: %v", err)
        }
        fmt.Println("✅ 成功加载索引")

        fmt.Println("\n🎉 所有操作执行完成！")
}
```

<Tab zoneid="D454UVdNVC" title="Java">

### ```Java
public void diskANNIndexTest() {
    String stringPKCollection = CommonFunction.createNewCollection();
    R<RpcStatus> indexR =
        milvusClient.createIndex(
            CreateIndexParam.newBuilder()
                .withIndexType(IndexType.DISKANN)
                .withCollectionName(stringPKCollection)
                .withFieldName(CommonData.defaultVectorField)
                .withMetricType(MetricType.L2)
                .withIndexName("DiskAnnIndex")
                .withExtraParam("{\"max_degree\":128}")
                .build());
    Assert.assertEquals(indexR.getStatus().intValue(), 1);
    milvusClient.dropCollection(
     DropCollectionParam.newBuilder().withCollectionName(stringPKCollection).build());
  }
}
```



</Tab>
</Tabs>


<span id="uk68Z5PV"></span>
### Resource Calculator

You can use the Resource calculator to calculate the required resources. For detailed steps, see [Resource estimation](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Resource_estimation).
