---
title: "Common concepts"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Common_concepts"
---

AI Native BaaS for Supabase relies on the AI Native Database Platform (AIDAP) and provides services through two database engines: Supabase and PostgreSQL This topic summarizes the common concepts of the AI Native Database Platform.

|**Terminology** |**Concept** |
|---|---|
|Region |The geographic location of the data. |
|Workspace |A workspace is a logical unit and the basic operational unit for using the AI Native Database Platform. After creating a workspace, you can create resources such as branches, databases, and accounts within it. |
|Branch |Multiple isolated resource groups within a workspace, where each group is referred to as a branch. These resources include databases, computing capabilities, and other configurations. You can create a new branch based on an existing one. When creating a new branch, it inherits all changes and data from the parent branch up to a specific point in time. After creation, any operations on the new branch \- such as inserts, updates, and deletions \- only affect that branch and do not impact the parent branch. All branches are isolated from each other. |
|Storage space |Storage space refers to the space occupied by data files, index files, log files (including online logs and archive logs), and temporary files. It is measured in GB·hours, with data collected every 30 minutes. The usage is calculated by multiplying the collected data by the unit price, and the result is rounded to six decimal places. |
|Compute |The resources required to run a workspace branch, measured in Compute Units (CU). Currently, 1 CU represents the standard service capacity of 1 core CPU and 4 GB of memory. |
|Compute usage |Total compute actually used, measured in CU·hours. Running 1 CU for 1 hour equals 1 CU\-hour. Data is collected every second, and the usage is calculated by multiplying the collected data by the unit price, with the result rounded to six decimal places. |
|Branch compute |Total compute allocated to and actually used by a branch. Each branch has an independent compute unit. Its branch compute reflects the branch's workload and resource consumption. |
