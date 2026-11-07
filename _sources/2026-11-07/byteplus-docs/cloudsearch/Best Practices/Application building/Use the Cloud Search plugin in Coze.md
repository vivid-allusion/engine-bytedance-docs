---
title: "Use the Cloud Search plugin in Coze"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Use-the-Cloud-Search-plugin-in-Coze"
---

This topic describes the complete process of using the Cloud Search plugin in Coze

<span id="vddoVC5h"></span>
## Background

The Volcano Cloud Search Service plugin is provided by BytePlus Cloud Search Service. It uses BytePlus's Elasticsearch and OpenSearch engines and is compatible with the open\-source Elasticsearch and OpenSearch syntax. It supports hybrid text and vector search, effectively combining precise queries with semantic queries. The Volcano Cloud Search Service plugin also supports storing ultra\-large\-scale vectors (ranging from hundreds of thousands to fifty billion) and enables [Coze](https://www.coze.cn/open/docs/guides/welcome) chatbot to use cloud search features.

The Volcano Cloud Search Service plugin now supports the search template tool, allowing vector\-text recall by calling the Elasticsearch or OpenSearch search template API.

<span id="NBCjmXdh"></span>
## Activate Cloud Search service instance and build knowledge base


1. **Turn on the BytePlus Cloud Search service**

   1. Register a BytePlus account and complete real\-name authentication.

   2. Activate [Cloud Search service](https://www.byteplus.com/en/product/es) in the BytePlus console.

2. **Create an engine instance**

   Create an Elasticsearch or OpenSearch instance. For more information, see [Getting Started](https://docs.byteplus.com/en/docs/cloudsearch/getting-started).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to use OpenSearch 2.9.0 or later for hybrid search and vector\-related scenarios, supporting tens of billions of vectors.   </div>
   

3. **Enable public network access**. Enable public network access for the instance. For more information, see [Configure instance public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access).

4. **Build knowledge base**

   1. Create an index and import data. For hybrid retrieval (e.g., combined vector and keyword search), see [Best practices for hybrid retrieval and re-ranking based on Cloud Search](https://docs.byteplus.com/en/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search).

   2. Create a search template. Since DSL configuration involves one or more parameters and can be complex, it is recommended to configure a search template to standardize the query. For example, the following is a template for hybrid queries on Cloud Search documents. It is recommended to configure the parameters from, size, and keyword, which represent the starting offset, the number of results returned per query, and the search keywords, respectively.

      ```YAML
      PUT _scripts/my_search_template
      {
        "script": {
          "lang": "mustache",
          "source": {
            "_source": {
              "excludes": "*_knn"
            },
            "from": "{{#from}}{{from}}{{/from}}{{^from}}0{{/from}}",
            "size": "{{#size}}{{size}}{{/size}}{{^size}}10{{/size}}",
            "query": {
              "hybrid": {
                "queries": [
                  {
                    "remote_neural": {
                      "summary_knn": {
                        "query_text": "{{keyword}}",
                        "k": 1000
                      }
                    }
                  },
                  {
                    "match": {
                      "summary": "{{keyword}}"
                    }
                  }
                ]
              }
            }
          }
        }
      }
      ```
      


<span id="Wgl4Aagq"></span>
## Use the Volcano Cloud Search plugin in Cozy

Depending on the application scenario, this document separately introduces the operation process of using the Cloud Search plugin in Cozy's AI assistant and in Doudi workflow.

<span id="BdfmfgsI"></span>
### Use the Cloud Search plugin in the AI assistant plugin.


1. Create an AI assistant in Doudi. For more details about creating a Doudi AI assistant, see [Build an AI assistant agent](https://www.coze.cn/open/docs/guides/agent_quick_start).

2. In the newly created Coze agent’s **skills**, search for the “Volcano Cloud Search Service” plugin and add it. For detailed information on adding plugins to the Cozy agent, refer to [Add skills to the agent > Plugins](https://www.coze.cn/open/docs/guides/agent_plugin).

3. Edit the following parameters of the Volcano Cloud Search plugin within the agent and set whether the parameters are visible. For more details about modifying plugin parameters, see [Plugins > Parameters configuration](https://www.coze.cn/open/docs/guides/agent_plugin#95b4b08d).

   
   |Parameter name |Description |Visibility |
   |---|---|---|
   |endpoint |Public network access address for OpenSearch. Must be a complete URL (e.g., https://host:port). |No |
   |username |Authentication username |No |
   |secret |Password for the username. |No |
   |Index |Index name |No |
   |params |Query URL parameters, fill in information such as pipeline. |No |
   |template_id |ID of the preset search template. Enter the ID of the search template created above here. |No |
   |template_param_keyword |Search keywords (corresponding to {{keyword}} in the template), length <8000 characters. |Yes |
   |template_param_size |Number of results per page (corresponding to {{size}} in the template, 1 ≤ value ≤ 200). |Yes |
   |template_param_from |Pagination start offset (corresponding to {{from}} in the template). If provided, must be ≥ 0. |Yes |
   |template_source |Search template content passed directly (JSON format). |No |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After setting the default value of a parameter and making it invisible, the agent will use only this preset value when invoking the plugin. This reduces unnecessary judgments by the large model and improves plugin call efficiency.   </div>
   

4. Modify the agent’s persona and response logic.

   ```Plain Text
   每次用户输入时，先调用BytePlus云搜索服务的search_template工具进行搜索，用户问题作为template_param_keyword参数输入。输出结果在hits中用列表显示。
   ```
   

5. Perform query debugging.


<span id="HT18Pvbl"></span>
### Use the Cloud Search plugin in Workflow.


1. Create a Workflow in the Koozy agent or resource library. For detailed information on creating workflows in the Coze AI, refer to [Add skills to the agent > Workflows](https://www.coze.cn/open/docs/guides/agent_workflow). For more information, see [Create a workflow](https://www.coze.cn/open/docs/guides/use_workflow#3cb77b2e)

2. Select the **Volcano Cloud Search Plugin (search_template)**  tool in the workflow

3. Configure the inputs and outputs of search_template

4. The output result is in the source field, formatted as a JSON string The following is an example of parsing this string into text for further processing

   ```Python
   import json
   async def main(args: Args) -> Output:
       params = args.params
       print(params)
       # Build output object
       value = ""
       for item in args.params["input"]:
            for content in json.loads(item["source"])["content"]:
               value+=content["summary"]+"\n"
       ret: Output = {"content": value}
       return ret
   ```
   

5. Perform query debugging
