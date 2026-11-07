---
title: "DataFlow overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DataFlow_overview"
---

In AI training and inference scenarios, you can accelerate data access in TOS through FileNAS and reduce costs by exporting cold data from FileNAS to TOS.

<span id="af46465d"></span>
## Challenges


* Diversified performance requirements:

   * AI training datasets require high\-throughput read bandwidth. However, once the raw data has been processed, it will not be accessed again for a while, so the performance demands are minimal.

   * Writing and loading checkpoints need sudden bursts of high bandwidth, whereas older checkpoints only require basic storage reliability.

* Rising cold data costs:

   * The rapid growth of computing clusters and the increased need for efficient training are driving up the demand for high\-performance file storage capacity and costs.

   * Some data is stored in both file storage and object storage, further increasing cost pressure.

* Data lifecycle management challenges:

   * Data access frequency and the characteristics of hot and cold data change over time.

   * Scheduling hot and cold data requires significant manual efforts and resources.


<span id="89f95bb1"></span>
## Data mobility 

DataFlow is a FileNAS feature that greatly simplifies data lifecycle management, reducing costs and improving efficiency.

You can configure the DataFlow feature using DataFlow policies and DataFlow tasks:


|**Configuration method** |**Description** |
|---|---|
|DataFlow policies |* Default configuration (**On\-demand**)<br><br>   After a policy is created, the system loads metadata of all files within the TOS bucket or bucket prefix associated with the policy into FileNAS at once.<br><br>   When a user or application accesses files through FileNAS:<br><br>   * If data already exists in FileNAS, the system directly returns the data.<br><br>   * If data is absent in FileNAS, the system automatically loads the data from TOS to FileNAS. You can access the data in real time without waiting for the load to complete.<br><br>* Bidirectional data flow: A bidirectional data flow between FileNAS and TOS, based on configured rules.<br><br>* DataFlow rules: Include import, export, and eviction rules. An import rule can load either metadata or both metadata and data simultaneously.<br><br>* File conflict policies: Include skipping duplicate files and keeping the newest file. |
|DataFlow tasks |* Unidirectional DataFlow: A one\-time flow of data in one direction between FileNAS and TOS, based on selected task type and rules.<br><br>* DataFlow tasks: Include import, export, eviction, and delete tasks. An import task loads both metadata and data simultaneously.<br><br>* File conflict policies: Include skipping duplicate files, keeping the newest file, and overwriting existing files. |


<span id="98c9b05e"></span>
## Usage limits 

For DataFlow usage limits, see [Limits - Cache FileNAS](https://docs.byteplus.com/en/docs/nas/Limits#iSpfzCWc).

<span id="59266bc8"></span>
## Related documentation


* [Managing DataFlow policies](https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_policies)

* [Managing DataFlow tasks](https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_tasks)
