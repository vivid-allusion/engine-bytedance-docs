---
title: "Memory optimization"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Memory_optimization"
---

Memory optimization includes OOM trends, leak analysis, large objects, and single device memory details, which can help you optimize memory more effectively.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* Memory optimization has been integrated. For details, refer to [Integrating the Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) and [Integrating the iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* Memory optimization has been configured. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".T09N6LaL5Yq_"></span>
## OOM trends

As part of the OOM trend analysis, metrics for memory leaks are provided. In addition to the core metrics—number of OOM occurrences, OOM rate, number of affected users, and proportion of affected users—extended metrics are also provided for further analysis of OOM, such as the amount of memory used by the app and the proportion of memory used by the app.

<span id="20f9efea"></span>
### Filter dimensions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, device ID, User ID, system version, app version, app minor version number, device model, OOM type, process name, APM SDK version, download channel, PV custom dimension.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">OOM types:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">java: Java exception, java.lang.OutOfMemoryError.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">native: When a Native crash or ANR occurs, it is typically because a 32\-bit application on a 32\-bit device exceeds 2.8 GB of virtual memory, or a 32\-bit application on a 64\-bit device exceeds 3.8 GB of virtual memory.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Launch: Java OOM during the launch phase.   </div>
   

* Filter dimensions supported by iOS:

   Time, device ID, User ID, jailbreak status, system version, app version, app minor version, device model, APM SDK version, download channel, PV custom dimension.


<span id=".5oyH5qCH5aSn55uY"></span>
### Metrics dashboard

The OOM trend chart displays the trend of the OOM metric under the filter conditions. On the right side of the metric data, you can view changes in OOM data compared to the previous period.


* Supports adding filter criteria for custom dimensions, and allows you to select the dimension, the relationship between the dimension and its value, and the value. The relationship between dimensions and values can be configured as '=' or '≠'.

* Click the download button to download a data overview of the `.png` file type.

* Click **View crash details** to navigate to the **Crash trends** page, where you can view specific OOM crash trends, distributions, and crash details.


Indicator description:


|**Metric** |**DescriptionS** |
|---|---|
|OOM count |Number of OOM occurrences with filter applied (PV) |
|OOM rate |Number of OOM occurrences under filter conditions / total number of launches under filter conditions |
|The affected user count |Number of users (UV) affected by OOM issue under filter conditions |
|Proportion of affected users |Number of deduplicated UVs with OOM errors under filter conditions / total number of deduplicated UVs under filter conditions |


<span id="e567d854"></span>
### Extended metrics

In addition to the default metrics provided in the dashboard, OOM also supports extended metrics.

<span id="60acb047"></span>
#### iOS client


|**Reported fields** |**Metric Name** |
|---|---|
|app_memory_rate |App memory usage percentage |
|app_memory |App memory usage size |


<span id="ac67f438"></span>
#### Android client


|**Reported fields** |**Metric Name** |**Obtaining method** |
|---|---|---|
|total_pss_background |Physical memory (background) |Debug.MemoryInfo.getTotalPss() |
|total_pss_foreground |Physical memory (foreground) |Debug.MemoryInfo.getTotalPss() |
|java_heap_background |Java memory usage (background) |Runtime. *getRuntime* ().totalMemory()\-Runtime. *getRuntime* ().freeMemory() |
|java_heap_foreground |Java foreground memory usage |Runtime. *getRuntime* ().totalMemory()\-Runtime. *getRuntime* ().freeMemory() |
|graphics_background |Video memory (background) |Debug.MemoryInfo.getMemoryStat("summary.graphics") |
|graphics_foreground |Foreground video memory |Debug.MemoryInfo.getMemoryStat("summary.graphics") |
|vm_size_background |Virtual memory (background) |/proc/[pid]/status |
|vm_size_foreground |Virtual memory (front end) |/proc/[pid]/status |
|java_heap_background_used_rate |Java memory usage rate (backend) |java_heap_background/Runtime. *getRuntime* ().maxMemory() |
|java_heap_foreground_used_rate |Java memory utilization (foreground) |java_heap_foreground/Runtime. *getRuntime* ().maxMemory() |
|dalvik_pss_background |Java physical memory usage (background) |Debug.MemoryInfo.dalvikPss |
|dalvik_pss_foreground |Java physical memory usage (foreground) |Debug.MemoryInfo.dalvikPss |
|native_pss_background |Native physical memory usage (background) |Debug.MemoryInfo.nativePss |
|native_pss_foreground |Native physical memory usage (foreground) |Debug.MemoryInfo.nativePss |


<span id=".T09N6K-m5oOF"></span>
### OOM details

Click the extended metric name to go to the metric details page.

<span id=".5oyH5qCH6LaL5Yq_5Zu-"></span>
#### Indicator trend charts

<span id=".6Ieq5a6a5LmJ57u05bqm5YiG5p6Q"></span>
#### Custom dimensions analysis

<span id=".5rOE6Zyy5YiG5p6Q"></span>
## Leak analysis

A memory leak occurs when unused objects (objects that are no longer in use) continue to occupy memory or when the memory used by such objects is not released in a timely manner, resulting in wasted memory space. Memory leaks are sometimes minor and difficult to detect, so developers may be unaware of the existence of memory leaks, the excessive accumulation of leaks, or memory exhaustion, which can ultimately lead to out\-of\-memory (OOM) errors.

Leak analysis provides a list of object types that cause leaks and details, allowing you to individually analyze those objects responsible for severe memory leaks.

<span id="9dcb4292"></span>
### Filter dimensions

You can filter data using the following filter criteria:

Time, system, system version, App version, device model, APM SDK version, issue status, assignee, tags, leak details.

<span id=".5rOE5ryP6LaL5Yq_"></span>
### Leak analysis


* By default, the list displays the following: leak description, start and end versions, number of occurrences, number of affected users, average size, total size, handler, and status.

* Click the settings button to configure the columns displayed in the list, including year\-over\-year count, year\-over\-year affected users, year\-over\-year average size, and year\-over\-year total size. Among these, the leak description cannot be hidden.

* Click the download button to download the first 1000 records. You can view the details of the leaked data in .xlsx file format.

* Supports one\-click sorting by count, affected user count, average size, or total size in ascending or descending order.

* Supports directly assigning a handler and modifying the processing status.

* The columns for frequency and number of affected users support viewing the trend chart. A trend chart displays up to the most recent 48 points.


<span id=".5rOE5ryP6K-m5oOF"></span>
### Leak details

Click the leak description in the leak trend list to open the leak details page. You can query leak summaries, detailed information, leak trends, leak distributions, detailed information, reference chains, and symbol tables.

<span id="2173d6ec"></span>
#### Summary

In the summary, you can view the number of leak occurrences, the number of affected users, the proportion of affected users, the most recent report time, the most recent occurrence time, and the first occurrence time. You can also view and set the leak status, assignee, and tags.

<span id="73d61518"></span>
#### Distribution of leaks

The leak distribution supports filtering data by different dimensions. By default, data is filtered by device model, device system version, ROM information, and download channel. You can click **Select dimension** to customize distribution dimensions.

<span id="61040dca"></span>
#### Leak trends

Display data in the leak trend according to the filter conditions. By default, you view the trend of the data by the number of occurrences. You can switch to viewing the trend of the data by the number of affected users.

<span id="bcb6e7eb"></span>
#### Detailed information

You can view detailed information about leaked abnormal data in the details section.


* Click **Show custom dimension parameters** to view only custom parameters.

* Click **download log file** to view a log file in .json format and view detailed information in the log file.

* Click **Single device memory details** to view the specific memory usage of the current DID during OOM, including data on leaks, large objects, and more.

* Click the upper right corner to switch and view detailed information for other leak data.

* Click the **Trace** link next to the device identifier or UserID to go to the **Log Query** page and view the logs for that device identifier or UserID.


<span id="0a0c49f3"></span>
#### Reference chains

The reference chain displays the specific reference relationships between the leaked Activity class and the specific GC Root. The leak issue can be resolved by breaking the reference relationship. All leaks should be optimally resolved.

<span id=".5aSn5a-56LGh5YiG5p6Q"></span>
## Analysis of large objects

A large object refers to either an object with an individual size greater than 1000KB, or a class with more than 50 instances and a total memory size greater than 10000KB. Large objects are major contributors to memory usage and are a key focus of analysis during memory optimization.

The large object list provides both large objects that occupy excessive memory and small objects that are aggregated due to their large quantity, helping you more accurately understand which objects are occupying memory.

<span id=".562b6YCJ5p2h5Lu2"></span>
### Filter dimensions

You can filter data using the following filter criteria:

Time, system version, APP version, device model, large object type, APM SDK version, issue status, assignee, tags, lag details.

<span id=".5aSn5a-56LGh6K-m5oOF5YiX6KGo"></span>
### Large object details list


* By default, the list displays large object details, start and end versions, number of times, number of affected users, average size, total size, person in charge, and status.

* Click the settings button to configure the columns displayed in the list, including YoY count, YoY affected user count, YoY average size, and YoY total size. Among them, hiding object details is not supported.

* Click the download button. You can download the first 10,000 records and view details of large object data in .xlsx file format.

* Support one\-click sorting by number of occurrences, number of affected users, average size, or total size in ascending or descending order.

* Supports directly assigning an assignee and modifying the processing status.

* The columns for number of occurrences and number of affected users support viewing trend charts. The trend chart displays up to the most recent 48 points.


<span id=".5aSn5a-56LGh6K-m5oOF"></span>
### Large object details

Click "Large Object Details" in the Large Object Analysis List to enter the Large Object Details page. In addition to querying large object summaries, detailed information, large object trends, large object distribution, details, reference chains, retained objects, and the symbol table.

<span id=".5pGY6KaB"></span>
#### Summary

In the summary, you can view the number of occurrences of large objects, the number of affected users, the proportion of affected users, the most recent reporting time, the most recent occurrence time, and the first occurrence time. You can also view and set the status, assignee, and tags for large objects.

<span id=".5aSn5a-56LGh5YiG5biD"></span>
#### Large object distribution

In large object distribution, you can filter data by different dimensions. By default, data is filtered by device model, device system version, ROM information, and download channel. You can click **Select Dimension** to customize distribution dimensions.

<span id=".5aSn5a-56LGh6LaL5Yq_"></span>
#### Trends in large objects

Display data based on filter criteria within the large object trends section. By default, view data trends by occurrence count. You can switch to viewing data trends by affected user count.

<span id=".6K-m57uG5L-h5oGv"></span>
#### Detailed information

You can view detailed information about abnormal data of large objects in the detailed information section.


* Click **Show custom dimension parameters** to view only custom parameters.

* Click **Download log file** to view a log file in .json format and view detailed information in it.

* Click **Single device memory details** to view the specific memory usage of the current DID during OOM events, including data on leaks, large objects, and other data.

* Click the upper right corner to switch to view details of other large objects.

* Click **Trace** next to the device identifier or UserID to go to the **Logs Query** page, where you can view the logs for that device identifier or UserID.


<span id="f8ca0e43"></span>
#### Reference chains

The reference chain displays the specific reference relationships from large objects to the specific GC Root. This allows you to determine whether the reference relationships are reasonable and whether they can be disconnected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A file path can have up to 1000 levels.</div>


<span id="e0c8e373"></span>
#### Held objects

A held object displays which specific objects are referenced by large objects, resulting in high memory usage. This allows you to determine whether optimizing the held objects can help reduce memory consumption.

For example, in the diagram, there are too many List cache objects and the cache objects are too large, resulting in high memory usage. Optimization can be achieved by clearing cache objects.

<span id=".5Y2V6K6-5aSH5YaF5a2Y6K-m5oOF"></span>
## Memory details for a single device

In the single device memory details, you can directly analyze memory issues for a single device. iOS provides direct and precise analysis of a single device’s memory reference tree, dominator tree, instances, and other related data, while Android can download and query the raw data for a single device.

<span id="9a0f99a2"></span>
### Filter dimensions

You can filter data using the following filter criteria.


* Filter dimensions supported by the Android system:

   Time, system version, APP version, device model, APP minor version, download channel.

* Filter dimensions supported by iOS:

   Time, issue creation status, foreground/background status, jailbreak status, hidden downgrade cases, system version, APP version, device model, APP minor version number, download channel.


<span id=".QW5kcmlvZOeVjOmdouamguiniA=="></span>
### Android interface overview


* The list displays data such as Device ID, collection time, APP version, APP minor version, operating system version, device model, and more.

* Supports sorting by collection time, app version, app minor version, operating system version, and device model.

* Click the download button to download the first 10,000 records of device memory information in `.xlsx` file format.

* Click **Raw Data Download** in the Actions column. The platform will package the target device's data into a zip file. After extracting the file, you can view the contents of the `.hprof` file.

* Click DeviceID to expand it and view information such as object leaks, individual large objects, and class\-level large objects.

   * In the Object Leak tab, click the object name to enter the leak details page and perform leak analysis.

   * In the single large object tab, click the object name to enter the large object details page to perform large object analysis.

   * On the Class Large Objects tab, click the class name to view the large object details and perform large object analysis.


<span id=".aU9T55WM6Z2i5qaC6KeI"></span>
### iOS interface overview


* The list displays data such as Device ID, collection time, app version, app minor version number, operating system version, device model, and more.

* Supports sorting by collection time, app version, app minor version number, operating system version, and device model.

* Click the download button to download the first 10,000 records and view device memory information in .xlsx file format.

* Click **view details** in the Actions column to enter the memory details page and view detailed information about the device.

   The memory details page is roughly divided into five main areas: (1) cluster list, (2) instances, (3) basic information, (4) reference tree and dominator tree, and (5) backtrace path.


<span id=".6IGa57G75YiX6KGo"></span>
#### Cluster list

The clustering list provides an overview of App memory, with memory nodes aggregated by type. Sorting and other methods can help you quickly determine the general distribution of memory within the App and initially expose potential issues.


* Enter the class name in the search box to search for the specified node. Fuzzy matching is supported.

* To provide finer granularity in the display, the default aggregation is based on **class name + size**. You can click **Aggregate by class name** to aggregate and display by class name only.

* Check **Only look at the leaks** to display only nodes with leaks.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If, after checking this option, no nodes are displayed, it means that there are no leaked node types.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you check the box, the node count and memory usage data in the upper left corner will also change accordingly.   </div>
   

* Click a node information item to display all instances of this type in the Instances list (②) on the right.


Parameter descriptions in the list:


|**Parameters** |**DescriptionS** |
|---|---|
|Class name |Indicates the memory node type name.<br><br><br>* **Aggregate by type name + size**: Display node type name + node size.<br><br>* **Aggregate by class name**: Only class names are displayed.<br><br><br>When you select different aggregation methods, the data in the Count, SHALLOW SIZE, and RETAIN SIZE columns will change. At the same time, the display information for the instance list in Region ② will also change. |
|Quantity |Number of nodes of this type. |
|SHALLOW SIZE |Total memory usage of all instances of nodes of this type. |
|RETAIN SIZE |The total memory usage of all instances of this type of node and of the nodes they dominate (The definition of domination can be found in the appendix.) |


<span id=".5a6e5L6L5YiX6KGo"></span>
#### Instances

Instances displays all nodes in a specific set from the cluster list. You can label a type of node using analytical methods, classify nodes based on their usage, and click a node to view detailed information about a specific instance.


* The top left corner displays the node type of the current instance list, while the top right corner shows the total memory used by all instances in the current instance list (excluding dominator nodes).

* Enter the name of any ancestor (such as a parent, a parent's parent, and so on, up to and including the root node) or a specific pointer in the search box to filter nodes that have the corresponding ancestor. This feature is typically used to confirm how many nodes belong to the same category or a specific object. For example, whether all items are in the cache, whether all belong to a certain VC, and so on.

   Caution: Fuzzy matching is not supported here, and do not include size\-related strings. After entering the text, press Enter or click the search button, and a dialog box will appear. For example, enter __NSCFDictionary here.

   The dialog box displays the current number of instance nodes of the __NSCFString type, that is, all instances of the __NSCFString type whose ancestors are of the __NSCFDictionary type, including both leaked and non\-leaked instances. After you click Confirm, these nodes will be tagged.

   <span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/44eb39c819614a0ca684aaa8f05ee8bd~tplv-em5hxbkur4-noop.image) </span>

   Double\-click a label to delete all labels of this type. For example, double\-clicking "1" in the image above will delete all "1" labels.

* Each line in the instance information displays the address of the instance. Inside the parentheses, the value before the '+' indicates the memory size occupied by the instance itself, while the value after the '+' represents the total memory size of the nodes dominated by the instance.

   Click an instance entry, and its basic information, reference tree, and dominator tree will be displayed below.


<span id=".5Z-65pys5L-h5oGv"></span>
#### Basic information

Basic information displays a node’s basic information, including its size, address, type, whether it is a leak, labels, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/738e2ebaa81f469f9e50747052ba45c5~tplv-goo7wpa0wc-image.image) </span>

