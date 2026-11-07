---
title: "Model Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Model_Configurations"
---

In the Data Agent platform, model configuration is the core prerequisite for ensuring the proper operation of intelligent query and in\-depth research functionalities. By correctly selecting and connecting the embedding model, query model, and analysis model, you can ensure that the system efficiently processes dataset embedding, accurately understands user queries, and generates in\-depth analysis reports.

<span id="6779bd08"></span>
# Prerequisites


* The model configuration feature requires super administrator permissions.


<span id="39346627"></span>
# Select models


1. After logging in to the BytePlus console, click Intelligent Analysis Agent to enter the product. Select a project to access the agent list.

2. At the top of the Intelligent Analysis Agent list page, click the Model Configuration button to enter the configuration interface.

3. After entering the model configuration interface, you will see three configuration items: embedding model, query model, and analysis model. After selecting the target model from the available model list, the intelligent query and analysis models must be tested for connectivity.

   
   |Configuration items |Function |Instructions |
   |---|---|---|
   |**Embedding model (Embedding)**  |Converts text/data into vectors for semantic retrieval and knowledge base matching. |Select the model from the dropdown list; it is saved automatically.<br><br>**Caution**: If the user changes the embedding model, reconfigure embedding in the model configuration interface. |
   |**Intelligent query model** |Convert natural language questions into data query commands (such as SQL), for the intelligent query feature |After selecting a model from the dropdown, click the Test Connection button. If "Connection successful" is displayed, the connection takes effect. |
   |**Analysis model** |Interpret data results and generate business insights, for the in\-depth research and insights report features. |After selecting a model from the dropdown, click the Test Connection button. If "Connection successful" is displayed, the connection takes effect. |
   

4. Click the **Test Connection** button on the right side of the intelligent query and analysis models to ensure the selected models are available. After clicking, the system will initiate a connectivity check. The check results are explained as follows:

   * Check passed: The model status is normal and can be saved.

   * Check failed: The interface will display specific error information based on the error type provided by R&D. Please modify the model selection according to the prompts.

5. After completing the selection, click the Submit button in the upper right corner to complete the model configuration.

   Closing the page during submission: If you close the browser after clicking Submit but before the test connection is completed, the current configuration **will not be saved successfully**. When you next enter the configuration page, the last successfully saved model configuration will still be displayed.


&nbsp;
