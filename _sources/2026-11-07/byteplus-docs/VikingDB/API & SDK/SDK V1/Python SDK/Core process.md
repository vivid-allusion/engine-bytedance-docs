---
title: "Core process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Core_process1"
---

<span id="core-process"></span>
# Core process

To quickly integrate the VikingDB Python SDK into your application, you can use this complete code example. This guide provides a sample request that covers the entire workflow: creating a collection, writing vector data, building an index, and executing various data query and retrieval operations.

```Python
# Sample code 
fields = [ 
    Field( 
        field_name="doc_id", 
        field_type=FieldType.String, 
        is_primary_key=True 
    ), 
    Field( 
        field_name="text_vector", 
        field_type=FieldType.Vector, 
        dim=10 
    ), 
    Field( 
        field_name="like", 
        field_type=FieldType.Int64, 
        default_val=0 
    ), 
    Field( 
        field_name="price", 
        field_type=FieldType.Float32, 
        default_val=0 
    ), 
    Field( 
        field_name="author", 
        field_type=FieldType.List_String, 
        default_val=[] 
    ), 
    Field( 
        field_name="aim", 
        field_type=FieldType.Bool, 
        default_val=True 
    ), 
] 
res = vikingdb_service.create_collection("example", fields, "This is an example") 
# Return a collection instance 
print(res) 

res = vikingdb_service.get_collection("example") 
# Return a collection instance 
print(res) 

vikingdb_service.drop_collection("example")  # No value is returned. 

res = vikingdb_service.list_collections() 
# Return a list 
print(res) 

vector_index = VectorIndexParams(distance=DistanceType.COSINE,index_type=IndexType.HNSW, 
                                 quant=QuantType.Float) 
res = vikingdb_service.create_index("example","example_index", vector_index, cpu_quota=2, 
                                    description="This is an index", partition_by="like", scalar_index=None) 
# Return an index instance 
print(res) 

res = vikingdb_service.get_index("example", "example_index") 
# Return an index instance 
print(res.description) 

vikingdb_service.drop_index("example", "example_index")  # No value is returned. 

res = vikingdb_service.list_indexes("example") 
# Return a list 
print(res) 

def gen_random_vector(dim): 
    res = [0, ] * dim 
    for i in range(dim): 
        res[i] = random.random() - 0.5 
    return res 
collection = vikingdb_service.get_collection("example") 
field1 = {"doc_id": "11", "text_vector": gen_random_vector(10), "like": 1, "price": 1.11, 
          "author": ["gy"], "aim": True} 
field2 = {"doc_id": "22", "text_vector": gen_random_vector(10), "like": 2, "price": 2.22, 
          "author": ["gy", "xjq"], "aim": False} 
field3 = {"doc_id": "33", "text_vector": gen_random_vector(10), "like": 1, "price": 3.33, 
          "author": ["gy", "xjq"], "aim": False} 
field4 = {"doc_id": "44", "text_vector": gen_random_vector(10), "like": 1, "price": 4.44, 
          "author": ["gy", "xjq"], "aim": False} 
data1 = Data(field1) 
data2 = Data(field2) 
data3 = Data(field3) 
data4 = Data(field4) 
datas = [] 
datas.append(data1) 
datas.append(data2) 
datas.append(data3) 
datas.append(data4) 
collection.upsert_data(datas)  # No value is returned. 

collection = vikingdb_service.get_collection("example") 
res = collection.fetch_data(["11", "22", "33", "44"]) 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 

collection = vikingdb_service.get_collection("example") 
collection.delete_data("11")  # No value is returned. 

index = vikingdb_service.get_index("example", "example_index") 
res = index.fetch_data(["11", "33"], partition="default", output_fields=["doc_id", "like"]) 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 

index = vikingdb_service.get_index("example", "example_index") 
res = index.search_by_id("11", limit=2, output_fields=["doc_id", "like", "text_vector"], partition="default") 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 

index = vikingdb_service.get_index("example", "example_index") 
def gen_random_vector(dim): 
    res = [0, ] * dim 
    for i in range(dim): 
        res[i] = random.random() - 0.5 
    return res 
res = index.search_by_vector(gen_random_vector(10), limit=2, output_fields=["doc_id", "like", "text_vector"], 
                             partition="default") 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 

index = vikingdb_service.get_index("example", "example_index") 
def gen_random_vector(dim): 
    res = [0, ] * dim 
    for i in range(dim): 
        res[i] = random.random() - 0.5 
    return res 
res = index.search(order=VectorOrder(gen_random_vector(10)), limit=2, 
                   output_fields=["doc_id", "like", "text_vector"], 
                   partition="1", filter={"op": "range", "field": "price", "lt": 3.5}) 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 
res = index.search(order=ScalarOrder("price", Order.Desc), limit=6, 
                   output_fields=["price"], 
                   partition="default", 
                   filter={"op": "range", "field": "price", "lt": 5}) 
# Return a list 
for item in res: 
    print(item) 
    print(item.fields) 

# A test that contains text fields 
fields = [ 
    Field( 
        field_name="doc_id", 
        field_type=FieldType.String, 
        is_primary_key=True 
    ), 
    Field( 
        field_name="text", 
        field_type=FieldType.Text, 
        pipeline_name="text_split_bge_large_zh" 
    ), 
    Field( 
        field_name="like", 
        field_type=FieldType.Int64, 
        default_val=0 
    ), 
    Field( 
        field_name="price", 
        field_type=FieldType.Float32, 
        default_val=0 
    ), 
    Field( 
        field_name="author", 
        field_type=FieldType.List_String, 
        default_val=[] 
    ), 
    Field( 
        field_name="aim", 
        field_type=FieldType.Bool, 
        default_val=True 
    ), 
] 
res = vikingdb_service.create_collection("example_text", fields, "This is an example include text") 

vector_index = VectorIndexParams(distance=DistanceType.COSINE, index_type=IndexType.HNSW, 
                                 quant=QuantType.Float) 
res = vikingdb_service.create_index("example_text", "example_index_text", vector_index, cpu_quota=2, 
                                    description="This is an index include text", partition_by="like", 
                                    scalar_index=None) 

collection = vikingdb_service.get_collection("example_text") 
field1 = {"doc_id": "11", "text": {"text":"this is one"}, "like": 1, "price": 1.11, 
          "author": ["gy"], "aim": True} 
field2 = {"doc_id": "22", "text": {"text":"this is two"}, "like": 2, "price": 2.22, 
          "author": ["gy", "xjq"], "aim": False} 
field3 = {"doc_id": "33", "text": {"text":"this is three"}, "like": 1, "price": 3.33, 
          "author": ["gy", "xjq"], "aim": False} 
field4 = {"doc_id": "44", "text": {"text":"this is four"}, "like": 1, "price": 4.44, 
          "author": ["gy", "xjq"], "aim": False} 
data1 = Data(field1) 
data2 = Data(field2) 
data3 = Data(field3) 
data4 = Data(field4) 
datas = [] 
datas.append(data1) 
datas.append(data2) 
datas.append(data3) 
datas.append(data4) 
collection.upsert_data(datas)  # No value is returned. 

index = vikingdb_service.get_index("example_text", "example_index_text") 
res = index.search_by_text(Text(text="this is five"), filter={"op": "range", "field": "price", "lt": 4}, 
                           limit=3, output_fields=["doc_id", "text", "price", "like"], partition="default") 
for item in res: 
    print(item) 
    print(item.fields) 
list = [RawData("text","hello1"), RawData("text","hello2")] 
res = vikingdb_service.embedding(EmbModel("bge_large_zh"), list) 
print(res) 
for item in res: 
    print(item)
```