Parameter description:


|**Parameters** |**DescriptionS** |
|---|---|
|Class name |The class name of the current node is displayed in the format "class name + size". |
|Node types |Type associated with the node<br><br>`OC/Swift/Virtual C++` objects can obtain meaningful information through symbolication. |
|Ptr |The node address. |
|VMType |Virtual memory type, such as Heap or a specific VM type. |
|VMSize |The measurement criteria for memory size vary for different types of nodes.<br><br><br>* For memory nodes managed by libmalloc, this size is the final size allocated by `malloc`.<br><br>* For the `VM: Stack` type, this size indicates the size requested by the VM.<br><br>* For the static area type, this value is always 0. The memory size used by the static area is not reflected here, but is reflected in the specific `VM Region`.<br><br>* For other VM types, this size is the actual amount of physical memory used. |
|RetainedSize |The sum of the memory sizes of all nodes dominated by the node. |
|Is this an abandoned issue |Is the current node an Abandoned Memory (if you are not familiar with the definition of Abandoned, refer to the appendix)? |
|Leak or not |Is the current node leaking memory? |


Common VM types:


|VM type |DescriptionS |
|---|---|
|`VM: Stack` |Stack memory: Each thread has its own thread stack, as well as TLS and other data, all of which are stored in the VM: Stack. The children of this node represent the temporary variables referenced by the stack, as well as TLS and other data; the entry point for AutoreleasePool is also located here. The type of thread can be determined based on the stack size: the main thread is typically 1008 KB, GCD threads and default threads are 544 KB, and other sizes should be mapped according to business requirements. For example, some threads in TTPlayer have a stack size of 160 KB. |
|`VM: ImageIO` |The data used by ImageIO is typically image data, and this type of data is commonly encountered when using methods such as `imageNamed/imageWithData`. |
|`VM: CG Raster Data` |The raster data used by CoreGraphics is typically a picture. For example, commonly used frameworks such as SDWebImage and other similar frameworks use CoreGraphics to render pictures. In apps that make heavy use of network pictures, this type of VM is typically the main consumer of memory. |
|`WebKit Malloc` |WebKit's heap memory: WebKit manages memory using its own bmalloc instead of libmalloc. Cross\-platform solutions (mini games, mini programs, RN, Weex) and H5 make extensive use of this type of memory. |
|`VM: IOSurface` |Key structures for sharing data across processes, CPUs, and GPUs include textures, framebuffers, and pictures. These are commonly found in effects rendering and video recording. |
|`VM: IOKit` |Memory allocation related to iOS drivers is commonly found in scenarios such as texture storage, including certain texture allocations in Metal. Similar to IOSurface, it frequently appears during special effects rendering and video recording. |
|`VM: LayerKit` |CoreAnimation memory usage is commonly associated with the Layer's BackingStore. If there are too many layers, this type of memory usage can become excessive. |
|`VM: SQLite Page Cache` |The page cache allocated by SQLite. |
|`VM: Type 0` |There are multiple possibilities. Memory directly allocated using VM Alloc is of this type, and memory in the Data segment also belongs to this type. |


