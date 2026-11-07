---
title: "upsert_data"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_upsert_data"
---

<span id="3f21fc7b"></span>
# Overview

The `upsert_data` method inserts new data or updates existing data within a specified Collection. This method supports writing data individually or in batches of up to 100 entries per request. For large\-scale data ingestion scenarios, you can enable the asynchronous mode to achieve a significant performance improvement.

<span id="780c82f5"></span>
# **Request parameters**


|**parameter name** |**sub\-parameter** |**type** |**Required?**  |**parameter description** |
|---|---|---|---|---|
|Data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data instance or list of Data instances.</div><br> |Fields |Array\ < map \> |Yes |Specifies the data to be written.<br><br><br>* A single request can write a maximum of 100 items.<br><br>* Each data item is a map where keys are field names and values are the corresponding field values.<br><br>* The total size of the field data cannot exceed 65,535 bytes. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: An integer value.<br><br>   * Float: A floating\-point value.<br><br>   * String: A string.<br><br>   * Bool: A boolean value (`true` or `false`).<br><br>   * List: An array of strings.<br><br>   * List: An array of integers.<br><br>   * Vector: An array of floating\-point numbers.<br><br>   * sparse_vector: A JSON object where each key is a string representing a keyword and its value is a float representing the keyword's weight.<br><br>   * Text: A map that must contain the key "text" with a string value.<br><br>      * Text: Write text as a string to the original data source, such as {"text": "hello world"}.<br><br>   * Image: Currently supports writing TOS paths. The format is`tos://{bucket}/{object_key}`. |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 or a positive integer.<br><br>* Default value: 0, which indicates that the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Data deleted due to TTL expiration is not immediately removed from the index. |
|async_upsert |*  |Bool |No |Specifies whether to make an asynchronous request. This mode is suitable for large\-scale data writing scenarios and can improve performance by up to 10 times.<br><br><br>* True: Indicates an asynchronous request.<br><br>* Default: `False`, which indicates a synchronous request. |


<span id="f673af74"></span>
# Example

<span id="020ce88a"></span>
## Request parameters

Synchronous write data example:

```Python
collection = vikingdb_service.get_collection("example")
```


```Python
def gen_random_vector(dim):
    res = [0, ] * dim
    for i in range(dim):
        res[i] = random.random() - 0.5
    return res
   
field1 = {"doc_id": "11", "text_vector": gen_random_vector(12), "text_sparse_vector": {"hello": 0.34, "world": 0.03, "!": 0.11}, "like": 1, "price": 1.11,
          "author": ["gy"], "aim": True}
field2 = {"doc_id": "22", "text_vector": gen_random_vector(12), "text_sparse_vector": {"hi": 0.12, "there": 0.043, "!": 0.5},"like": 2, "price": 2.22,
          "author": ["gy", "xjq"], "aim": False}
data1 = Data(field1)
data2 = Data(field2)
datas = []
datas.append(data1)
datas.append(data2)
collection.upsert_data(datas)  


async def upsert_data():
    def gen_random_vector(dim):
        res = [0, ] * dim
        for i in range(dim):
            res[i] = random.random() - 0.5
        return res


    collection = await vikingdb_service.async_get_collection("async")
    field1 = {"doc_id": "111", "text_vector": gen_random_vector(10), "like": 1, "price": 1.11,
             "author": ["gy"], "aim": True}
    field2 = {"doc_id": "222", "text_vector": gen_random_vector(10), "like": 2, "price": 2.22,
             "author": ["gy", "xjq"], "aim": False}
    field3 = {"doc_id": "333", "text_vector": gen_random_vector(10), "like": 3, "price": 3.33,
             "author": ["gy", "xjq"], "aim": False}
    field4 = {"doc_id": "444", "text_vector": gen_random_vector(10), "like": 4, "price": 4.44,
             "author": ["gy", "xjq"], "aim": False}
    data1 = Data(field1)
    data2 = Data(field2)
    data3 = Data(field3)
    data4 = Data(field4)
    datas = [data1, data2, data3, data4]
    await collection.async_upsert_data(datas)
asyncio.run(upsert_data())
```


Example of writing data asynchronously:

```Python
import multiprocessing
import struct, base64, uuid, tqdm, time
from volcengine.viking_db import *

queue = multiprocessing.Queue(maxsize=10)
event = multiprocessing.Event()

def consumer():
    """Consumer function: Retrieve data from the queue and process it"""
    vikingdb_service = VikingDBService()
    vikingdb_service.set_ak("ak")
    vikingdb_service.set_sk("sk")
    collection = vikingdb_service.get_collection("")
    items = []
    while not event.is_set() or not queue.empty():
        item = queue.get()
        items.append(item)
        if len(items) == 50:
            collection.upsert_data(items, async_upsert=True)
            items = []

    print("Consumer received event. Exiting...")

if __name__ == "__main__":
    # Create consumer processes
    processors = []
    for i in range(10):
        p = multiprocessing.Process(target=consumer)
        p.start()
        processors.append(p)

    # Prepare data
    datas = []
    for i in range(100000):  
        # Compress the vector
        float_array = [0.124135132531424]*1024
        packed_data = struct.pack('f'*len(float_array), *float_array)
        s =  base64.b64encode(packed_data).decode()
        uuid4 = uuid.uuid4()  # User can modify this to the desired ID
        datas.append(Data({"id": str(uuid4), "text_vertor": s}))
    
    for data in tqdm.tqdm(datas):
        queue.put(data)
    # Notify consumers to stop working
    event.set()
    for p in processors:
        p.join()

    print("Main process exiting...")
```


<span id="4c86cdf2"></span>
## Return value

Upon successful execution, this function does not return a value.
