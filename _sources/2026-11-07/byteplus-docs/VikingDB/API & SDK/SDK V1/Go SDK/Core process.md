---
title: "Core process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_Core_process"
---

<span id="core-process"></span>
# Core process

To quickly get started with the VikingDB Go SDK, you can use this complete code example that demonstrates the entire workflow. The sample requests guide you through creating a collection, writing vector data, building an index, querying data, and performing hybrid retrieval.

```Go
// Create a collection named go. 
fields := []vikingdb.Field{ 
    { 
       FieldName:    "doc_id", 
       FieldType:    vikingdb.String, 
       IsPrimaryKey: true, 
    }, 
    { 
       FieldName: "text_vector", 
       FieldType: vikingdb.Vector, 
       Dim:       12, 
    }, 
    { 
       FieldName:  "like", 
       FieldType:  vikingdb.Int64, 
       DefaultVal: 0, 
    }, 
    { 
       FieldName: "price", 
       FieldType: vikingdb.Float32, 
       Dim:       12, 
    }, 
    { 
       FieldName:  "author", 
       FieldType:  vikingdb.ListString, 
       DefaultVal: []string{}, 
    }, 
    { 
       FieldName:  "aim", 
       FieldType:  vikingdb.Bool, 
       DefaultVal: true, 
    }, 
} 
collection, err := service.CreateCollection("go", fields, "this is a go example") 
if err != nil { 
    print(err.Error()) 
} 
// Write data to the collection. 
collection, _ := service.GetCollection("go") 
field1 := map[string]interface{}{ 
    "doc_id":      "111", 
    "text_vector": genRandomVector(12), 
    "like":        1, 
    "price":       1.11, 
    "author":      []string{"gy"}, 
    "aim":         true, 
} 
field2 := map[string]interface{}{ 
    "doc_id":      "222", 
    "text_vector": genRandomVector(12), 
    "like":        2, 
    "price":       2.22, 
    "author":      []string{"gy", "xjq"}, 
    "aim":         false, 
} 
field3 := map[string]interface{}{ 
    "doc_id":      "333", 
    "text_vector": genRandomVector(12), 
    "like":        3, 
    "price":       3.33, 
    "author":      []string{"gy"}, 
    "aim":         true, 
} 
field4 := map[string]interface{}{ 
    "doc_id":      "444", 
    "text_vector": genRandomVector(12), 
    "like":        4, 
    "price":       4.44, 
    "author":      []string{"gy"}, 
    "aim":         true, 
} 
data1 := vikingdb.Data{ 
    Fields: field1, 
    TTL:    100000, 
} 
data2 := vikingdb.Data{ 
    Fields: field2, 
    TTL:    200000, 
} 
data3 := vikingdb.Data{ 
    Fields: field3, 
    TTL:    100000, 
} 
data4 := vikingdb.Data{ 
    Fields: field4, 
} 
datas := []vikingdb.Data{ 
    data1, 
    data2, 
    data3, 
    data4, 
} 
err := collection.UpsertData(datas) 
if err != nil { 
    print(err.Error()) 
} 

// Query data in the collection. 
collection, _ := service.GetCollection("go") 
res, err := collection.FetchData([]string{"111", "222", "333", "444"}) 
if err != nil { 
    fmt.Println(err) 
} 
for _, item := range res { 
    fmt.Println(item) 
} 

// Create an index named goIndex for the collection. 
vectorIndex := &vikingdb.VectorIndexParams{ 
    Distance:  vikingdb.COSINE, 
    IndexType: vikingdb.HNSW, 
} 
indexOptions := vikingdb.NewIndexOptions().SetVectorIndex(vectorIndex).SetCpuQuota(2).SetDescription("this is an index").SetPartitionBy("").SetScalarIndex([]string{"price", "like"}) 
index, err := service.CreateIndex("go", "goIndex", indexOptions) 
if err != nil { 
    fmt.Println(err) 
} 
fmt.Println(index) 


// Perform hybrid retrieval. 
index, _ := service.GetIndex("go", "goIndex") 
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}) 
res, err := index.Search(vikingdb.VectorOrder{Id: "111"}, searchOption) 
if err != nil { 
    fmt.Println(err) 
} 
for _, item := range res { 
    fmt.Println(item) 
} 

// Or 
index, _ := service.GetIndex("go", "goIndex") 
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}) 
res, err := index.Search(vikingdb.ScalarOrder{FieldName: "price", Order: vikingdb.Desc}, searchOption) 
if err != nil { 
    fmt.Println(err) 
} 
for _, item := range res { 
    fmt.Println(item) 
}
```
