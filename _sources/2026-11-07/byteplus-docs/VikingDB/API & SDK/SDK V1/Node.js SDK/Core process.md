---
title: "Core process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_Core_process"
---

<span id="core-process"></span>
# Core process

To integrate the VikingDB Node.js SDK into your application, you can use this complete code example. It demonstrates the entire core workflow: creating a collection, writing vector data, creating an index, querying data, and performing retrieval.

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

async main() { 
  declare const service: vikingdb.VikingdbService 
  
  await service.collection.CreateCollection({ 
    CollectionName: 'test_collection', 
    Description: 'a test collection', 
    Fields: [ 
      { FieldName: 'Id', IsPrimary: true, FieldType: vikingdb.FieldType.Int64 }, 
      { FieldName: 'Name', FieldType: vikingdb.FieldType.String }, 
      { FieldName: 'Sex', FieldType: vikingdb.FieldType.Bool, DefaultValue: false }, 
      { FieldName: 'Vector', FieldType: vikingdb.FieldType.DenseVector, Dim: 4 } 
    ] 
  }) 
  
  interface Record { 
    Id: number 
    Name: string 
    Sex: boolean 
    Vector: [number, number, number, number] 
  } 
  
  const data: Record[] = [ 
    { Id: 1, Name: 'Tom', Vector: [1, 2, 3, 4] }, 
    { Id: 2, Name: 'Jerry', Sex: true, Vector: [2, 3, 4, 5] }, 
  ] 
  
  await service.data.UpsertData({ 
    CollectionName: 'test_collection', 
    Fields: data, 
  }) 
  
  await service.index.CreateIndex({ 
    CollectionName: 'test_collection', 
    IndexName: 'test_index', 
    Description: 'a test index', 
    CpuQuota: 10, 
    ShardConfig: { 
      ShardPolicy: vikingdb.index.ShardPolicy.Auto 
    }, 
    VectorIndex: { 
      IndexType: vikingdb.index.IndexType.Hnsw, 
      Distance: vikingdb.index.Distance.Ip, 
      Quant: vikingdb.index.Quant.Int8, 
    }, 
    ScalarIndexes: ['Name'] 
  }) 
  
  const response = await service.search.SearchByVector<Data>({ 
    CollectionName: 'test_collection', 
    IndexName: 'test_index', 
    Limit: 10, 
    DenseVector: [[1, 2, 3, 4]] 
  }) 
  
  console.log(response.Data) // Output the search result. 
} 

main()
```
