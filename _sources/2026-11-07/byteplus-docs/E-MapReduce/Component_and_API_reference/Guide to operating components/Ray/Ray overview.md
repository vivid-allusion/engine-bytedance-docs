---
title: "Ray overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_overview"
---

<span id="c6094a6c"></span>
## What is Ray

Ray is an open\-source distributed computing framework designed to simplify the process of running distributed applications across various computing resources. Ray provides a set of simple and intuitive APIs, enabling developers to easily build, deploy, and manage large\-scale distributed applications. Based on this distributed computing framework, Ray offers a range of libraries for data science and artificial intelligence.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/652a3627e4f042e0b643092bd891c5d4~tplv-goo7wpa0wc-image.image) </span>

<span id="3a419f9e"></span>
### Ray Core

Ray's distributed computing foundation provides low\-level programming APIs, allowing users to conveniently convert single\-node programs into distributed computing tasks.

**Features**:


* Easy to use: The details of distributed execution are well encapsulated, so users can get started without extensive distributed computing experience.

* Minimal code changes required: Code modifications are straightforward.

* Good scalability: Modified Ray code can scale from a single local node to thousands of nodes.


**Related concepts**:


* Task: An interface for functions, used to define a function that can be executed in a distributed manner across the cluster.

* Actor: An interface for classes, used to define a class that can be instantiated and executed in a distributed manner across the cluster.

* Object: A distributed immutable object, used to transfer data between distributed Tasks and Actors.


<span id="ba561180"></span>
### Ray AI Libraries

Libraries for data science and artificial intelligence built on Ray Core, enabling a one\-stop pipeline for data reading, processing, training, and inference.


* Data: Provides data loading and transformation capabilities.

* Train: A distributed model framework based on Ray, supporting TF, PyTorch, Horovod, as well as training tools such as XGB and LightGBM.

* Tune: Scalable hyperparameter tuning to optimize model performance.

* Serve: Used to deploy models for online inference services.

* RLlib: A scalable distributed reinforcement learning library.


<span id="e7e94875"></span>
## What can Ray do


1. Machine learning: Ray provides a complete set of machine learning libraries, including tools for training and deploying machine learning models. For example, Ray's RLlib library is an open\-source library for reinforcement learning, making it easy to conduct large\-scale reinforcement learning training on Ray.

2. Data processing: Ray can be used for large\-scale data processing tasks, such as data cleaning, data transformation, data analysis, and more. The Modin library of Ray is an open\-source library for large\-scale data processing. It distributes Pandas data processing operations across multiple nodes, enabling fast data processing.

3. Distributed systems: Ray provides a simple set of APIs that can be used to build and run distributed systems. For example, Ray's Serve library is an open\-source library for building and running distributed services, making it easy to deploy and scale services on Ray.

4. High\-performance computing: Ray's distributed computing capabilities can be used for various high\-performance computing tasks, such as scientific computing, simulation, optimization, and more.

5. Real\-time computing: Used for real\-time computing tasks, such as real\-time data analysis, real\-time machine learning, and more. Ray's real\-time computing capabilities mainly come from the Actor model and distributed task scheduling capabilities.


<span id="f77cbb7b"></span>
### Architecture

A Ray cluster consists of a group of Worker nodes and a Head node. A Ray cluster can be of fixed size or can automatically scale based on the application workload running on the cluster. Please refer to the official website [Ray Clusters Overview](https://docs.ray.io/en/master/cluster/getting-started.html)

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1e8455a9ff648bdb47d7e374b26241e~tplv-goo7wpa0wc-image.image" width="1758px" /></div>



* Head node: The control center of the cluster, responsible for managing the overall cluster state, scheduling tasks, and allocating resources.

   * Global Control Store is a component used to store cluster state and metadata information.

   * AutoScaler is a component that automatically increases or decreases the number of worker nodes based on the current workload.

   * Raylet is responsible for task scheduling and resource management.

* Worker Node is a node that executes actual computing tasks.


After Ray Cluster is deployed, you can submit jobs on the Ray Cluster. There are two ways to submit jobs. For specific usage, please refer to [RayCluster Quick Start](https://docs.byteplus.com/docs/undefined/69aa398f8252b50542cbfa68) and [RayJob Quick Start](https://docs.byteplus.com/docs/undefined/69aa3952ecb469056b16c9f9).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c07f497989544f7a997d959adbab5000~tplv-goo7wpa0wc-image.image" width="1440px" /></div>


<span id="5b7f8238"></span>
### **Main features**


1. Ease of use: Ray provides a simple set of APIs, allowing developers to easily write distributed applications.

2. Performance: Ray has designed a new scheduling algorithm that enables efficient task scheduling on large\-scale clusters.

3. Flexibility: Ray supports a variety of computation models, including batch processing, stream processing, graph computation, and more.

4. Scalability: Ray can run on clusters with thousands of nodes, supporting large\-scale computing tasks.

5. Integration: Ray can seamlessly integrate with other popular data processing and machine learning frameworks, such as TensorFlow, PyTorch, and more.


<span id="32142f80"></span>
### How to use Ray

The core APIs of Ray include the following key concepts:


1. `ray.init()`: Initializes the Ray cluster. You can pass an address to connect to an existing cluster.

2. `@ray.remote`: Converts a function into a task and a class into an actor.

3. `ray.put()`: Places a value into Ray's object store.

4. `ray.get()`: Retrieves a value from the object store. Returns the value you previously placed, or the result computed by a task or actor.

5. `.remote()`: Runs actor methods or tasks on the Ray cluster and is used to instantiate actors.

6. `ray.wait()`: Returns two lists of object references, one containing completed tasks and the other containing unfinished tasks.


**Example**:

A simple example illustrates how Ray works. Suppose there is a database from which you want to retrieve data. The following is an example of parallel processing using Ray:

```Python
import ray
import time

start = time.time()
# Python list simulating a database
database = ["Learning", "Ray", "Flexible", "Distributed", "Python", "for", "Machine", "Learning"]

# Use the ray.remote decorator to convert a function into a Ray task
@ray.remote
def retrieve_task(item):
    time.sleep(item / 10.)
    return item, database[item]

# Launch Ray tasks and collect their references
object_references = [retrieve_task.remote(item) for item in range(5)]

# Use ray.get() to obtain task results
data = ray.get(object_references)

# Print the time required to retrieve the data
print(f'Runtime: {time.time() - start:.2f} seconds, data:')
print(*data, sep="\n")
```


<span id="d5c19682"></span>
## Ray on EMR

This directory contains instructions for using the semi\-managed EMR version of the Ray component. For instructions on the fully managed EMR Serverless component, see: [Serverless Ray parameter description](https://docs.byteplus.com/docs/E-MapReduce/95182).
