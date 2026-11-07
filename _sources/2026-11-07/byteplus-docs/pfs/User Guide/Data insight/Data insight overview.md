---
title: "Data insight overview"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Data_Insight_Overview"
---

Data insight is a file system data analysis feature provided by PFS file storage. With data insight, you can analyze the data properties and access behavior within the file system in depth, then use these results for refined data management, such as data migration, deleting files, and setting directory quotas, helping achieve efficient storage resource utilization and cost control.

<span id="53de619c"></span>
## Product features


* **File system analysis**

   By customizing data insight policies, you can thoroughly analyze specified directories (execution directories) in the PFS file system and filter out files that meet policy rule criteria. Filtered results can be exported to a specified directory in the same file system, TOS, or browser, or visualized as analysis charts based on TLS log service.

* **Directory capacity query**

   Supports checking the capacity usage of a specified directory in the file system.

* **Visual analysis**

   Based on Log Service TLS, provides visual analysis charts for data insights. You can further explore and visualize data insights using these charts.


<span id="bdb6e2cd"></span>
## Use cases

You can process the file system based on data insights, such as migrating or deleting data Data Insight use cases include, but are not limited to:


* **Storage layout optimization**

   * **Capacity management**

      Query file system usage and storage capacity, predict file system growth trends, plan storage resource allocation more effectively, avoid insufficient or excessive allocation, and determine the right expansion plan.

   * **Hot and cold data filtering**

      Optimize storage layout by identifying hot and cold data in the file system based on data access frequency.

* **Performance analysis**

   Gain insights into performance and identify access bottlenecks in the file system. For example, analyze attributes like file access frequency and access time to find files that cause performance degradation, and take optimization measures accordingly.

* **Storage cost management**

   Gain cost\-related insights to enable observability for the file system with low barriers, while ensuring business agility. Adjust storage strategies based on these insights, such as selecting appropriate file system specifications and optimizing cloud costs.

* **Visualization monitoring**

   Use data insights for visual monitoring of file system status, including storage capacity and usage, to promptly detect and address potential issues.


<span id="6bd250a1"></span>
## Usage


|Limit |Note |
|---|---|
|Number of data insight tasks that can run simultaneously on a single file system |1 |
|Number of execution directories that can be associated with a single data insight task |10 |


<span id="b4e2b1a5"></span>
## Workflow


1. [Creating file systems](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system)

2. [Enable data insight service](https://docs.byteplus.com/en/docs/pfs/Enable_Data_Insight_Service)

3. [Create a data insight policy](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies#e05deaf7)

4. [Create a data insight task](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks#f256f405)

5. [View data insight results](https://docs.byteplus.com/en/docs/pfs/View_data_insight_results)
