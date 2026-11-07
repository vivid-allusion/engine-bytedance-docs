---
title: "Voice Replication Order and Usage Guide"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication"
---

<span id="VEdKRfYm"></span>
# Overview

Voice Replication lets you create and manage custom voice replicas, and use the corresponding SpeakerID in Text\-to\-Speech (TTS) synthesis service. You can experience the full voice cloning workflow directly via the console, or perform advanced integrations through [our APIs](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-training).

**End\-to\-End Process**


1. **Purchase or create a voice slot.** 

   * **Prepaid voices:**  Purchase one or more voice slots in the console, or use the APIs for batch purchase and management. 

   * **Postpaid voices:**  No voice slot fee is charged when the voice is created. The voice slot fee is charged when the voice is first used for TTS speech synthesis. 

2. **Train the voice.** 

   Submit training audio for the selected SpeakerID, then query the training status. 

3. **Evaluate the voice quality.** 

   For postpaid voices, you can test the voice before committing to speech synthesis. **Test synthesis is charged based on the Sound Replication 2.0 model's pricing.** 

4. **Synthesize speech.** 

   Once you are satisfied with the voice quality, pass the trained SpeakerID to the TTS synthesis APIs through the speaker parameter. 


<span id="XEek1qyV"></span>
### Postpaid Voice Notes <span data-api-tag="add|yPgX5g">新增</span>


* **No upfront voice slot fee:**  When using a postpaid voice, the voice slot fee is **not charged immediately**. The fee is charged when the voice is first used for speech synthesis. Test synthesis is charged according to the **Sound Replication 2.0** model's pricing. 

* **The voice is fixed after synthesis:**  Once the voice is used for speech synthesis, it is finalized and **cannot be retrained or recreated**. Please make sure the voice quality meets your requirements before proceeding with speech synthesis. 

* **7\-day retention period:**  If a voice that has only been tested is not officially used within **7 days**, the system will automatically delete the voice.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Important</div>



* <div data-tips="true" data-tips-type="warning">We have recently launched <strong>Voice Replication 2.0</strong> along with an upgraded voice cloning API.</div>


   <div data-tips="true" data-tips-type="warning">Please note that newly purchased SpeakerIDs can only be used with the <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-training">new voice cloning API</a>. Existing SpeakerIDs are not affected and will continue to work with the <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v1">legacy API</a>. In addition, existing SpeakerIDs can be upgraded to the new <strong>Voice Replication 2.0</strong> model through the <a href="https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-upgrade">voice upgrade API</a> to benefit from the improved voice replication quality.   </div>
   

* <div data-tips="true" data-tips-type="warning">Voice slots for ICL 1.0 and ICL 2.0 have been unified and upgraded. They no longer incur storage fees or expire. This applies to both Prepaid and Postpaid voices. </div>



<span id="iEztetaG"></span>
# Prerequisite: Obtain an API Key

Before calling the APIs, sign in to the [BytePlus console ](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default)and go to **Settings \-\> API Keys** to create an API Key. The API Key is valid for a long time and can be disabled or deleted at any time.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Important </div>


<div data-tips="true" data-tips-type="warning">Treat your API Key as a sensitive credential. Do not expose it in public environments. </div>


<div data-tips="true" data-tips-type="warning">Store it securely and rotate it periodically to prevent unauthorized access and potential financial loss.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521105838-242236312849.png) </span>

<span id="1en9gleI"></span>
# Step 1. Buy voice slots and obtain SpeakerIDs

Buy voice slots before training. After purchase, each voice slot is associated with a SpeakerID. The SpeakerID is used in both Voice Replication APIs and TTS APIs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">All voice slots can be trained up to 15 times. Exceeding this limit will result in an error, and further training will not be possible.</div>


**Choose a purchase method**