<span id=".5byV55So5qCR5ZKM5pSv6YWN5qCR"></span>
#### Reference trees and dominator trees

The left image in the figure is the reference graph, and the right image is its corresponding dominator tree.

If every path from the root node M to node B must pass through node A, then node A dominates node B. The closest dominator of node B is its parent in the dominator tree.

In a dominator tree, if the parent node is released, all of its child nodes are released.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd4e148ff4e94b1b8bb34e9f0160224b~tplv-goo7wpa0wc-image.image) </span>

The reference tree displays the reference relationships associated with the current node. The parent node is the parent of the current node in the reference tree, and the child node is the child of the current node in the reference tree.

The dominator tree displays the dominance relationships related to the current node. The parent node is the current node's parent in the dominator tree, and the child nodes are the current node's children in the dominator tree.

By using the reference tree and dominator tree, you can quickly identify which business object ultimately references a node, making it easier to locate problems.


* Collapse Heap parent nodes: Heap parent nodes without symbols in the compressed reference tree. After you check this option, the system will automatically backtrack and search each path from the current node to the root node for the first node with semantic significance. The Heap nodes in these paths will then be hidden, and the nodes with semantic significance will be displayed in the parent node list. This helps you quickly locate meaningful business objects.

* Aggregate display: Group nodes of the same type (class and size) together for display, and show the number of such nodes in parentheses.

