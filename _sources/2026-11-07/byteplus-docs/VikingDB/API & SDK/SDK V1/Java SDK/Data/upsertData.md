---
title: "upsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_upsertData"
---

<span id="354cb780"></span>
# Overview

upsertData is used to write data in the specified dataset Collection. The specified data written is an array, allowing one or more pieces of data to be inserted at a time, up to 100 pieces of data can be inserted at a time.

<span id="d6ac23e8"></span>
# **request parameters**


|**parameter name** |**sub\-parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|---|
|DataObject<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataObject instance or list of instances.</div><br> |Fields |Array\ < map \> |Yes |Specifies the data to be written.<br><br><br>* The number of data written in a single write does not exceed 100.<br><br>* Each piece of data is used as a map, with key as the field name and value as the field value.<br><br>* The maximum length of fields when data is written is 65535. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: The format is string.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: The format is vector (array of floating\-point numbers).<br><br>   * sparse_vector: The format is a json dictionary, k is a string type, which represents the literal of the keyword, and v is a float type, which represents the weight value of the keyword.<br><br>   * Text: The format is map < string, string \>, currently text is supported.<br><br>      * Text: Write text as a string to the original data source, such as {"text": "hello world"}.<br><br>   * Image: Currently supports writing tos paths. The format is`tos://{bucket}/{object_key}`. |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 and a positive integer.<br><br>* Default value: Default is 0, indicating that the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Data ttl is deleted and will not be updated to the index immediately. |
|async_upsert |*  |Bool |No |Whether it is asynchronous request interface, suitable for large\-scale data writing scenarios, and the performance is improved by 10 times.<br><br><br>* True: Indicates an asynchronous request for writing.<br><br>* Default: Default is False, indicating a normal request. |


<span id="b9dcb66d"></span>
# Example

<span id="2b21aeaa"></span>
## Request parameters

```Java
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


```Java
HashMap field1 = new HashMap();
List author1 = new ArrayList<>();
author1.add("name1");
author1.add("name2");
field1.put("doc_id", "11");
field1.put("text_vector", genRandomVector(12));
field1.put("text_sparse_vector", {"hello": 0.34, "world": 0.03, "!": 0.11});
field1.put("like", 1);
field1.put("price", 1.11);
field1.put("aim", true);
field1.put("author", author1);
DataObject dataObject1 = new DataObject()
                        .setFields(field1)
                        .build();
HashMap field2 = new HashMap();
List author2 = new ArrayList<>();
author2.add("name3");
author2.add("name4");
field2.put("doc_id", "22");
field2.put("text_vector", genRandomVector(12));
field2.put("text_sparse_vector", {"hi": 0.12, "there": 0.043, "!": 0.5});
field2.put("like", 2);
field2.put("price", 1.11);
field2.put("aim", false);
field2.put("author", author2);
DataObject dataObject2 = new DataObject()
                        .setFields(field2)
                        .build();
HashMap field3 = new HashMap();
List author3 = new ArrayList<>();
author3.add("name5");
author3.add("name6");
field3.put("doc_id", "33");
field3.put("text_vector", genRandomVector(12));
field3.put("text_sparse_vector", {"hi": 0.12, "there": 0.043, "!": 0.5});
field3.put("like", 3);
field3.put("price", 3.33);
field3.put("aim", false);
field3.put("author", author3);
DataObject dataObject3 = new DataObject()
                        .setFields(field3)
                        .build();
HashMap field4 = new HashMap();
List author4 = new ArrayList<>();
author4.add("name7");
author4.add("name8");
field4.put("doc_id", "44");
field4.put("text_vector", genRandomVector(12));
field4.put("text_sparse_vector", {"hi": 0.12, "there": 0.043, "!": 0.5});
field4.put("like", 4);
field4.put("price", 4.44);
field4.put("aim", false);
field4.put("author", author4);
DataObject dataObject4 = new DataObject()
                        .setFields(field4)
                        .build();

List dataObjects = new ArrayList<>();
dataObjects.add(dataObject1);
dataObjects.add(dataObject2);
dataObjects.add(dataObject3);
dataObjects.add(dataObject4);
collection.upsertData(dataObjects);
```


Example of writing data asynchronously:

```Java
class Consumer implements Runnable {
    private final LinkedBlockingQueue queue;
    private final AtomicBoolean event;
    
    public Consumer(LinkedBlockingQueue queue, AtomicBoolean event) {
        this.queue = queue;
        this.event = event;
    }

    @Override
    public void run() {
        VikingDBService vikingdbService = null;
        try {
            vikingdbService = new VikingDBService();
        } catch (Exception e) {
            e.printStackTrace();
        }
        Collection collection = null;
        try {
            collection = vikingdbService.getCollection("");
        } catch (Exception e) {
            e.printStackTrace();
        }
        List items = new ArrayList<>();
        
        while (!event.get() || !queue.isEmpty()) {
            try {
                DataObject item = queue.poll(1, TimeUnit.SECONDS);
                if (item != null) {
                    items.add(item);
                    if (items.size() == 50) {
                        try {
                            collection.upsertData(items, true);
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                        items.clear();
                    }
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }

        System.out.println("Consumer received event. Exiting...");
    }
}

public class test {
    public static List genRandomVector(int dim){
        List res = new ArrayList<>();
        for(int i=0;i
            res.add(new Random().nextDouble());
        }
        return res;
    }
    
    public static void main(String[] args) throws Exception {
        VikingDBService vikingDBService = new VikingDBService();
        LinkedBlockingQueue queue = new LinkedBlockingQueue<>(10);
        AtomicBoolean event = new AtomicBoolean(false);
        List processors = new ArrayList<>();
        
        for (int i = 0; i < 10; i++) {
            Thread p = new Thread(new Consumer(queue, event));
            p.start();
            processors.add(p);
        }
        int num = 10000;

        List datas = new ArrayList<>();
        for (int i = 0; i < num; i++) {
            float[] floatArray = new float[1024];
            Arrays.fill(floatArray, 0.124135132531424f);
            ByteBuffer byteBuffer = ByteBuffer.allocate(floatArray.length * Float.BYTES);
            byteBuffer.asFloatBuffer().put(floatArray);
            String s = Base64.getEncoder().encodeToString(byteBuffer.array());
            UUID uuid4 = UUID.randomUUID(); 

            HashMap field = new HashMap();
            field.put("id", uuid4);
            field.put("text_vector", s);
            DataObject dataObject = new DataObject()
               .setFields(field)
               .build();
            datas.add(dataObject);
        }

        ProgressBar pb = new ProgressBar("Processing", num);
        for (DataObject data : datas) {
            queue.put(data);
            pb.step();
        }
        pb.close();

        event.set(true);
        for (Thread p : processors) {
            p.join();
        }
        System.out.println("Main process exiting...");
     }
 }
```


<span id="ebe9ae9b"></span>
## Return value

Java call to execute the above task, the execution is successful without return information.
