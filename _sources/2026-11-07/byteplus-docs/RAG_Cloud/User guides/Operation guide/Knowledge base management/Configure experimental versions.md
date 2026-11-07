---
title: "Configure experimental versions"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Configure_experimental_versions"
---

To find the most effective processing strategy for your knowledge base, you can create an experimental version. This feature allows you to test different offline processing configurations, such as embedding models and slicing strategies, using your existing documents. It provides a safe environment to evaluate performance without impacting the main version or requiring you to re\-upload documents.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The experimental version allows you to configure different offline processing strategies (such as embedding models, slicing strategies, and more) based on the existing knowledge base documents, and test their effectiveness. During this process, you do not need to upload documents again.</div>


<span id="6c339879"></span>
# Procedure


1. Entry points for experimental version features. Currently, there are two entry points for experimental version features, as shown in the diagram below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d88602bd39be43adb0dfacc9be5ac59b~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c5a89879b034e659e85c00b14be0b98~tplv-goo7wpa0wc-image.image) </span>

2. Create a new experimental version.

   Configuring an experimental version is almost the same as configuring a knowledge base. When creating a new experimental version, you can set the document processing strategies you want to test. Note the following configuration items:

   1. Experimental version name: Must not be the same as the name of the main version. The name must start with an English letter, cannot be empty, and can only contain letters, numbers, and underscores (_), with a length of 1 to 128 characters.

   2. Data type: The data type of the experimental version of the knowledge base must be consistent with that of the main version.

   3. Synchronize newly added documents: When enabled, documents uploaded to the main version of the knowledge base will be automatically processed according to the current experimental version's strategy.

   4. For other parameter settings, refer to [create](https://docs.byteplus.com/docs/209/pipeline_create).

      **Note: Each experimental version is resource\-isolated and billed separately. Please create with care!** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb6c9bacab0048788c8c40df76e75ea6~tplv-goo7wpa0wc-image.image) </span>

3. Open the experimental workspace.

   You can see the names of the main version and the experimental version. Click to switch between versions or configure each version separately.

   After importing documents and completing parsing and processing, you can perform knowledge search and Q&A.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a20823a206a649c7a430d3274a4c2112~tplv-goo7wpa0wc-image.image) </span>

4. Import documents.

   **Note: The experimental version does not support uploading documents; it only supports importing documents from the main version.** 

   You can choose to import some documents from the main version for testing, or import all existing documents from the main version at once.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53857d74c583470880e9d2b3e88b8e21~tplv-goo7wpa0wc-image.image) </span>

5. Publish as main version.

   You can choose to publish the experimental version as the main version. After publishing, the experimental version's configuration becomes the main configuration of the knowledge base, and the original main version's configuration is retained as an experimental version.

   **Note: The experimental version can be published as the main version only when it contains all the documents from the main version.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4eae1048ee4957ba2ebb0252c70d14~tplv-goo7wpa0wc-image.image) </span>

6. Delete experimental version.

   You can choose to edit or delete the experimental version in the version information section of the knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/528ec8fb662d41ed84527776d4ff4fbe~tplv-goo7wpa0wc-image.image) </span>
