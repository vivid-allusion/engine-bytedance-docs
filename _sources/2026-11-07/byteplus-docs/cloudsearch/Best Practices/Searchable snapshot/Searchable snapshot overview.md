---
title: "Searchable snapshot overview"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Searchable_snapshot_overview"
---

Cloud Search supports snapshots that can be searched, based on snapshots to build searchable snapshot indexes. After generating a searchable snapshot index, you can delete the original index while the searchable snapshot index still provides retrieval capabilities. When retrieving a searchable snapshot index, the index reads data from the snapshot repository in real time instead of downloading all index data to instance storage during recovery, which helps reduce instance storage costs.

<span id="901f964e"></span>
## Precautions


* To use snapshots that can be searched, you need to enable cold data nodes in the instance in advance. Instances with Elasticsearch versions 6.7.1 and 6.8.23 do not support cold data nodes and therefore do not support snapshots that can be searched. Instances with Elasticsearch 7.10.2 and later versions and OpenSearch 2.9.0 and later versions support snapshots that can be searched.

* A searchable snapshot index is essentially a read\-only index where index data is stored in snapshot format in a remote repository.


<span id="4a86c3cf"></span>
## Methods to create searchable snapshots


* [Manually create searchable snapshots](https://docs.byteplus.com/docs/cloudsearch/Manually_create_searchable_snapshots): You need to manually create snapshots, then select the indexes within the snapshots and restore these indexes as searchable snapshots. This method does not automatically delete old indexes; manual deletion is required.

* [Create searchable snapshots using ISM](https://docs.byteplus.com/docs/cloudsearch/Create_searchable_snapshots_through_ISM): You can configure an Index State Management (ISM) policy to automatically create searchable snapshots in a specific index state (for example, the Cold state). When a new index matches the index name pattern in the ISM policy, the system triggers the ISM policy. When the index enters the Cold phase, it automatically creates searchable snapshots.

   When creating searchable snapshots via ISM, the system automatically generates a new index, deletes the original index, and creates a read\-only searchable snapshot index. Assuming the original index is `nginxlogs-000001`, the newly generated index is `nginxlogs-000002`, and the generated searchable snapshot read\-only index is `remote-nginxlogs-000001`.
