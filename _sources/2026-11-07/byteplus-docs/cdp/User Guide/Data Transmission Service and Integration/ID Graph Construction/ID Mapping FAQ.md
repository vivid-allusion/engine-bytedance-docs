---
title: "ID Mapping FAQ"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/ID_Mapping_FAQ"
---

<span id="a4d905bf"></span>
# FAQ


|**Q\-Graph Calculation: Does VeCDP's IDMapping use graph calculation? If not, explain the reasons** |
|---|
|* Graph calculation itself is a very general concept, which can be answered from several perspectives:<br><br>   * It calculates based on a model using graphs, where the graph's construction originates from the configuration on the interface (ID type representing points\relations between IDs representing edges). The specific calculation process can be understood as finding relationships on the graph. If a relationship is found, it is reused, if not, a new OneID is generated. Refer to Chapter 3 for more details.<br><br>   * However, traditional graph algorithms are not directly used. For instance, calculating OneID based on connected graphs. This decision considers various aspects like computational performance and satisfaction of requirements.<br><br>   * Since traditional graph algorithms are not used, data is not stored in graph storage; instead, it is stored directly in associative tables.<br><br>* In summary: IDM utilizes a graph model, but how calculations are performed based on the graph is a proprietary algorithm developed by us, ensuring efficient outputs, aligning with business facts, and enabling traceability of the generation process. |
|**Q\-Fuzzy Recognition: Does VeCDP's IDMapping support the integration of unstructured fuzzy recognition? For example, information such as avatars, aliases, contracts, etc.**  |
|* Not supported. If there is relevant information, non\-structured data can be converted into structured data, such as avatar ID, avatar gender characteristics, etc. |
|**Q\-Data Timeliness: What is the timeliness of OneID generation by IDMapping?**  |
|* IDM supports two types of timeliness: offline daily updates and real\-time updates. Offline updates rely on the upstream dataset for daily morning execution. Real\-time updates can achieve sub\-second level updates to generate OneID.<br><br>* IDM supports the logic of integrating offline and real\-time for OneID generation. During offline updates, the real\-time data on the same day before the offline task will be included in the statistics, and real\-time updates will also refer to the OneID generated offline. |
|**Q\-Task Execution: When does the IDMapping task execute daily?**  |
|* IDMapping has a strong dependency on the upstream dataset. After the dataset task update is complete, IDM tasks will automatically update and execute. |
|**Q\-Task Execution: Can the tasks of each entity in IDMapping be set with a priority order? Priority can guarantee that a specific entity task is produced first.**  |
|* Not supported temporarily. The function is under planning. |
|**Q\-After the re\-execution of the task, ID Mapping can find ID=1 in the base table, but the tag cannot be found?**  |
|Consider two aspects:<br><br><br>* If ID=1 was generated for the first time that day, the OneID corresponding to the ID will automatically update and change every time the task is re\-executed.<br><br>* If ID=1 was generated before that day, and the task rerun did not update the tag task, you can click to re\-execute the complete tag for ID to ensure data consistency. |
|**Q\-Data Isolation: What is the granularity of the effective IDMapping? Does it support project isolation and application isolation?**  |
|* IDMapping generates OneID around the subject. The subject is at the group level, so all projects within the group can see the same subject and use the same subject data.<br><br>* IDMapping does not currently support project isolation or application isolation. Isolation fundamentally contradicts the logic of integrating multiple source data, so isolation is not recommended. If isolation is necessary, you can refer to the following solutions:<br><br>   * Use multiple subjects for data isolation. Each target object that needs absolute isolation can be treated as an independent subject.<br><br>   * Adopt full isolation by multiple groups. Multiple groups can completely isolate data and management, equivalent to purchasing multiple sets of VeCDP products. |
|**Q\-Business System Integration: Can downstream business systems also support full system\-wide IDMapping reuse?**  |
|* Supports the option to flow back the tag table or IDM table to the downstream data warehouse or business system for direct querying. |
