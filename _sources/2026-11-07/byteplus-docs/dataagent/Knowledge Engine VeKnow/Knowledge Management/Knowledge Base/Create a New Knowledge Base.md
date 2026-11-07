---
title: "Create a New Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Create_a_New_Knowledge_Base"
---

Enterprise knowledge engines need to build corresponding knowledge bases. This article shows you how to create different types of knowledge bases.

# Operation Steps

1. Go to the Enterprise Knowledge Engine page and click **Knowledge Management \> Knowledge Base** in the left navigation bar.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a547dcd4364c473bb37a3ad5d30cd65e~tplv-goo7wpa0wc-image.image)

2. Click **Add Knowledge Base** , fill in the basic configuration information, and click "Save" after completion to complete the creation of the new knowledge base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b29e2f153c4248998f1ef825149aa513~tplv-goo7wpa0wc-image.image)

   The specific parameter configuration instructions are as follows:

   |parameter |parameter description |
   |---|---|
   |name |Knowledge base name |
   |describe |Briefly describe the purpose or content of the enterprise knowledge engine (limited to 200 words). |
   |content type |Select the type of knowledge base. Currently, the following five types are supported:<br><br><br>* General content: Support uploading files, importing from WeChat library, importing from object store, importing from relational database.<br><br>* Query cache: Support XLSX, CSV and other format files.<br><br>* QA Q & A: Support XLSX, CSV and other format files.<br><br>* Terminology: Supports XLSX, CSV and other formats.<br><br>* Customer data: used to create a principal repository that supports uploading principal data already in VeCDP.<br><br><br>> **说明**<br><br><br><br>* > The Query Cache Type Knowledge Base is a value\-added option at an additional cost.<br> |
   |Whether to update knowledge regularly |No update required: One\-time import, no need to update data later.<br><br>Timed update: Support setting the update frequency according to the day/week/month granularity, and specifying the specific update time. If there is no 31st day of the month, the date is skipped. Timely update of task execution, you can view the status of knowledge updates through each knowledge update time on the knowledge management page in the knowledge base.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17315c0b18694105bb2fb8abb5e89f71~tplv-goo7wpa0wc-image.image) |

# Next Step

1. After the knowledge base is created, you need to import and manage knowledge. For details, please refer to [Import Knowledge](https://docs.byteplus.com/docs/dataagent/Import_Knowledge)and [Knowledge Management](https://docs.byteplus.com/docs/dataagent/Manage_Knowledge).

2. Build ontology semantics and Knowledge Graph, see [Ontology Semantic Construction](https://docs.byteplus.com/docs/dataagent/Ontology_Semantic_Construction)and [Knowledge Graph](https://docs.byteplus.com/docs/dataagent/Knowledge_Graph).

3. Project and management, please refer to the specific operation [Authorization Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__).