* Note: Each node in the reference tree has a button that indicates the reference relationship. Different reference types are distinguished by color. The button displays either the variable name or the offset. 'assign' indicates an offset of 0, and 'Indirect' indicates an indirect reference relationship. Click the button to switch nodes. At the same time, ③ Basic Information and ④ Reference Tree and Dominator Tree will update to display the information corresponding to the selected node.

   Relationship descriptions:

   
   |**Parameters** |**DescriptionS** |
   |---|---|
   |Indirect Relation |Not a direct reference. When you check **Collapse Heap parent node**, this type of node will appear. |
   |Weak Ref |Weak reference. |
   |Strong Ref |Strong reference. |
   |Unknown/Assign |Unknown reference or assign. |
   

* Cycle: During backtracking by clicking on parent nodes in the reference tree, some nodes may display a strikethrough, indicating that this node was previously part of a cycle during the backtracking process. In section ⑤ Backtracking path, you can view which nodes appeared in the path of the generated cycle.

* Node information: Each node in the reference tree and dominator tree consists of the following: class name + size + (address) + (dominated size, excluding its own memory) + reference relationship button.


<span id=".5Zue5rqv6Lev5b6E"></span>
#### Backtracking path

The backtracking path records the path taken when tracing from a node to its ancestors, which can help you understand how an object is referenced by business objects.


