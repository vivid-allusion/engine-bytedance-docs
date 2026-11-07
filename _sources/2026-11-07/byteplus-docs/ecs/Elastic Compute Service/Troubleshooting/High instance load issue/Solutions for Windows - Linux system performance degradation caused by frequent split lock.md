---
title: "Solutions for Windows/Linux system performance degradation caused by frequent split lock triggers in the code"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/performance_degradation_caused_by_frequent_split_lock_triggers_in_the_code"
---

This topic mainly describes how to troubleshoot performance degradation issues (such as abnormal increases in CPU usage and program stuttering) caused by frequent split locks triggered by the code.

> This topic may contain information about third\-party products. Related information is for reference only. BytePlus does not make any implied guarantees or other forms of commitments for the performance, reliability, or potential impacts of operations that involve any third\-party product.


<span id="Wsl6lNkq"></span>
## Problem description

When you use instances with AMD CPU specifications (architecture such as Genoa, Turin, etc.), the instance computing performance may decrease significantly when split locks are frequently triggered. For example, CPU usage may increase abnormally and programs may stutter.

<span id="9JmRhqiD"></span>
## Causes

Due to the granularity of the cache consistency protocol being one cache line, when atomic operation data crosses cache lines, the cache lock mechanism cannot ensure data consistency. It downgrades to bus locking to ensure consistency. This situation is called split lock, where "split" can be understood as the cache being split into two lines during memory access.

Bus locking will cause severe performance degradation, increasing memory access latency by about 100 times. If it is a memory\-intensive workload, performance may decrease by two orders of magnitude. Therefore, on X86 processors, code causing split lock should be avoided. [Learn more](https://developer.volcengine.com/articles/7096405105133502471).

<span id="EwASSStG"></span>
## Procedure

<span id="ZsfAZCi8"></span>
### Linux system


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Use the perf tool to capture triggered processes and code segments. For more information about the perf tool, please refer to its [official documentation](https://perfwiki.github.io/main/tutorial/#sample-analysis-with-perf-report).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, only General\-purpose <a href="https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNhbA==">g3al</a> specifications are supported, and the kernel version must be 4.15 or above.   </div>
   

   1. Execute the perf command to capture split lock events. Take capturing for 30 seconds as an example.

      ```Bash
      perf record -e ls_locks.bus_lock -a sleep 30
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can adjust the last argument of the command above to the actual capture duration. For example, change <code>30</code> to <code>20</code>.      </div>
      

   2. Execute the following command to generate a report. If the time consumption ratio of the target event process does not meet your business expectations, perform systematic fixes in your code.

      ```Bash
      perf report -i perf.data
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb2a6bdc6420337cae3c9e86728b02e2.png) </span>

      Description of key fields:

      
      |Field |Description |
      |---|---|
      |Overhead |Event percent (time proportion). |
      |Command |Process name triggering the event. |
      |Symbol |The function or kernel symbol that triggers the event.<br><br><br>* [.] : User level.<br><br>* [k]: Kernel level. |
      

3. Please locate the processes and code segments causing split lock at your code level, then perform systematic repairs (eliminate the occurrence of split lock).

   * **Business code**

      * It is recommended to align the structure without crossing cache line access, using tools such as "compiler memory alignment" or "__cacheline_aligned" for related operations.

         > It is recommended to use the default memory alignment tool provided by the compiler for operations.         
         

      * Align the structure according to the size of the members and the order in which they are declared.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Try not to use atomic instructions for access, as this may cause unaligned memory access.      </div>
      

   * **Open source code**: Submit an issue to the open source community and promote community resolution.

   * **Closed\-source software**: Find a feedback channel and prompt the software provider to resolve it.


<span id="H6bDWWei"></span>
### Windows operating system

It is recommended to promote the corresponding software developers to solve the issue based on the business form.
