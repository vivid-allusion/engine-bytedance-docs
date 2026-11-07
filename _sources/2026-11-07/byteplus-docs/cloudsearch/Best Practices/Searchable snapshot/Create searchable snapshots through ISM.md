---
title: "Create searchable snapshots through ISM"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_searchable_snapshots_through_ISM"
---

Cloud Search supports the searchable snapshot feature, which builds a read\-only searchable snapshot index based on snapshots. This article introduces the procedure for generating searchable snapshots through ISM.

<span id="7e1a1ceb"></span>
## Background

ISM (Index State Management) is an automation plugin for index lifecycle management. It allows automatic execution of various actions based on predefined policies to optimize index performance, storage efficiency, and data management.

In searchable snapshot scenarios, it helps convert infrequently used indexes into searchable snapshots automatically, optimizing cluster storage efficiency and avoiding frequent manual snapshot creation.

<span id="6927298d"></span>
## Prerequisites


* Before experiencing searchable snapshots, ensure cold data nodes are enabled in the instance. Elasticsearch versions 6.7.1 and 6.8.23 do not support cold data nodes and thus do not support searchable snapshots. Instances with Elasticsearch 7.10.2 and OpenSearch 2.9.0 versions support searchable snapshots.

* You can create a new instance and enable cold data nodes during creation. For detailed steps, see [Create instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2).

* If you have an existing instance without cold data nodes enabled, you can enable them by upgrading the instance. For detailed steps, see [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading).

* ISM policies only automatically associate with indexes that are not yet created. When a new index matches the index name pattern in the ISM policy, the index and ISM policy will automatically associate.


<span id="ac6bdb10"></span>
## Create searchable snapshots


1. log in to the visualization tool and go to the command line.

   1. Log in to the visualization tool. Use the public access address to log in to the visualization tool. See [public access to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. Select **Management \> Dev Tools** from the left navigation bar.

2. Create a snapshot repository.

   Create a snapshot repository named `doc-repo`. You can customize the repository name in actual use.

   ```HTTP
   PUT _snapshot/doc-repo
   {
     "type" : "s3",
     "settings" : {
       "bucket" : "es-shadow-prod-cn-beijing-210094***",
       "path_style_access" : "false",
       "endpoint" : "tos-s3-cn-beijing.ivolces.com/",
       "protocol" : "https",
       "client" : "default",
       "base_path" : "_remote_index",
       "region" : "cn-beijing",
       "searchable" : true
     }
   }
   ```
   

   * `bucket`: use the system default bucket directly. The system default bucket is not visible on your TOS product page. You can view its name by moving the mouse over **bucket name** on the **snapshot management** page of Cloud Search.

   * `endpoint`: the S3 Endpoint address of the TOS bucket. Use the private network address directly; the region is the same as the Cloud Search instance.

   * `base_path`: user\-defined snapshot storage path.

   * `region`: the region of the TOS bucket, which matches the region of the Cloud Search instance.

   * `searchable`: when creating a snapshot repository using the system\-built TOS bucket, **this parameter must be set to true**. When using other TOS buckets, this parameter does not need to be configured.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7627598c54bf42bba188ba891ecf703d~tplv-goo7wpa0wc-image.image) </span>