* Base node information: gray font; base node of the current backtracking path, that is, the first node at the start of the path.

* Click the blue text below the base node information to roll back to the previous node of the current node on the traceback path.

* Set as root node: After you click, the current node is set as the root node of the backtracking path.

* Path search: After you click, the following dialog box appears. The text box displays the backtracking path, and gray text indicates how many nodes in the current instance list have this backtracking path. Click confirm, and the nodes in the Instances list that have this backtrace path will be tagged.

* Path list: Displays information about each node in the current backtracking path, as well as the reference relationships between nodes.


<span id=".5pyA5L2z5a6e6Le1"></span>
## best practices

<span id=".aU9T5Y2V6K6-5aSH5YaF5a2Y5YiG5p6Q5pyA5L2z5a6e6Le1"></span>
### Best practices for memory analysis on a single iOS device

<span id="db85046a"></span>
#### Related terms


|Terms |DescriptionS |
|---|---|
|Abandoned and leaks |Apple's official documentation introduces the memory categories of iOS apps:<br><br><br>* Leaked memory：Memory unreferenced by your application that cannot be used again or freed (also detectable by using the Leaks instrument).<br><br>* Abandoned memory：Memory still referenced by your application that has no useful purpose.<br><br>* Cached memory：Memory still referenced by your application that might be used again for better performance.<br><br><br>APMPlus MemoryGraph uses a leak detection method similar to garbage collection. If node A cannot be reached from the root node, node A is considered leaked. If a group of nodes forms an independent subgraph that is not connected to the main graph, this group is classified as Abandoned. The determination of leaks does not consider strong or weak reference relationships, but only considers reachability. |
|Data definition |MemoryGraph records all of an app's memory states and relationships:<br><br><br>* Libmalloc Heap: Heap memory allocated by libmalloc. Business and logic objects (such as `OC/C++/Swift/C` structures and similar types) are mainly allocated in this region.<br><br>* Virtual memory: all VMs except the Libmalloc Heap, including images, textures, thread stacks, Data segments, heap memory not allocated by Libmalloc, and many others.<br><br>* Reference relationships: reference symbols (`OC/Swift` objects support member variable names, while offsets are displayed for others); `OC/Swift` additionally records strong and weak reference types (for performance reasons, strong and weak reference types captured by `block` are not supported at this time).<br><br>* For memory in the Libmalloc Heap, each memory block managed by Libmalloc is treated as an individual node. For VM, each `VM Region` is treated as an individual node. |


