---
title: "How to perform performance analysis"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/How_to_perform_performance_analysis"
---

<span id="性能分析cpu火焰图简介"></span>
# Performance Analysis CPU Flame Diagram Introduction

Flame maps are used to visualize hierarchical data and help users quickly and accurately identify code call paths. Algorithm engineers can use the performance analysis function of the Machine Learning Platform to Create CPU Flame Graph, obtain the time consumption of each function in the code and the call relationship between each function, and analyze the performance bottleneck of the code.

In the flame diagram, each rectangle represents a function or method, and the width of the rectangle represents the proportion of the function or method in the total acquisition time. The wider the width, the greater the proportion. Each column matrix represents a call stack, and the height of the rectangle in the column indicates the depth of the function or method in the call stack. The higher the position, the deeper the call stack.

<span id="性能分析样例"></span>
## Performance Analysis Sample


* Code and link description


```python
def main ():                 #Call link description
    func1                    Link 1: main-func1-func3-func5-func6-func8
                             Link 2: main-func1-func3-func5-func7
    func2                    #Link 3: main-func2-fun4
    func4                    #Link 4: main-func4
    
def func1():
    func3
def func2():
    func4
def func3():
    func5
def func4():
def func5():
    func6
    func7
def func6():
    func8
def func7():
def func8():
```


The above code will obtain the following call link:


1. `main`\-\>`func1`\-\>`func3`\-\>`func5`\-\>`func6`\-\>`func8`

2. `main`\-\>`func1`\-\>`func3`\-\>`func5`\-\>`func7`

3. `main`\-\>`func2`\-\>`func4`

4. `main`\-\>`func4`

* CPU flame graph result


It can be seen from the analysis of flame diagram that the width of the topmost function `func8`is wider and takes up more CPU time. Although the width of the function `func5`is large, most of the CPU time is occupied by the function `func8`it calls, which itself takes up less CPU time. Similarly, the width of the function `func2`is large, but most of the CPU time is essentially occupied by the function `func4`. Therefore, if you want to improve the performance of the program, you should focus on the optimization analysis of function `func8`and function `func4`.

<span id="性能分析任务创建流程"></span>
# Performance Analysis Task Creating Process

<span id="前置条件"></span>
## precondition


1. The task is in the running state.

2. Only task Creators are allowed to submit profiling tasks.


<span id="提交流程"></span>
## submission process


1. Go to a custom tasks/inference service details page and click Create profiling.

2. Fill in the relevant configuration fields:

   1. Select process

      1. [ **Recommended** ] Case\-based analysis: Select all process analysis of an instance (POD).

      2. Process\-based analysis: Selecting a number of process analyses within an instance (POD).

   2. Duration of collection:

      Sampling is typically performed at a rate of 100 samples per second. The current function is continuously traced back to its caller until there is no longer a calling relationship, a single sampling.

   3. Select language:

      1. Python

> Only analyze all Python processes.


      3. C++

> Only all C++ processes are analyzed.


   4. Advanced Configuration

      1. Language is C++

         1. Configuration parameters:

            1. Perf: Implement data fetching of execution stack based on hardware PMU.

            2. BCC: Implement data fetching of the execution stack based on the eBPF mechanism provided by the kernel (currently not supported).

         2. Stack backtracking method: When the platform collects data, it directly collects the currently executing function. In order to generate the call stack of the function (that is, from the entry function to the entire call chain of the currently collected function), there needs to be a way to do stack backtracking. The current platform's Perf tool supports three stack backtracking methods. If there are no special circumstances, they are all in the fp mode:

            1. Fp [ **default choice** ]: Preserve relevant information in the generated code by reserving the frame pointer at compile time.

            2. Dwarf: Stack traceback based on compile\-time CFI information.

            3. LBR: Stack backtracking is based on the registers provided by the CPU, but requires support from newer CPU models, such as x86, etc. At the same time, the depth of the stack is also limited, generally 32 layers.

      2. When the language is Python

         1. Idle [ **turned on by default** ]: Under normal circumstances, the performance analysis tool will only perform stack traceback on the progress/thread executing on the CPU. When this option is turned on, it will grab the stack traceback of the progress/thread executing on the CPU and the stack traceback of the progress/thread not executing (idle) on the CPU.


<span id="创建结果样例"></span>
## Create Results Sample

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ee7e1fff7dab473bb2686634ccdd4eb.jpg) </span>

The above figure is a CPU flame graph collected by a Python program. The results of the performance analysis task mainly include the following modules:


1. Percentage of key functions (TOP10): Shows the ten functions that consume the most CPU time for this analysis task.

2. List of instances: Shows all the instances selected for this analysis task.

3. Sampling timing change: During the collection period, the change chart of the CPU sampling information of the analysis task (which can be understood as the change chart of CPU utilization during the sampling time). The horizontal axis is time, and the vertical axis is the number of samples. The more samples, the higher the CPU usage.

4. Function graph: Ranking according to the number of samples of the function in the flame graph, and showing the number and proportion of samples of the corresponding function.

5. Flame graph: Each column represents a call stack, and each matrix represents a function.

   1. Horizontal axis: The flame graph collects multiple call stack information, aggregating many information in a horizontal alphabetical manner. The width of the horizontal grid represents the frequency of its occurrence in the sample, so the larger the width of a grid, the more likely it is to be the cause of the bottleneck.

   2. Vertical axis: The depth of the function stack, arranged from bottom to top according to the calling relationship. The top grid represents the function that is consuming CPU resources at the time of sampling.

> When the fetching language is Python and the idle configuration is enabled, the vertical axis will contain information about the functions that are using and not using CPU resources.


<span id="差分-聚合功能"></span>
## Differential/Aggregation Functions

Machine Learning Platform Performance Analytics supports differential and aggregate analysis of multiple acquisition instances, which can be created on the performance analysis task details page.

<span id="差分火焰图"></span>
### differential flame diagram

The basic concept of differential flame diagram:


1. Benchmark flame graph: that is, the first task instance selected.

2. Contrast Flame Chart: Example of a task that compares to a baseline flame chart.

3. The temperature of the color represents the increase or decrease based on the benchmark flame map, the cool color is the decrease, and the warm color is the increase; the depth of the color represents the size of the difference, and the darker the color, the greater the difference.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f106feb5abc50686869ed1d29648c382.png) </span>

<span id="聚合火焰图"></span>
### Aggregate flame graph

Aggregate flame maps are mainly used to analyze the overall hotspots of multiple instances. The darker the color, the hotter the hotspots.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_712ac151932a1b86dcc0e713a6ed4c79.png) </span>

<span id="coming-soon"></span>
# Coming Soon


* Memory performance analysis

* GPU performance analysis
