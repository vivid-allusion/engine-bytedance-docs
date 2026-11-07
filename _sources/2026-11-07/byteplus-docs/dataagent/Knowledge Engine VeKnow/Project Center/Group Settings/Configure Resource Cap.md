---
title: "Configure Resource Cap"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Configure_Resource_Cap"
---

Enterprise super administrators can manage the number of knowledge bases in a project, the number of knowledge bases within a single knowledge base, and the number of knowledge graphs in the enterprise knowledge engine's group settings.

# Usage restrictions

Only enterprise superadministrators have permission to configure resource caps.

# Operation steps

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Group Settings** \> **Resource Cap Configuration**.

4. On the **resource cap configuration** page, view the resource cap for each project.

5. Click **Edit** in the **Action** column to support the following configuration actions.

   * **knowledge base configuration**

      You can choose to configure **by quantity** or **by storage space**.

      |**Configuration method** |**Description** |
      |---|---|
      |By quantity |* Number of knowledge bases: Sets the maximum number of knowledge bases allowed to be created in the project; 0 means unlimited; values range from 0 to 100,000.<br><br>* Number of knowledge in a single knowledge base: Set the maximum number of knowledge items allowed to be stored in each knowledge base; 0 means unlimited; the value range is 0~ 100,000.<br><br>* Capacity early warning threshold: In the current mode, when the utilization rate reaches this ratio, the early warning will be displayed, which will not affect the new entry judgment; the value range is 1~ 100%. |
      |By storage space |* Total capacity of the project knowledge base: Set the upper limit of the original file capacity of all valid general knowledge bases in the project; 0 means unlimited; the value range is 0~ 100,000 GB<br><br>* Single knowledge base capacity: Set the upper limit of the original file capacity of a single valid general knowledge base; 0 means unlimited; the value range is 0~ 100,000 GB<br><br>* Capacity early warning threshold: In the current mode, when the utilization rate reaches this ratio, the early warning will be displayed, which will not affect the new entry judgment; the value range is 1~ 100% |

   * **Knowledge Graph Configuration**

      Number of Knowledge Graphs: Set the maximum number of Knowledge Graphs allowed to be created in the project; values range from 1 to 100,000