<span id=".5LiA6Iis5L2_55So6Lev5b6E"></span>
#### Commonly used paths

The method of using MemoryGraph is not fixed. The following process is simply a common approach for typical scenarios. You can apply it flexibly according to your own understanding, making MemoryGraph a powerful tool for solving memory issues.


1. Identify prominent and problematic memory sets in the clustering list. Instances of the same size within a category typically have similar purposes, so prioritize those sets that use the most memory.

   In abnormal scenarios with a particularly large number of nodes, analysis may sometimes begin with collections that have large occupancy numbers.

2. Select a node from the set, view its parent in the reference tree, and continue tracing back until you find a business\-related object.

3. If the final business object does not have obvious direct strong references or container references, consider whether there are circular references, check for block references, and use code to analyze each one individually.

4. Randomly select other nodes in the set, check if there are similar paths, and confirm the problem.

5. If any objects are found to be abnormal during the entire process, analyze and handle them flexibly.


<span id=".5p-l5om-5omA5pyJ55qEVmlld0NvbnRyb2xsZXI="></span>
#### Find all ViewControllers


1. Find a ViewController instance and view the reference tree.

2. In the reference tree, find a parent node as shown in the following figure.

3. View the parent node of this HashTable. If the parent node is UIKitCore, then this container includes all ViewControllers.

4. Select the subnodes in the diagram above to view all ViewControllers.
