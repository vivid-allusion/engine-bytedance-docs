---
title: "Comparing branches"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Comparing_branches"
---

This topic introduces the steps to perform branch comparison.

<span id="qn2V5J41"></span>
## Background

In parallel multi\-branch development scenarios, it is necessary to clarify the database structure (Schema) differences between the source branch and target branch before merging branches. Traditional manual comparison or open\-source tools suffer from low efficiency, inability to directly export migration SQL, and a high risk of misjudging Rename as delete and recreate, leading to data loss.

The "compare branch" function generates safe migration SQL based on schema diff (target branch + migration SQL = source branch). It provides a visual object\-level difference review capability and supports rename changes recognition via OID under restricted scenarios. The entire process is asynchronous and non\-locking, helping users efficiently and safely complete structure alignment without affecting business operations.

<span id="Y5LLDLWz"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The source branch and target branch status are both **Running**.


<span id="sy91XI50"></span>
## Precautions


* Only one branch compare task can exist under each branch at the same time.

* It is recommended that the number of tables in one branch compare task does not exceed 2000.

* Branch compare supports difference comparison for the following objects:

   
   |**Object** |**tip** |
   |---|---|
   |table |Table. Includes table columns, indexes, foreign keys, and triggers |
   |sequence |Sequences |
   |function |Functions |
   |procedure |program |
   |view |views |
   |materialized_view |materialized view |
   |extension |Extensions |
   |enum |Enums |
   |comment |Comment |
   


<span id="GyADPVZK"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** on the right of the branch section to enter the target workspace's **Branch management** page.

4. Click **Compare branch** in the upper\-right corner of the page to enter the **Compare branch** page.

5. On the **Compare branch** page, specify the source branch, source database, source schema, target branch, target database, and target schema in order, then click **Compare**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After completing the comparison, the differences will be displayed one by one by table. You can expand the difference in the difference list to get detailed difference content.</div>


<span id="KwHOqUf6"></span>
## Next steps

<span id="uGwD4JFC"></span>
### Download difference information to local

After completing the comparison, you can click Download all differences at the upper\-right corner of the difference list to download the difference information to your local device. Difference information will be organized according to the following directory structure and compressed in zip format for download.

```Plain Text
<Comparison Task ID>_<Source Schema Name>_<Target Schema Name>-<Comparison Task Completion Time>.zip
└──<Comparison Task ID>_<Source Schema Name>_<Target Schema Name>-<Comparison Task Completion Time>/
    ├── result.sql # Difference result SQL (migration SQL).
    ├── diff.meta # Overall comparison result
    ├── <Source Schema Name>-<Source Object>_<Target Schema Name>-<Target Object>/ # First group of difference directories
    │   ├── target.sql # Complete DDL definition of the source branch object.
    │   ├── source.sql # Complete DDL definition of the target branch object.
    │   ├── result.sql # Difference result SQL (migration SQL).
    │   ├── diff.meta # Complete comparison json.
    └── ……
```


<span id="VYpBeQ7G"></span>
## Related APIs


|**API** |Description |
|---|---|
|[DescribeBranchSchemaNames](https://docs.byteplus.com/docs/aidap/DescribeBranchSchemaNames) |Call the DescribeBranchSchemaNames API to query the list of schemas for the branch. |
|[CreateSchemaDiff](https://docs.byteplus.com/docs/aidap/CreateSchemaDiff) |Call CreateSchemaDiff API to create a branch compare task. |
|[DescribeSchemaDiffJobStatus](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffJobStatus) |Call DescribeSchemaDiffJobStatus to query the status of the branch comparison task. |
|[DescribeSchemaDiffResultMeta](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultMeta) |Call DescribeSchemaDiffResultMeta API to query detailed information of the Compare branch task. |
|[DescribeSchemaDiffResultSQLText](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultSQLText) |Call DescribeSchemaDiffResultSQLText API to query the SQL text of the branch compare result. |
|[DescribeSchemaDiffResultSQLTextAll](https://docs.byteplus.com/docs/aidap/DescribeSchemaDiffResultSQLTextAll) |Call the DescribeSchemaDiffResultSQLTextAll API to query the complete migration SQL text for the branch comparison task. |
|[GetSchemaDiffResultDownloadLink](https://docs.byteplus.com/docs/aidap/GetSchemaDiffResultDownloadLink) |Call GetSchemaDiffResultDownloadLink API to obtain the download link for the branch compare result. |


&nbsp;
