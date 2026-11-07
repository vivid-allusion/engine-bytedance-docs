---
title: "Practical guide for converting traditional Python programs to Ray programs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Practical_guide_for_converting_traditional_Python_programs_to_Ray_programs"
---

Ray is a flexible distributed computing framework that supports parallel tasks and asynchronous execution based on the actor model. By converting traditional Python programs to Ray programs, you can fully leverage Ray's parallel and distributed computing capabilities to improve program performance and scalability. This article provides a detailed introduction to converting both standalone Python programs and multiprocess programs to Ray programs.

<span id="839ba78c"></span>
## Ray API introduction


|**API** |**Description** |**Example** |
|---|---|---|
|ray.init() |Initialize the Ray context. | |
|@ray.remote |A decorator for functions or classes, specifying that the function will be executed as a task and the class as an actor, running in different processes. |```Python```<br>```@ray.remote```<br>```class Actor(object):```<br>```    def method(y)```<br>```        ...                                     …```<br> |
|.remote |Used for each remote function, remote class declaration, or remote class method call. Remote operations are asynchronous. |```Python```<br>```ret_id = fun.remote(x)```<br>```a = Actor.remote()```<br>```ret_id = a.method.remote(y)```<br> |
|ray.put() |Stores an object in the object store and returns its ID. This ID can be used to pass the object as a parameter to any remote function or method call. This is a synchronous operation. |```Python```<br>```x_id = ray.put(x)```<br> |
|ray.get() |Returns an object or a list of objects from an object ID or a list of object IDs. This is a synchronous (that is, blocking) operation. |```Python```<br>```x = ray.get(x_id)```<br>```…```<br>```objects = ray.get(object_ids)```<br> |
|ray.wait() |Returns two lists from a list of object IDs: one containing the ready object IDs, and one containing the object IDs that are not yet ready. |```Python```<br>```ready_ids, not_ready_ids = ray.wait(object_ids)```<br> |


<span id="ec0b8e5c"></span>
## Conversion scenarios for traditional Python programs to Ray programs

<span id="8b444d52"></span>
### Preparation

Deploy the Ray environment. It is recommended to deploy Ray services in the EMR on VKE product. Refer to [EMR official website](https://docs.byteplus.com/docs/E-MapReduce/109064) for environment deployment. You can also perform manual deployment by following the [official website](https://docs.ray.io/en/latest/ray-overview/installation.html) and using `pip install ray`.

<span id="46e14e64"></span>
### Converting standalone Python programs to Ray programs

**Example:** 

Calculate the squares of a set of numbers.


|**Traditional single\-machine Python program** |**Refactor as a Ray program** |
|---|---|
|```Python```<br>```def compute_square(x):```<br>```    return x * x```<br>``````<br>```numbers = [1, 2, 3, 4, 5]```<br>```squares = [compute_square(x) for x in numbers]```<br>```print(squares)```<br> |```Python```<br>```import ray```<br>``````<br>```# Initialize Ray```<br>```ray.init()```<br>``````<br>```# Convert function to Ray task```<br>```@ray.remote```<br>```def compute_square(x):```<br>```    return x * x```<br>``````<br>```numbers = [1, 2, 3, 4, 5]```<br>``````<br>```# Asynchronously invoke Ray task```<br>```futures = [compute_square.remote(x) for x in numbers]```<br>``````<br>```# Retrieve task results```<br>```squares = ray.get(futures)```<br>```print(squares)```<br>``````<br>```# Shut down Ray```<br>```ray.shutdown()```<br> |


**Conversion steps:** 


1. Import Ray and initialize the Ray cluster.

2. Use the `@ray.remote` decorator to convert functions into Ray tasks.

3. Call Ray tasks using the `.remote()` method.

4. Retrieve task results using `ray.get()`.


<span id="38fdaada"></span>
### Converting multiprocess programs to Ray programs

**Example:** 

Process multiple data blocks in parallel.


|**Traditional multi\-process Python program** |**Ray program** |
|---|---|
|```Python```<br>```import multiprocessing```<br>``````<br>```def process_data(data):```<br>```    return [x * 2 for x in data]```<br>``````<br>```data_chunks = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]```<br>``````<br>```with multiprocessing.Pool(processes=3) as pool:```<br>```    results = pool.map(process_data, data_chunks)```<br>``````<br>```print(results)```<br> |```Python```<br>```import ray```<br>``````<br>```# Initialize Ray```<br>```ray.init()```<br>``````<br>```# Convert function to Ray task```<br>```@ray.remote```<br>```def process_data(data):```<br>```    return [x * 2 for x in data]```<br>``````<br>```data_chunks = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]```<br>``````<br>```# Asynchronously invoke Ray task```<br>```futures = [process_data.remote(chunk) for chunk in data_chunks]```<br>``````<br>```# Retrieve task results```<br>```results = ray.get(futures)```<br>```print(results)```<br>``````<br>```# Shut down Ray```<br>```ray.shutdown()```<br> |
| | |


**Steps for converting to Ray programs**:


1. Import Ray and initialize the Ray cluster.

2. Use the `@ray.remote` decorator to convert functions into Ray tasks.

3. Call Ray tasks using the `.remote()` method.

4. Retrieve task results using `ray.get()`.


**Advantages of converting to Ray programs:** 


* Efficient data processing:

   * Ray provides shared object storage, avoiding the serialization and deserialization overhead when passing large objects between processes in Python multiprocessing.

   * For stateful computation: Ray offers the actor abstraction, making it simple to encapsulate and modify state in a distributed environment. Python multiprocessing lacks this natural parallelization approach, resulting in complex implementations and poor performance.

* Scalability and fault tolerance:

   * Distributed computing: Ray is designed for scalability and can run the same code on a single machine, a cluster, or even in a cloud environment. It can easily scale to hundreds or even thousands of nodes.

   * Automatic fault recovery: Ray workloads automatically recover from machine and process failures, ensuring reliability and stability of computing tasks.


<span id="00a928e2"></span>
### Refactor the pipeline workflow using the Ray Data module

The Ray Data module uses `Dataset` to define distributed datasets. To perform a series of pipeline operations on a dataset, the Ray Data model can be used.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ad685ddee5c464c9b123da76571482f~tplv-goo7wpa0wc-image.image) </span>

