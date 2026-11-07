---
title: "Word frequency statistics using Ray (WordCount)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ray_word_frequency_statistics_using_ray"
---

This section introduces an example of using Ray to perform word frequency statistics (Word Count).

<span id="_1-简介"></span>
## 1 **Introduction**

MapReduce is a distributed computing model that divides the processing of large datasets into three stages:


1. **Map stage**: Applies a specified function to each element in the dataset for transformation or mapping, generating key\-value pairs where the key represents an element and the value is a metric calculated for that element.

2. **Shuffle stage**: Collects all outputs from the Map stage and organizes them by key. If the same key appears on multiple compute nodes, this stage includes transferring or shuffling data between different nodes.

3. **Reduce stage**: Aggregates the elements from the Shuffle stage. The total number of occurrences for each word is the sum of its occurrences on each node.


<span id="_2-使用指导"></span>
## 2 Usage guide


1. First, define two functions:

   1. `map_task`: This function takes a segment of text as input and then counts the number of occurrences of each word in that segment. It uses a dictionary `word_counts` to Save each word and its occurrence count.

   2. `reduce_task`: This function is used to merge the results of multiple `map_task` tasks. It takes multiple dictionaries as input (that is, the output of each `map_task`) and merges them into a single dictionary containing all words and their total occurrence counts.

2. Parallel processing of text data: Using a list comprehension and the `map_task.remote()` method, a Ray task is created for each segment of text and submitted to the Ray runtime for parallel processing.

3. Next, merge the processing results: Use `reduce_task.remote(*map_results)` to pass all `map_task` results as arguments to `reduce_task`, merging these results in parallel.

4. Finally, retrieve and print the result: Use `ray.get(reduce_result)` to obtain the execution result of `reduce_task`.

5. Complete sample code

   Contents of the wordcount.py file

   ```python
   import ray
   
   # Initialize Ray
   ray.init()
   
   # Define a Ray task
   @ray.remote
   def map_task(text):
       # Count word frequencies
       word_counts = {}
       for word in text.split():
           if word in word_counts:
               word_counts[word] += 1
           else:
               word_counts[word] = 1
       return word_counts
   
   # Define another Ray task
   @ray.remote
   def reduce_task(*word_counts_list):
       # Merge word frequency statistics
       word_counts = {}
       for word_counts_dict in word_counts_list:
           for word, count in word_counts_dict.items():
               if word in word_counts:
                   word_counts[word] += count
               else:
                   word_counts[word] = count
       return word_counts
   
   # Text data
   texts = ['hello world', 'world world', 'hello hello world']
   
   # Use Ray tasks to process text data in parallel
   map_results = [map_task.remote(text) for text in texts]
   
   # Use Ray tasks to merge processing results
   reduce_result = reduce_task.remote(*map_results)
   
   # Retrieve and print results
   result = ray.get(reduce_result)
   print(result)
   ```
   

6. Run the above Python code

   ```shell
   ray job submit --working-dir . -- python wordcount.py
   ```
   

7. View the execution result:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_517b9a87c4b43aabf5073000832e7c29.png) </span>


Summary: This use case demonstrates how the Ray framework simplifies the implementation of distributed computing tasks. By breaking computations down into multiple small tasks (Map phase), then executing these tasks in parallel across multiple cores or nodes, and finally merging the results (Reduce phase), Ray can efficiently process large\-scale datasets. This approach is very common in big data processing and distributed machine learning.
