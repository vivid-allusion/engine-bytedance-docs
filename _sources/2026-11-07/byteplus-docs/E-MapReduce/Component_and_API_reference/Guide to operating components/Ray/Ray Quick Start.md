---
title: "Ray Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_Quick_Start"
---

This section introduces how to quickly use Ray using the Core module and Data module. You can also refer to the official website [Getting Started](https://docs.ray.io/en/latest/ray-overview/getting-started.html).

<span id="21cf47fb"></span>
## Preparation

Deploy the Ray environment. It is recommended to deploy the Ray service in the EMR on VKE product. Refer to the [EMR official website](https://docs.byteplus.com/docs/E-MapReduce/109064) for environment deployment. You can also manually deploy Ray by following the instructions on the [official website](https://docs.ray.io/en/latest/ray-overview/installation.html) and running `pip install ray`.

<span id="a43a3870"></span>
## Ray Core module

The API provided by Ray Core horizontally scales Python tasks across a cluster. The most important APIs are two computation interfaces and one data interface.


* Task: A stateless parallel computation unit. This is a function\-oriented interface used to define a function that can be executed in a distributed manner within the cluster. When calling a function, use Ray's `@ray.remote` decorator to convert a regular Python function into a Task:

   ```Python
   import ray
   
   @ray.remote
   def add(x, y):
       return x + y
   
   # Call the function remotely.
   result_id = add.remote(1, 2)
   # Fetch the result.
   result = ray.get(result_id)  # result = 3
   ```
   

* Actor: A stateful parallel computation unit. This is a class\-oriented interface used to define a class that can be executed in a distributed manner within the cluster. Use Ray's `@ray.remote` decorator to convert a regular Python class into an Actor. Suitable for scenarios that require persistent state and long\-running operation.

   **Example**:

   ```Python
   import ray
   
   @ray.remote
   class Counter(object):
       def __init__(self):
           self.value = 0
   
       def increment(self):
           self.value += 1
           return self.value
   
   # Create an actor from this class.
   counter = Counter.remote()
   
   # Call the actor.
   ```
   

* Object: A distributed object that is immutable, used to transfer data between Tasks and Actors. Use `ray.get()` and `ray.put()` to load and retrieve data.


<span id="bb7ba475"></span>
## Ray Data module

Ray Data is a data processing framework based on Ray Core. It is a data processing library designed specifically for ML, mainly addressing data preparation and processing issues related to model training or inference, known as the last mile problem in data processing. For more information, refer to the official website [Offline Batch Inference](https://docs.ray.io/en/latest/data/overview.html#batch-inference-overview) and [Data Preprocessing and Ingestion for ML Training](https://docs.ray.io/en/latest/data/overview.html#preprocessing-and-ingest-for-ml-training).

Ray Data provides an abstract class for data: [Dataset](https://docs.ray.io/en/latest/data/api/dataset.html#ray.data.Dataset), a distributed data collection. Dataset provides common big data processing primitives, covering most stages of data processing, such as:


* Loading data: Data loading, such as reading Parquet files and more.

* Transforming data: Data transformation operations, such as [map_batches()](https://docs.ray.io/en/latest/data/api/doc/ray.data.Dataset.map_batches.html).

* Consuming data: Data consumption, such as using take_batch() and iter_batches() to access data.

* Saving data: Data saving, such as calling [write_parquet()](https://docs.ray.io/en/latest/data/api/doc/ray.data.Dataset.write_parquet.html#ray.data.Dataset.write_parquet) to save data in Parquet format to TOS object storage.


**Example**

```Python
from typing import Dict
import ray
from ray.data import Dataset

# Initialize Ray
ray.init()

def process_batch(batch: Dict[str, int]):
    # Square the data in each batch
    return {"result": [x ** 2 for x in batch["id"]]}


# Generate data using the range method
ds = ray.data.range(20)

# Use the map_batches method to process data in parallel
transformed_ds = ds.map_batches(process_batch, batch_size=4)

# Batch printing can be performed here
for batch in transformed_ds.iter_batches(batch_size=5):
    print(batch)

# Save the results locally
transformed_ds.write_parquet("local:///tmp/res/")
```