Example:


|`multiprocessing` example |Ray example |
|---|---|
|```Python```<br>```import multiprocessing```<br>```import time```<br>``````<br>``````<br>```# Data processing step 1```<br>```def process_step1(data):```<br>```    time.sleep(1)```<br>```    return [item * 2 for item in data]```<br>``````<br>```# Data processing step 2```<br>```def process_step2(data):```<br>```    time.sleep(1)```<br>```    return [item + 5 for item in data]```<br>``````<br>```# Data processing step 3```<br>```def process_step3(data):```<br>```    time.sleep(1)```<br>```    return [item * 3 for item in data]```<br>``````<br>```if __name__ == '__main__':```<br>```    data = [i for i in range(10)]```<br>``````<br>```    # Parallel processing using multiprocessing```<br>```    pool = multiprocessing.Pool()```<br>``````<br>```    step1_results = pool.apply_async(process_step1, (data,))```<br>```    step2_input = step1_results.get()```<br>```    step2_results = pool.apply_async(process_step2, (step2_input,))```<br>```    step3_input = step2_results.get()```<br>```    final_results = pool.apply_async(process_step3, (step3_input,))```<br>``````<br>```    pool.close()```<br>```    pool.join()```<br>``````<br>```    print(final_results.get())```<br> |```Python```<br>```import ray```<br>```import time```<br>```from typing import Dict```<br>``````<br>```ray.init()```<br>``````<br>```# Data processing step 1, the type of data is: Dict[str, int]```<br>```def process_step1(data):```<br>```    time.sleep(1)```<br>```    return {'id':[item * 2 for item in data['id']]}```<br>``````<br>```# Data processing step 2```<br>```def process_step2(data):```<br>```    time.sleep(1)```<br>```    return {'id':[item + 5 for item in data['id']]}```<br>``````<br>```# Data processing step 3```<br>```def process_step3(data):```<br>```    time.sleep(1)```<br>```    return {'id':[item * 3 for item in data['id']]}```<br>``````<br>```if __name__ == '__main__':```<br>```    # Start data generation task```<br>```    result = ray.data.range(10)\```<br>```        .map_batches(process_step1)\```<br>```        .map_batches(process_step2)\```<br>```        .map_batches(process_step3)\```<br>```        .take_all()```<br>``````<br>```    # ray.data.Dataset can include schema metadata.```<br>```    # The returned results here are {'id': 27}, {'id': 15}, {'id': 21}, {'id': 69}, {'id': 39}, {'id': 63}, {'id': 57}, {'id': 51}, {'id': 33}, {'id': 45}```<br>```    print(result)```<br>``````<br>```    ray.shutdown()```<br> |


<span id="541f5f54"></span>
## Important notes for using the Ray API

<span id="45e2c042"></span>
### Calling remote functions and methods

Remote function and method calls are asynchronous and return an object ID (ObjectID) instead of the actual result. To obtain the actual result, use `ray.get()`.

```Python
# Asynchronous invocation
result_id = my_function.remote(5)

# Retrieve results
result = ray.get(result_id)
```


<span id="41a4cad3"></span>
### Delay calling `ray.get()`

`ray.get()` is a blocking operation and waits until the result is ready. Calling `ray.get()` too early will block other operations in the program and affect parallelism. It is recommended to call `ray.get()` after all tasks have been launched.

```Python
# Not recommended
results = [ray.get(my_function.remote(x)) for x in range(4)]

# Recommended
result_ids = [my_function.remote(x) for x in range(4)]
results = ray.get(result_ids)
```


<span id="7d3575a5"></span>
### Avoid small tasks

Each remote task call incurs some overhead. If a task is very small, a Ray program may be slower than an equivalent Python program. It is recommended to design tasks to take at least several milliseconds to amortize the overhead of calls.

```Python
# Not recommended
@ray.remote
def tiny_task(x):
    return x

# Recommended
@ray.remote
def larger_task(start, end):
    return [x for x in range(start, end)]
```


<span id="cb0fed8a"></span>
### Use `ray.put()` to store large objects

When passing a large object as a parameter to a remote function, Ray will call `ray.put()` in the background to store the object in the local object store. If the same large object is passed multiple times, it is recommended to explicitly call `ray.put()` and pass its ID to avoid duplicating the object.

```Python
# Not recommended
result_ids = [my_function.remote(large_object) for _ in range(10)]

# Recommended
large_object_id = ray.put(large_object)
result_ids = [my_function.remote(large_object_id) for _ in range(10)]
```


<span id="e296f734"></span>
### Use `ray.wait()` to process results as early as possible

When using `ray.get()` for the results of multiple tasks, you must wait for the last task to finish, which increases the program's runtime. It is recommended to use `ray.wait()`, which returns as soon as any object is ready, allowing results to be processed earlier.

```Python
result_ids = [my_function.remote(x) for x in range(4)]
while result_ids:
    done_id, result_ids = ray.wait(result_ids)
    result = ray.get(done_id[0])
    process_result(result)
```
