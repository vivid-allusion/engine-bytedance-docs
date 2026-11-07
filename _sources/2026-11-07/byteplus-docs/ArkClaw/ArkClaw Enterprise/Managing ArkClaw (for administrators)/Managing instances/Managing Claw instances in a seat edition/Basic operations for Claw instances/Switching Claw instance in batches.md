---
title: "Switching Claw instance in batches"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Bulk_switching_models_for_Claw_instances"
---

After the administrator modifies the available model or default model in model management, the default model modification only takes effect for newly created Claw instances. Existing instances will not be automatically synchronized. **This article describes how to use bulk operations to uniformly apply model modifications to existing Claw instances.** 

<span id="paqB5XvD"></span>
## Prerequisites

Model configuration modification has been completed. For detailed operations, please refer to [model management](https://docs.byteplus.com/en/docs/ArkClaw/Model_management).

<span id="ooGiPAuX"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group).

2. In the left\-side navigation pane, choose "Claw management \> Claw list".

3. Under the "Instances" tab, select all target Claw instances.

4. Switch the model of employee Claw instances/shared Claw instances based on your actual scenario.

   
   <Tabs>
   <Tab zoneid="qhMR8b04WJ" title="Switch to Default model">
   <TabTitle>Switch to Default model</TabTitle>
   
   * **Application scenarios**: This operation applies when you decommission models or specify that employees use the default model. After the operation, the model used by employee Claw instances is switched to the default model, and the available model list is updated. This operation may affect running tasks. Perform the operation when employees are idle.
   
   * **Note**:
   
      * After switching, the model currently used by all selected Claw instances will be immediately updated to the Default model.
   
      * After the administrator switches all instances to the Default model, employees can still modify to other available models. For detailed procedures, refer to [Adjust inference model](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__).
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Switching to the Default model will<strong> affect</strong> tasks running on the current Claw instances. Please proceed with caution.      </div>
         
   
      * **Procedure**: Click “… \> Switch to Default model” at the bottom of the list.
   
   
   </Tab>
   <Tab zoneid="IUzs3Ln0Lw" title="Issue latest model configuration">
   <TabTitle>Issue latest model configuration</TabTitle>
   
   * **Application scenarios**: This operation applies when Claw available models are added in model configuration. After the operation, the list of models available for employee Claw instances is updated. This operation interrupts all tasks currently running in the selected Claw instances. Confirm the scope of impact before operating. We recommend that you notify the relevant employees in advance.
   
   * **Description after operation**:
   
      * After the configuration is issued, the **available model types** of all selected Claw instances are immediately updated to the models configured by the current administrator.
   
      * If the model update deletes the model currently used by the Claw instance, after issuing the latest model configuration, the current model of the Claw instance will become the default model. If the model update still contains the model currently used by the Claw instance, after issuing the latest model configuration, the current model of the Claw instance will remain unchanged, and only the available model range will be updated to the latest model.
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Issuing the latest model configuration will <strong>interrupt</strong> all tasks currently running in Claw instances. Please proceed with caution.      </div>
         
   
      * **Procedure**: Click "... \> Issue latest model configuration" at the bottom of the list.
   
   
   </Tab>
   </Tabs>
   

5. In the dialog box that pops up, click the "OK" button to complete the operation.

6. After the operation is completed, check whether the "Default model" column of the target instance in the Claw list has been updated to the expected model. Employees will automatically use the new model the next time they open the Claw instance.
