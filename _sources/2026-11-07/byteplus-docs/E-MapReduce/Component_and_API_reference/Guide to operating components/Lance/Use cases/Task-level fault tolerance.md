---
title: "Task-level fault tolerance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Task-level_fault_tolerance"
---

<span id="94987271"></span>
## Background of the solution

When users use Ray to transform or preprocess data into Lance, Ray tasks may fail during execution, resulting in some data failing to be submitted completely. This situation causes significant inconvenience and potential issues for data processing. To address this challenge, we have proposed several business solutions to prevent full data reprocessing when Ray Core job submissions fail and restart. At the same time, we have conducted in\-depth research into multiple Lance\-related data processing scenarios and efficient usage approaches. Users can record processed files at the business layer by writing custom code, which helps avoid starting from scratch during recovery whenever possible.

**Key points include:** 


1. **RayCore checkpoint mechanism implementation**: By skillfully applying the decorator pattern, a universal checkpoint mechanism has been created. Task status is carefully checked and set both before and after function execution to ensure accuracy and completeness.

2. **Currently only supports OneToOneOperator operations**: At this stage, only OneToOneOperator operations are supported. Redis is used to record processed files; however, operations involving repartition or shuffle are currently not supported.


This means special attention must be paid to the type and scope of operations during data processing to avoid unnecessary errors and repeated processing. We will also continue to improve and expand the types of supported operations to enhance the efficiency and flexibility of data processing.

<span id="ac02688b"></span>
## Architecture of the solution

Because the design of the checkpoint is closely tied to the business, it is essential to implement fault tolerance measures at the business code level. By leveraging the logic of Ray job processing, we can segment at the file level.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/419fc7f4944543d4a5bb8d9e0258d8c6~tplv-goo7wpa0wc-image.image) </span>

Specifically, the overall Ray architecture diagram is shown above: at the business layer, it is important to clearly identify the smallest split point, starting from the file level, and to fully utilize external Redis or object storage as checkpoint storage to record in detail which files have been processed and which files have not yet been processed. At the same time, it is also necessary to consider factors such as file size, type, and processing priority to ensure the efficiency and accuracy of checkpoint storage. In addition, to improve system reliability and fault tolerance, a scheduled backup mechanism can be implemented to periodically back up checkpoint data to other storage media to prevent data loss or corruption.

**Design considerations**


* Implement pluggable checkpoint middleware using the decorator pattern to enhance system flexibility and scalability. This design allows middleware to be easily added or replaced without modifying the original code, meeting different business requirements and scenarios.

* Abstract the state storage layer and consider supporting Redis/TOS as storage media from a business perspective. This approach enables flexible selection of appropriate storage solutions based on actual application performance requirements, data scale, and cost budget, thereby improving system adaptability and efficiency.

* Provide exception state capture and metadata persistence capabilities so that when the system encounters an exception, relevant state information and metadata can be promptly captured and recorded to facilitate troubleshooting and recovery, ensuring system stability and reliability.

* When a RayData job fails to commit and restarts, it is not necessary to reprocess all data. This feature can significantly improve job execution efficiency and resource utilization.

   * Currently, only OneToOneOperator is supported, such as various forms of Map, including read, write, map, map_batches, limit, filter, and so on. This means that data can be processed in a one\-to\-one manner, ensuring data accuracy and consistency.

   * This solution does not support operations involving repartition or shuffle. This is due to the complexity and high resource consumption of such operations, which require further research and optimization to enable support.


<span id="d2d8efff"></span>
## Code sample

**Define external checkpoint storage**

We use the decorator pattern to implement a generic checkpoint mechanism. We can create a decorator that checks whether the task has been completed before the decorated function executes, and sets its status after execution. This approach can be applied to any functionality that needs to record execution status and support idempotent operations.

```Python
import ray
import redis
import functools
import hashlib
import lance
import pyarrow as pa
# --------------------------
# Redis checkpoint core module
# --------------------------
redis_conn = redis.Redis(host='localhost', port=6379)
def checkpoint(func):
    """简化的Checkpoint装饰器"""
    @functools.wraps(func)
    def wrapper(file_info):
        # Generate unique file identifier
        file_id = hashlib.md5(file_info['url'].encode()).hexdigest()
        key = f"checkpoint:{file_id}"
        
        # Check if processed
        if redis_conn.exists(key):
            print(f"跳过已处理文件: {file_info['url']}")
            return None
            
        try:
            # Execute processing task
            result = func(file_info)
            # Mark as completed
            redis_conn.set(key, "processed", ex=86400)  # 24-hour expiration
            return result
        except Exception as e:
            print(f"处理失败: {file_info['url']} - {str(e)}")
            raise
            
    return wrapper
```


**Process data based on business checkpoint**

```Python
# --------------------------
# Core data processing logic
# --------------------------
@ray.remote(max_retries=2)
@checkpoint
def process_file(file_info):
    """文件处理主逻辑"""
    print(f"开始处理: {file_info['url']}")
    
    # 1. Read text file
    data = []
    with open(file_info['url'], 'r') as f:
        for line in f:
            data.append({"text": line.strip().upper()})
    
    # 2. Convert to Arrow Table
    table = pa.Table.from_pylist(data)
    
    # 3. Write Lance file
    lance.write_dataset(table, file_info["output_path"],mode="append")
    print(f"成功写入: {file_info['output_path']}")
    return True

# --------------------------
# Task scheduling
# --------------------------
def run_pipeline(files, output_dir):
    """任务入口函数"""
    futures = []
    for file_url in files:
        output_path = f"{output_dir}/{file_url.split('/')[-1]}.lance"
        futures.append(process_file.remote({
            "url": file_url,
            "output_path": output_path
        }))
    
    # Wait for all tasks to complete
    ray.get(futures)
    print("所有文件处理完成！")

# --------------------------
# Usage example
# --------------------------
if __name__ == "__main__":
    # Initialize Ray
    ray.init()
    
    # Example file list
    input_files = [
        "/data/input/file1.txt",
        "/data/input/file2.txt"
    ]
    
    # Execute processing
    run_pipeline(input_files, "/data/output")
```


The overall sample mainly provides a basic design concept, including:


1. **Checkpoint module**

* Generate a unique file identifier using MD5 hash

* Record processing status with simple key\-value pairs in Redis

* Automatically skip processed files

2. **Core processing workflow**

* Stepwise comments: Read → Transform → Write

* Directly use `lance.write_dataset` to simplify the write logic

* Retain necessary retry mechanism (`max_retries=2`)

* Use native Lance write interface


For production design testing, you can contact EMR team technical experts for further consultation on idempotency handling and fault\-tolerant retries to ensure production availability.
