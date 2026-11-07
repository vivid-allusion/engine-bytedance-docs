---
title: "Download QA Label CSV"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/download-qa-label-csv"
---

Call this interface to export all labels and their values under the current tenant, one label per line. The tag column gives the same string as the QA Excel import tag field (such as'City: Shanghai, Beijing '), and label_type columns are marked with single/multiple selections. Returns the UTF\-8 (BOM) encoded CSV. Requires that the current user has read access to the knowledge base module (consistent with kb/list).

# Interface description

* Interface name: download_labels_csv_permission_labels_csv_get

* Interface address:/permission/labels_csv

* Request method: GET
