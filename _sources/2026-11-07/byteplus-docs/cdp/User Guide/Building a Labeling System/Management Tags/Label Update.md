---
title: "Label Update"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_Update"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

Supports timed or manual updates to labels. Labels updated on a daily basis are dependent on upstream readiness before triggering downstream updates.


* **Timed update labels:**  Do not establish dependencies on manually updated upstream labels but still rely on the data source.

* **Manual update labels:**  Are entirely independent and won't automatically recalculate with upstream file updates. Users need to trigger updates manually if required.

> Notes\*:

> Data Update Cycle: Upstream attribute tables and downstream labels are updated on the 1st, 4th, and 5th of each month.

> For historical labels created, dependency updates are triggered only when editing label metadata.


<span id="_2-操作步骤"></span>
# 2. Operation Steps

Click **Labeling System \- New Label**, select the target label.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aad91b8dec80aba1b50a95826a3665c7.png) </span>

When entering the label creation interface, select the update type according to business requirements.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2933896900cbe24e4f53846a82f0f505.png) </span>
