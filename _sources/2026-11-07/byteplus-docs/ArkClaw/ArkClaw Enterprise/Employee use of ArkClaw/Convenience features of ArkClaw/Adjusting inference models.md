---
title: "Adjusting inference models"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__"
---

After the administrator configures multiple models, you can switch the inference model used by ArkClaw based on actual business scenarios.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The inference model can be switched through multiple entry points (as shown below). This topic only describes the operations for Entry ②, which displays full information.</div>


* <div data-tips="true" data-tips-type="default">The model list for Entry ② will synchronize automatically with configuration updates made by the enterprise administrator and always shows the latest models configured by the administrator.</div>


* <div data-tips="true" data-tips-type="default">The model list for Entry ① only shows models that have been selected for Entry ②. To use the latest available models, you need to switch through Entry ② first.</div>


* <div data-tips="true" data-tips-type="default">To use models not included in the list, please contact your enterprise administrator for configuration.</div>



<div data-tips="true" data-tips-type="default"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ae616de429bbbaa8a6853a986f30c98.png" width="486px" /></div>


<span id="cYeQYxyi"></span>
## Prerequisites


* The administrator has configured multiple inference models.

* If the model configured by the administrator is a custom model and the system prompts for authentication credentials, please contact the administrator to obtain your personal API Key (used for authentication when calling the model).


<span id="5okFz6yc"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Click the "Switch model" button.

4. Select a model configured by the administrator. To use a model that is not included, contact the enterprise administrator to configure it.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the models supported by Coding Plan and model recommendations, see <a href="https://docs.byteplus.com/en/docs/ModelArk/2276791?_vtm_=a78999.b69280.0_0.0_0.0.209_7651889180379710981#74c1f76c">Supported models</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the models supported by "Foundation models" and selection recommendations, see <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/model?groupType=ModelGroups&vendor=Bytedance&view=DEFAULT_VIEW">Foundation models</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For custom model introduction and selection recommendations, contact the enterprise administrator.   </div>
   

5. (Optional) If the selected custom model prompts for an API Key, enter your personal API Key. Then, click the "Confirm" button to switch the ArkClaw inference model.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the same model pool, you only need to configure the API Key once. When switching to any model under this model pool later, the system automatically reuses the saved API Key, so you do not need to enter it again.   </div>
   

6. **The new configuration takes effect automatically within 1 minute**. Once it takes effect, ArkClaw will use the new model for inference.
