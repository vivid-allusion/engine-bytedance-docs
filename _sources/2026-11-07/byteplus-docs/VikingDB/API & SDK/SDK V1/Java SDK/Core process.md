---
title: "Core process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Coreprocess"
---

<span id="core-process"></span>
# Core process

To quickly understand the end\-to\-end workflow of using the VikingDB Java SDK, you can use this complete code example. This guide demonstrates the entire process, from creating a collection and index to writing, querying, and retrieving vector data, helping you accelerate your integration.

```Java
       List<Field> fields = new ArrayList<>(); 
       fields.add(new Field().setFieldName("doc_id").setFieldType(FieldType.Int64).setPrimaryKey(true).build()); 
       fields.add(new Field().setFieldName("text_vector").setFieldType(FieldType.Vector).setDim(12).build()); 
       fields.add(new Field().setFieldName("like").setFieldType(FieldType.Int64).setDefaultVal(0).build()); 
       fields.add(new Field().setFieldName("price").setFieldType(FieldType.Float32).setDefaultVal(2.2).build()); 
       fields.add(new Field().setFieldName("aim").setFieldType(FieldType.Bool).setDefaultVal(false).build()); 
       fields.add(new Field().setFieldName("author").setFieldType(FieldType.List_String).build()); 
       CreateCollectionParam createCollectionParam = new CreateCollectionParam() 
                                                       .setCollectionName("javaSDKTest") 
                                                       .setFields(fields) 
                                                       .setDescription("test") 
                                                       .build(); 
       Collection collection = vikingDBService.createCollection(createCollectionParam); 

       Collection collection = vikingDBService.getCollection("javaSDKTest"); 
       System.out.println(collection); 

        vikingDBService.dropCollection("javaSDKTest"); 
        
        List<Collection> collections = vikingDBService.listCollections(); 
        for(Collection collection:collections){ 
            System.out.println(collection); 
        } 

        VectorIndexParams vectorIndex = new VectorIndexParams() 
                                        .setDistance(DistanceType.COSINE) 
                                        .setIndexType(IndexType.HNSW) 
                                        .setQuant(QuantType.Float) 
                                        .build(); 
        List<String> scalarIndex = new ArrayList<>(); 
        scalarIndex.add("price"); 
        scalarIndex.add("aim"); 
        CreateIndexParam createIndexParam = new CreateIndexParam() 
                                        .setCollectionName("javaSDKTest") 
                                        .setIndexName("test_index") 
                                        .setDescription("this is a test for index") 
                                        .setCpuQuoat(5) 
                                        .setVectorIndex(vectorIndex) 
                                        .setScalarIndex(scalarIndex) 
                                        .setPartitionBy("like") 
                                        .build(); 
        Index index = vikingDBService.createIndex(createIndexParam); 
        System.out.println(index); 

        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        System.out.println(index); 

        vikingDBService.dropIndex("javaSDKTest", "test_index"); 
    
        List<Index> indexes = vikingDBService.listIndexes("javaSDKTest"); 
        System.out.println(indexes); 

        HashMap<String,Object> field1 = new HashMap<String,Object>(); 
        List<String> author1 = new ArrayList<>(); 
        author1.add("name1"); 
        author1.add("name2"); 
        field1.put("doc_id", "11"); 
        field1.put("text_vector", genRandomVector(10)); 
        field1.put("like", 1); 
        field1.put("price", 1.11); 
        field1.put("aim", true); 
        field1.put("author", author1); 
        DataObject dataObject1 = new DataObject() 
                                .setFields(field1) 
                                .build(); 
        HashMap<String,Object> field2 = new HashMap<String,Object>(); 
        List<String> author2 = new ArrayList<>(); 
        author2.add("name3"); 
        author2.add("name4"); 
        field2.put("doc_id", "22"); 
        field2.put("text_vector", genRandomVector(10)); 
        field2.put("like", 2); 
        field2.put("price", 1.11); 
        field2.put("aim", false); 
        field2.put("author", author2); 
        DataObject dataObject2 = new DataObject() 
                                .setFields(field2) 
                                .build(); 
        HashMap<String,Object> field3 = new HashMap<String,Object>(); 
        List<String> author3 = new ArrayList<>(); 
        author3.add("name5"); 
        author3.add("name6"); 
        field3.put("doc_id", "33"); 
        field3.put("text_vector", genRandomVector(10)); 
        field3.put("like", 3); 
        field3.put("price", 3.33); 
        field3.put("aim", false); 
        field3.put("author", author3); 
        DataObject dataObject3 = new DataObject() 
                                .setFields(field3) 
                                .build(); 
        HashMap<String,Object> field4 = new HashMap<String,Object>(); 
        List<String> author4 = new ArrayList<>(); 
        author4.add("name7"); 
        author4.add("name8"); 
        field4.put("doc_id", "44"); 
        field4.put("text_vector", genRandomVector(10)); 
        field4.put("like", 4); 
        field4.put("price", 4.44); 
        field4.put("aim", false); 
        field4.put("author", author4); 
        DataObject dataObject4 = new DataObject() 
                                .setFields(field4) 
                                .build(); 
        Collection collection = vikingDBService.getCollection("javaSDKTest"); 
        List<DataObject> dataObjects = new ArrayList<>(); 
        dataObjects.add(dataObject1); 
        dataObjects.add(dataObject2); 
        dataObjects.add(dataObject3); 
        dataObjects.add(dataObject4); 
        collection.upsertData(dataObjects); 

        Collection collection = vikingDBService.getCollection("javaSDKTest"); 
        List<String> ids = new ArrayList<>(); 
        ids.add("11"); 
        ids.add("22"); 
        ids.add("33"); 
        ids.add("44"); 
        List<DataObject> dataObjects = collection.fetchData(ids); 
        System.out.println(dataObjects); 

        Collection collection = vikingDBService.getCollection("javaSDKTest"); 
        List<String> ids = new ArrayList<>(); 
        ids.add("11"); 
        ids.add("22"); 
        collection.deleteData(ids); 

        List<String> outputField = new ArrayList<>(); 
        outputField.add("doc_id"); 
        outputField.add("like"); 
        outputField.add("text_vector"); 
        HashMap<String, Object> filter = new HashMap<>(); 
        filter.put("op", "range"); 
        filter.put("field", "price"); 
        filter.put("lt", 4); 
        SearchByVectorParam searchByVectorParam = new SearchByVectorParam() 
                                                    .setVector(genRandomVector(10)) 
                                                    .setOutputFields(outputField) 
                                                    .setLimit(1) 
                                                    .setFilter(filter) 
                                                    .setPartition("default") 
                                                    .build(); 
        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        List<DataObject> datas = index.searchByVector(searchByVectorParam); 
        System.out.println(datas); 

        List<String> outputField = new ArrayList<>(); 
        outputField.add("doc_id"); 
        outputField.add("price"); 
        outputField.add("text_vector"); 
        HashMap<String, Object> filter = new HashMap<>(); 
        filter.put("op", "range"); 
        filter.put("field", "price"); 
        filter.put("lt", 4); 
        SearchByIdParam searchByIdParam = new SearchByIdParam() 
                                            .setOutputFields(outputField) 
                                            .setId("22") 
                                            .setPartition("default") 
                                            .setFilter(filter) 
                                            .setLimit(2) 
                                            .build(); 
        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        List<DataObject> datas = index.searchById(searchByIdParam); 
        System.out.println(datas); 

        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        List<String> outputField = new ArrayList<>(); 
        outputField.add("doc_id"); 
        outputField.add("like"); 
        outputField.add("text_vector"); 
        HashMap<String, Object> filter = new HashMap<>(); 
        filter.put("op", "range"); 
        filter.put("field", "price"); 
        filter.put("lt", 4); 
        List<DataObject> datas = index.search(new SearchParam() 
                                                .setVectorOrder(new VectorOrder().setVector(genRandomVector(10)).build()) 
                                                .setOutputFields(outputField) 
                                                .setPartition("default") 
                                                .setFilter(filter) 
                                                .setLimit(2) 
                                                .build()); 

        System.out.println(datas); 

        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        List<DataObject> datas = index.search(new SearchParam() 
                                                .setVectorOrder(new VectorOrder().setId("22").build()) 
                                                .setPartition("default") 
                                                .build()); 

        System.out.println(datas); 

        Index index = vikingDBService.getIndex("javaSDKTest", "test_index"); 
        List<DataObject> datas = index.search(new SearchParam() 
                                                .setScalarOrder(new ScalarOrder("price", Order.Asc).build()) 
                                                .setLimit(2) 
                                                .setPartition("default") 
                                                .build()); 
        System.out.println(datas); 

        ArrayList<String> ids = new ArrayList<>(); 
        ids.add("11"); 
        ids.add("22"); 
        ids.add("33"); 
        ids.add("44"); 
        Index index = vikingDBService.getIndex("test", "test_index"); 
        List<DataObject> dataObject = index.fetchData(ids, new FetchDataParam().setOutputFields(outputField).build()); 
        DataObject dataObject = index.fetchData("22", new FetchDataParam().setOutputFields(outputField).build()); 
        System.out.println(dataObject); 

        List<Double> res = vikingDBService.embedding(new EmbModel().setModelName("bge_large_zh").build(), new RawData().setDataType("text").setText("hello1").build()); 
        System.out.println(res); 

        ArrayList<RawData> rawDatas = new ArrayList<>(); 
        rawDatas.add(new RawData().setDataType("text").setText("hello1").build()); 
        rawDatas.add(new RawData().setDataType("text").setText("hello2").build()); 
        List<List<Double>> res = vikingDBService.embedding(new EmbModel().setModelName("bge_large_zh").build(), rawDatas); 
        for(List<Double> list: res){ 
            System.out.println(list); 
            System.out.println("-----------"); 
        } 

       List<Field> fields = new ArrayList<>(); 
       fields.add(new Field().setFieldName("doc_id").setFieldType(FieldType.String).setPrimaryKey(true).build()); 
       fields.add(new Field().setFieldName("text").setFieldType(FieldType.Text).setPipelineName("text_split_bge_large_zh").build()); 
       fields.add(new Field().setFieldName("like").setFieldType(FieldType.Int64).setDefaultVal(0).build()); 
       fields.add(new Field().setFieldName("price").setFieldType(FieldType.Float32).setDefaultVal(2.2).build()); 
       fields.add(new Field().setFieldName("aim").setFieldType(FieldType.Bool).setDefaultVal(false).build()); 
       CreateCollectionParam createCollectionParam = new CreateCollectionParam() 
                                                       .setCollectionName("test_text") 
                                                       .setFields(fields) 
                                                       .setDescription("test for text") 
                                                       .build(); 
       Collection collection = vikingDBService.createCollection(createCollectionParam); 

        VectorIndexParams vectorIndex = new VectorIndexParams() 
                                        .setDistance(DistanceType.COSINE) 
                                        .setIndexType(IndexType.HNSW) 
                                        .setQuant(QuantType.Float) 
                                        .build(); 
        List<String> scalarIndex = new ArrayList<>(); 
        scalarIndex.add("price"); 
        scalarIndex.add("like"); 
        CreateIndexParam createIndexParam = new CreateIndexParam() 
                                        .setCollectionName("test_text") 
                                        .setIndexName("test_index_text") 
                                        .setDescription("this is a test for index_text") 
                                        .setCpuQuoat(5) 
                                        .setVectorIndex(vectorIndex) 
                                        .setScalarIndex(scalarIndex) 
                                        .build(); 
        Index index = vikingDBService.createIndex(createIndexParam); 

        HashMap<String,Object> field1 = new HashMap<String,Object>(); 
        HashMap<String,String> text1 = new HashMap<>(); 
        text1.put("text", "this is one"); 
        field1.put("doc_id", "11"); 
        field1.put("text", text1); 
        field1.put("like", 1); 
        field1.put("price", 1.11); 
        field1.put("aim", true); 
        DataObject dataObject1 = new DataObject() 
                                .setFields(field1) 
                                .build(); 
        HashMap<String,Object> field2 = new HashMap<String,Object>(); 
        HashMap<String,String> text2 = new HashMap<>(); 
        text2.put("text", "this is two"); 
        field2.put("doc_id", "22"); 
        field2.put("text", text2); 
        field2.put("like", 2); 
        field2.put("price", 2.22); 
        field2.put("aim", false); 
        DataObject dataObject2 = new DataObject() 
                                .setFields(field2) 
                                .build(); 
        HashMap<String,Object> field3 = new HashMap<String,Object>(); 
        HashMap<String,String> text3 = new HashMap<>(); 
        text3.put("text", "this is three"); 
        field3.put("doc_id", "33"); 
        field3.put("text", text3); 
        field3.put("like", 3); 
        field3.put("price", 3.33); 
        field3.put("aim", false); 
        DataObject dataObject3 = new DataObject() 
                                .setFields(field3) 
                                .build(); 
        HashMap<String,Object> field4 = new HashMap<String,Object>(); 
        HashMap<String,String> text4 = new HashMap<>(); 
        text4.put("text", "this is four"); 
        field4.put("doc_id", "44"); 
        field4.put("text", text4); 
        field4.put("like", 4); 
        field4.put("price", 4.44); 
        field4.put("aim", false); 
        DataObject dataObject4 = new DataObject() 
                                .setFields(field4) 
                                .build(); 
        Collection collection = vikingDBService.getCollection("test_text"); 
        List<DataObject> dataObjects = new ArrayList<>(); 
        dataObjects.add(dataObject1); 
        dataObjects.add(dataObject2); 
        dataObjects.add(dataObject3); 
        dataObjects.add(dataObject4); 
        collection.upsertData(dataObject4); 

        Index index = vikingDBService.getIndex("test_text", "test_index_text"); 
        HashMap<String, Object> filter = new HashMap<>(); 
        filter.put("op", "range"); 
        filter.put("field", "price"); 
        filter.put("lt", 4); 
        Text text = new Text().setText("this.is test").build(); 
        SearchByTextParam searchByTextParam = new SearchByTextParam() 
                                                .setText(text) 
                                                .setFilter(filter) 
                                                .build(); 
        List<DataObject> datas = index.searchByText(searchByTextParam); 
        System.out.println(datas);
```
