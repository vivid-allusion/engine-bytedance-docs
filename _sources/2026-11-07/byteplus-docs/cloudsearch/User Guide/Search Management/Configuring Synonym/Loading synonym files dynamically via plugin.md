---
title: "Loading synonym files dynamically via plugin"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/using-synonym-plugin"
---

After you enable a synonym file in hot mode, the file does not automatically apply to existing indices. You can use the system plugin called analysis\-dynamic\-synonym to enable new synonym files to dynamically apply to existing indices. This topic describes how to use this plugin.

<span id="39b5b475"></span>
## Before you begin


* In this example, you log on to Kibana for index\-related operations, so make sure that the visualization tool has internet\-facing access enabled. For more information, refer to [Configuring public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool).

* Prepare a synonym term containing `CloudSearch,Elasticsearch` . You can configure it via GUI or upload a synonym file, and enable it. For more information, please see [Configuring synonym terms via GUI](https://docs.byteplus.com/docs/cloudsearch/31989) and [Uploading synonym files](https://docs.byteplus.com/docs/cloudsearch/uploading-synonym-files).

* Add the synonym terms to the IK main dictionary file and enable the dictionary file. You can configure it via GUI or upload an IK dictionary file, and enable it. For more information, please see [Configuring synonym terms via GUI](https://docs.byteplus.com/docs/cloudsearch/31989) and [Uploading IK dictionary files](https://docs.byteplus.com/docs/cloudsearch/31988).


<span id="b53d00e8"></span>
## Creating an index and specifying the synonym plugin


1. Go to the Kibana logon page by using one of the following methods:

   * On the **List of Instances** page, find the instance and click **Kibana** or **Dashboards** in the **Actions** column.

   * On the **Visualized control** Area of the **Instance information** tab, click the **Public network Entrance**.

2. On the Kibana logon page, type the username and password, then click **Log In**.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your password, go to the **Instance information** page and reset the password.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826ab6d2df5f4888a0e6b5a2db4f04e0~tplv-goo7wpa0wc-image.image) </span>

3. In the left\-side navigation pane of the Kibana page, choose **Management \> Dev Tools**. In the code area, run the following command to create an index and specify the synonym plugin

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command creates an index named <strong>doctest\-6</strong> and specifies the subsequent operations:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Configure an interpreter named <code>by_ik_smart</code>, use the <code>ik_smart</code> dictionary file, and specify the <code>default_dynamic_synonym</code> plugin.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In <strong>mappings</strong>, set fields in the index and specify the interpreter.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The command applies to instances whose version is 7.10.2. If your instance version is 6.7.1, adjust the command.   </div>
   

   ```Shell
   PUT /doctest-6
   {
     "settings": {
       "analysis": {
         "analyzer": {
           "by_ik_smart": {
             "tokenizer": "ik_smart",
             "filter": [
               "default_dynamic_synonym" 
             ]
           }
         }
       }
     },
      "mappings": {
           "properties": {
               "name": {
                   "type": "text",
                   "analyzer":  "by_ik_smart"
               }
           }
       }
   } 
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3346b957249548ef87703feba4afd7ec~tplv-goo7wpa0wc-image.image) </span>

4. Verify that the synonym file takes effect.

   ```Shell
   GET /doctest-6/_analyze
   {
   "analyzer": "by_ik_smart",
   "text": "CloudSearch"
   }
   ```
   

   The response indicates that `CloudSearch` and `Elasticsearch` are synonyms.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3fecf1694114371819312cbbc8eb0ce~tplv-goo7wpa0wc-image.image) </span>

5. In the code area, run the following command to write document data to the index.

   ```Shell
   POST /doctest-6/_doc/1
   {"name": "CloudSearch"}
   ```
   

6. In the code area, run the following command to query the document.

   ```Shell
   GET /doctest-6/_search?explain
   {
     "query": {
       "match": {"name": "Elasticsearch"}
     }
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3656b92331c42829e968d65eb3ae9ff~tplv-goo7wpa0wc-image.image) </span>

   When you query `Elasticsearch`, the response is `CloudSearch`, indicating that the synonym file takes effect.


<span id="aa998dc4"></span>
## Enabling a synonym file in hot mode

Modify the content of the synonym file to include `CloudSearch,Elasticsearch,ES` by adding `ES`. Then, update the synonym file in hot mode, meaning that the changes take effect while the instance is running.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**, and then click **File management** tab.

2. In the synonym file list, find the synonym file that you want to update, and then click **Hot Module Replacement** in the **Actions** column.

3. In the displayed dialog box, upload the updated file with the unchanged file name, and then click **Close**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/010b78951f38448b9d57c1e0c03c7a78~tplv-goo7wpa0wc-image.image) </span>

4. In the left\-side navigation pane of the Kibana page, choose **Management \> Dev Tools**.

5. Create an index and write document data into it.

6. Verify that the synonym file takes effect.

   ```Shell
   GET /doctest-8/_analyze
   {
   "analyzer": "by_ik_smart",
   "text": "CloudSearch"
   }
   ```
   

   The response indicates that `CloudSearch`, `Elasticsearch`, and `ES` are synonyms.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f59b7c42a3414a078336ad2e9a7e7eb5~tplv-goo7wpa0wc-image.image) </span>

7. In the code area, run the following command to query the document.

   ```Shell
   GET /doctest-8/_search?explain  
   {
     "query": {
       "match": {"name": "ES"}
     } 
   }
   ```
   

   When you query `ES`, the response is `CloudSearch`, indicating that the synonym file is dynamically loaded.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6d895c1518c4c58a70bb6962b0be01d~tplv-goo7wpa0wc-image.image) </span>