3. Create an ISM policy.

   Here, create an ISM policy with the id `searchable_snapshot_policy`. This policy divides indexes matching the format `nginxlogs-*` into three phases: Hot, Cold, and Delete.

   * The initial status of the index is Hot. When the number of documents exceeds 20, a rollover occurs automatically, generating a new index and moving the original to the Cold phase.

   * Indexes in the Cold phase automatically create searchable snapshots. Indexes enter the Delete phase automatically 5 days after creation. In the Cold phase, the original index is deleted and a read\-only searchable snapshot index is created.

      Assuming the original index is `nginxlogs-000001`, the newly created index is `nginxlogs-000002`, and the created searchable snapshot read\-only index is `remote-nginxlogs-000001`.

   * After entering the delete phase, the searchable snapshot read\-only index and the created snapshot data will be deleted.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note that commands for creating ISM policies differ between OpenSearch 2.9.0 and Elasticsearch 7.10.2 instances.   </div>
   

   
   <Tabs>
   <Tab zoneid="UywPWrhyVS" title="OpenSearch 2.9.0 version instance">
   <TabTitle>OpenSearch 2.9.0 version instance</TabTitle>
   
   ```HTTP
     
      PUT _plugins/_ism/policies/searchable_snapshot_policy
      {
        "policy": {
          "description": "policy-test",
          "default_state": "hot",
          "states": [
            {
              "name": "hot",
              "actions": [
                {
                  "rollover": {
                    "min_doc_count": 20
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "cold"
                }
              ]
            },
            {
              "name": "cold",
              "actions": [
                {
                  "searchable_snapshot": {
                      "snapshot_repository": "doc-repo"
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "delete",
                  "conditions": {
                    "min_index_age": "5d"
                  }
                }
              ]
            },
            {
              "name": "delete",
              "actions": [
                {
                  "delete": {
                      "delete_searchable_snapshot" : true
                  }
                }
              ]
            }
          ],
          "ism_template": {
            "index_patterns": [
              "nginxlogs-*"
            ],
            "priority": 10
          }
        }
      }
   ```
   
   
   
   </Tab>
   <Tab zoneid="tFOVQLuDgQ" title="Elasticsearch 7.10.2 version instance">
   <TabTitle>Elasticsearch 7.10.2 version instance</TabTitle>
   
   <span id="UegsarQd"></span>
   ### ```HTTP
      PUT _opendistro/_ism/policies/searchable_snapshot_policy
      {
        "policy": {
          "description": "policy-test",
          "default_state": "hot",
          "states": [
            {
              "name": "hot",
              "actions": [
                {
                  "rollover": {
                    "min_doc_count": 20
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "cold"
                }
              ]
            },
            {
              "name": "cold",
              "actions": [
                {
                  "searchable_snapshot": {
                      "snapshot_repository": "doc-repo"
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "delete",
                  "conditions": {
                    "min_index_age": "5d"
                  }
                }
              ]
            },
            {
              "name": "delete",
              "actions": [
                {
                  "delete": {
                      "delete_searchable_snapshot" : true
                  }
                }
              ]
            }
          ],
          "ism_template": {
            "index_patterns": [
              "nginxlogs-*"
            ],
            "priority": 10
          }
        }
      }
      PUT _opendistro/_ism/policies/searchable_snapshot_policy
      {
        "policy": {
          "description": "policy-test",
          "default_state": "hot",
          "states": [
            {
              "name": "hot",
              "actions": [
                {
                  "rollover": {
                    "min_doc_count": 20
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "cold"
                }
              ]
            },
            {
              "name": "cold",
              "actions": [
                {
                  "searchable_snapshot": {
                      "snapshot_repository": "doc-repo"
                  }
                }
              ],
              "transitions": [
                {
                  "state_name": "delete",
                  "conditions": {
                    "min_index_age": "5d"
                  }
                }
              ]
            },
            {
              "name": "delete",
              "actions": [
                {
                  "delete": {
                      "delete_searchable_snapshot" : true
                  }
                }
              ]
            }
          ],
          "ism_template": {
            "index_patterns": [
              "nginxlogs-*"
            ],
            "priority": 10
          }
        }
      }
   ```
   
   
   
   |**phase** |**actions** |**Description** |
   |---|---|---|
   |Hot |rollover |Condition: `"min_doc_count": 20`<br><br>Meaning: When the number of documents in the index exceeds 20, the rollover action triggers, creating a new index and entering the Cold phase. The new index can continue writing data, and when conditions are met, searchable snapshots will continue to be created.<br><br>You can also select other conditions; here are two configurations introduced:<br><br><br>* min_size: When the total storage value of all shards in the index exceeds this value, the action triggers.<br><br>* min_index_age: When the time interval since the index creation exceeds this value, the action triggers. |
   |Cold |searchable_snapshot |Configure searchable snapshot and support the following parameters:<br><br><br>* snapshot_repository: specify the created snapshot repository. string type, required.<br><br>* force_merge_max_segments_num: force merge the segment number of each shard in the index; default is no merge. force_merge indicates that the index will be set to `read-only` status before merging. integer type, optional. |
   ||transitions |Condition: `"min_index_age": "5d"`<br><br>Meaning: The index automatically enters the delete phase 5 days after creation. |
   |Delete |delete |delete_searchable_snapshot: whether to delete the created snapshot data, default is false, which means not deleting the snapshot. Boolean type, optional.<br><br>This parameter is only effective when the `searchable_snapshot` configuration item is included.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Entering the delete phase, the system automatically deletes searchable snapshot indexes. Whether to delete snapshot data depends on the <code>delete_searchable_snapshot</code> parameter configuration; setting it to <code>true</code> deletes the snapshot data along with it.</div><br> |
   
   
   
   </Tab>
   </Tabs>
   

4. Create an index and write multiple data entries.

   1. Create an index template.

      Create an index template named `nginxlogs_template`. You can customize the index template name in actual use.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following command creates an index template and adds a common index alias to all indexes matching the expression. Note that commands for associating aliases differ between OpenSearch 2.9.0 and Elasticsearch 7.10.2 instances.   </div>
   

   
   <Tabs>
   <Tab zoneid="M5Y7ExIQhS" title="OpenSearch 2.9.0 version instance">
   <TabTitle>OpenSearch 2.9.0 version instance</TabTitle>
   
   ```HTTP
   PUT _template/nginxlogs_template
   {
     "index_patterns": ["nginxlogs-*"],
     "settings": {
       "index": {
         "number_of_shards": 1,
         "number_of_replicas": 1,
         "plugins.index_state_management.rollover_alias": "nginxlogs"
       }
     }
   }
   ```
   
   
   
   </Tab>
   <Tab zoneid="BmyhyQLicm" title="Elasticsearch 7.10.2 version instance">
   <TabTitle>Elasticsearch 7.10.2 version instance</TabTitle>
   
   ```HTTP
   PUT _template/nginxlogs_template
   {
     "index_patterns": ["nginxlogs-*"],
     "settings": {
       "index": {
         "number_of_shards": 1,
         "number_of_replicas": 1,
         "opendistro.index_state_management.rollover_alias": "nginxlogs"
       }
     }
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   

   2. Create index.

      ```HTTP
      PUT /nginxlogs-000001
      {
        "aliases": {
          "nginxlogs": {
            "is_write_index": true
          }
        }
      }
      PUT /nginxlogs-000001
      {
        "aliases": {
          "nginxlogs": {
            "is_write_index": true
          }
        }
      }
      ```
      

   3. Repeatedly write multiple document data.

      Repeatedly execute the following commands to write multiple document data to the index. To trigger the ISM policy rollover action set in this article, you need to write more than 20 documents.

      ```HTTP
      POST /nginxlogs/_doc
      {
        "@timestamp": "2024-07-01T13:12:00",
        "message": "GET /search HTTP/1.1 200 1070000",
        "user": {
          "id": "kim"
        }
      }
      ```
      

5. Check the index data distribution to determine whether to generate a searchable snapshot index.

   ```HTTP
   GET _cat/shards?v&s=index,shard
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c5325f0a9a04809bd33e52562bb400f~tplv-goo7wpa0wc-image.image) </span>

   The newly created index name will automatically associate after matching the index expression in the ISM policy. After a period of time, you can run the above command to check whether a searchable snapshot index has been generated, which defaults to starting with `remote-`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">From the query results, you can learn the following important information:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A searchable snapshot index starts with <code>remote-</code> and is stored on <strong>cold data nodes</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system automatically generates a new index <code>nginxlogs-000002</code>, and after some time, the original index <code>nginxlogs-000001</code> will be deleted.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there is no searchable snapshot index starting with <code>remote-</code> in the index list, it usually means the ISM policy is still executing and the searchable snapshot index has not yet been generated. ISM policy execution generally takes a long time. You can check the policy execution progress with a command. For details, see <a href="https://docs.byteplus.com/docs/cloudsearch/Create_searchable_snapshots_through_ISM#c0752eea">1. How to check ISM policy execution progress?</a>   </div>
   

6. Search searchable snapshot indexes.

   ```HTTP
   GET /<index-name>/_search
   ```
   

   When searching searchable snapshot indexes, replace with the correct index name. In this article, you can query `remote-nginxlogs-000001` or `remote-nginxlogs*`.


<span id="2ca0c0df"></span>
## FAQs


* ### How to check the execution progress of an index’s ISM policy? <span id="c0752eea"></span>

   On the **Dev Tools** page, run the command `GET _opendistro/_ism/explain/<index-name>` to check the ISM policy execution progress.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/233d05231277402bbb675f4baba78c5f~tplv-goo7wpa0wc-image.image) </span>

* ### How to determine if an index is a searchable snapshot index? <span id="72aa3f82"></span>

   On the **Dev Tools** page, run `GET /<index-name>/_settings?pretty` to check the index configuration. If the index's storage type shows **remote_snapshot**, it means the index is a searchable snapshot index.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ec627dc6853448d8666479321355f75~tplv-goo7wpa0wc-image.image) </span>

* ### How to associate existing indices with ISM policies? <span id="31a16df5"></span>

   On the **Dev Tools** page, execute the following command to associate historical indices with the target ISM policy.

   * OpenSearch version instance:

   ```HTTP
   POST /_plugins/_ism/add/<index-name>
   {
     "policy_id": "searchable_snapshot_policy"
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/759d7b705e894fc0ae8860e212891769~tplv-goo7wpa0wc-image.image) </span>

   * Elasticsearch 7.10.2 version instance:

   ```HTTP
   POST /_opendistro/_ism/add/<index-name>
   {
     "policy_id": "searchable_snapshot_policy"
   }
   POST /_opendistro/_ism/add/<index-name>
   {
     "policy_id": "searchable_snapshot_policy"
   }
   ```