|Method |Recommended scenario |How to proceed |
|---|---|---|
|Console UI |First\-time setup, manual testing, or a small number of voices. |* Click "Purchase" from the [console home page](https://console.byteplus.com/voice/new/experience/clone?projectName=default).<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616093642-762451925317.png) </span><br><br><br>*  Select "voice slot" as the product type<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616093732-1253900705281.png) </span><br><br><br>* Copy the newly purchased SpeakerID<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616094823-528554200363.png) </span> |
|API batch purchase / management |Batch onboarding, platform integration, or automated voice management. |Use the [Voice Replication Management APIs](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationopenapi) to purchase or manage voice slots in batches.<br><br><br>1. Call `OrderAccessResourcePacks` to purchase a batch of voice slots. <br><br>2. Call `ListMegaTTSByOrderID` to list SpeakerIDs by orderID returned from step 1.<br><br>3. Call `BatchListMegaTTSTrainStatus` to list all existing SpeakerIDs. |


> **Note: ** This step is **not required** if you use **postpaid voices** over the [API](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-training).


<span id="wd8mhcV8"></span>
# Step 2. Train the voice

**Choose a training method**


|Method |Recommended scenario |How to proceed |
|---|---|---|
|Console UI |First\-time setup, manual testing, or a small number of voices. |* Click "Upload Audio" to upload a prompt audio file and start replication. <br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616100208-1165012901060.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616100321-1391701333474.png) </span><br><br><br>* After a successful clone, you can obtain the speakerID and try TTS synthesize directly. <br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616100551-532513080413.png) </span><br><br><br>* If you would like to train a new version for an existing SpeakerID (within 15 times), go to "Voice Library" \-\> "My Voices", and start a new training from there. <br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616101055-1230068676289.png) </span><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616101128-218207599681.png) </span> |
|Voice Clone APIs |Batch onboarding, platform integration, or automated voice management. |Refer to the [Voice Replication V3](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-voice-training) documentation, specify the local audio file path, encode it into Base64, and submit the request to complete voice replication.<br><br><br>1. Call `voice_clone` to upload prompt audios for new voice slots. <br><br>2. Call `get_voice` to query the status of existing SpeakerIDs.<br><br>3. Call `upgrade_voice` to upgrade a SpeakerID from the legacy Voice Replication 1.0 to Voice Replication 2.0<br><br><br>The enumeration for SpeakerID's `status` is as below, the SpeakerID can be used for TTS services if the status is `2` or `4`. <br><br><br>* NotFound = 0<br><br>* Training = 1<br><br>* Success = 2<br><br>* Failed = 3<br><br>* Active = 4<br><br><br>The enumeration for SpeakerID's `model_type` is as below.<br><br><br>* Voice Replication 1.0: `model_type = 1`<br><br>* Voice Replication 2.0: `model_type = 5`<br><br><br>For troubleshooting, see the [Error Code documentation](https://docs.byteplus.com/en/docs/byteplusvoice/voicereplication-v3-error-code-reference). |


> **Note:**  The Experience Center in the official website console currently supports **prepaid voices only**.


<span id="Ld2CHwb0"></span>
# Step 3. Synthesize speech with TTS

**Choose a synthesize method**


|Method |Recommended scenario |How to proceed |
|---|---|---|
|Console UI |First\-time setup, manual testing, or a small number of voices. |* Go to "Voice Library" \-\> "My Voices" and locate the cloned voice you would like to use.<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616114957-764901079946.png) </span><br><br><br>* Enter the text you would like to synthesize and click "Generate".<br><br><br><span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260616115126-1328833473254.png) </span> |
|TTS Synthesis APIs |Batch onboarding, platform integration, or automated voice management. |Please refer to:<br><br><br>* [TTS - Bi-directional Streaming (WebSocket)](https://docs.byteplus.com/en/docs/byteplusvoice/streaming_tts) for bi\-directional TTS usage.<br><br>* [TTS - Unidirectional Streaming (HTTP)](https://docs.byteplus.com/en/docs/byteplusvoice/unidirectional_tts_http) for uni\-directional TTS usage.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Important</div><br><br><br><div data-tips="true" data-tips-type="warning">The <strong>resource ID</strong> should be as below when trying to call TTS service with cloned SpeakerIDs.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Voice Replication 1.0：</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong><code>seed-icl-1.0</code></strong><strong> </strong>or<strong> </strong><strong><code>volc.megatts.default</code></strong><strong> </strong></div><br><br><br>* <div data-tips="true" data-tips-type="warning">Voice Replication 2.0:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong><code>seed-icl-2.0</code></strong></div><br> |


&nbsp;

&nbsp;

&nbsp;
