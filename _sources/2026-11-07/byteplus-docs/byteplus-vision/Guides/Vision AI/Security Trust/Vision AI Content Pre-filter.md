---
title: "Vision AI Content Pre-filter"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/vision-ai-content-pre-filter"
---

At BytePlus, we're committed to harnessing the power of AI responsibly and ethically. We rigorously invest in building robust systems and safeguards to ensure our AI solutions deliver competitive, reliable, and safe performance while adhering to the safety and security standards.

For enhanced safety performance, BytePlus offers the **Content Pre\-filter System**, a robust protection mechanism adaptable for diverse application scenarios. This content filter can detect specific categories of potentially risky content in input prompts and output completions, and will implement corresponding measures, such as refusing to answer or returning a more benign response. This protection mechanism, through a layered security stack, contributes to improving the robustness of the entire system.

&nbsp;

<span id="lLp7981b"></span>
## **I. How to Enable/Disable the Content Pre\-filter System**

Currently, BytePlus has integrated the Content Pre\-filter System into the Vision AI platform. Users can click on **Overview** tab in the [Vision AI console](https://console.byteplus.com/ai/overview) to enter the **Activated API List** interface, where they can enable or disable the Content Pre\-filter System function.


* **Activate API:**  When users activate an API service, they can control the content filtering function via the Content Pre\-filter button. To ensure the stability of content security, this feature is enabled by default.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_135320e8aef2a64e07d16c10f363dfff.png) </span>

**Please note**:


   * The implementation of Content Pre\-filter shall not be construed as a warranty by BytePlus regarding the appropriateness, or compliance of AI generated content. The user remains solely responsible for the usage of any generated content and shall bear all liability and damages arising from such use.

   * Regardless of whether the user enables or disables the Content Pre\-filter, they must comply with the customer agreement and [BytePlus GenAI Acceptable Use Policy](https://docs.byteplus.com/en/docs/legal/acceptable_use_policy_byteplus_genai).


<div style="text-align: center">
</div>


Besides filtering risky content, BytePlus also identifies content and/or behavior that may violate applicable product terms when using the service. Please note that even if you disable this feature, our services still maintain baseline content safety policies to strive to provide a positive usage environment for every user.

&nbsp;

<span id="Sq4HYbyD"></span>
## **II. How the Content Pre\-filter System Works**

When a user enables the Content Pre\-filter System feature, the system will detect and identify risky content when calling an API. It will then take action by refusing to answer or intervening in the response. 


* For users calling the API, when the system identifies risky content, the error "Algovproxy Risk Error" will be returned. For example:


```JSON
{
    "code": 50510, 
    "data": None, 
    "message": "Algovproxy Risk Error", 
    "request_id": "xxxxx", 
    "status": 50510, 
    "time_elapsed": "2.156702557s"
}
```


&nbsp;

<span id="o5WSKDvC"></span>
## **III. What Data Does the Content Pre\-filter System Filter?** 


* **Minor Safety:**  Any content involving the infringement of personal privacy of children and underage adolescents, and harm to their physical and mental health.

* **Hate Speech and Hateful Content:**  Including but not limited to racial discrimination, nationality discrimination, ethnic discrimination, sexual orientation, personal appearance, physical disabilities, etc.

* **Nudity, Sexual, and Graphic Content:**  Including but not limited to pornography, abuse, violence, and self\-harm, etc.

* **Misinformation:**  Content that is clearly deceptive and significantly inconsistent with facts.


&nbsp;

<span id="XwdjS2nx"></span>
## **IV. Data Privacy and Protection**

It is important to note that when users choose to enable the Content Pre\-filter feature, we will, in compliance with applicable laws and regulations, retain logs from the use of the Content Pre\-filter feature and the risk\-related content data filtered by it for a limited period. This data is stored on servers in Malaysia or Singapore belonging to BytePlus or its affiliates. The collected data will be used to assist you in troubleshooting issues encountered during use and to ensure normal operation.

BytePlus has established a comprehensive data security protection system, employing encryption technologies for data transmission and storage to ensure data confidentiality throughout these processes. Concurrently, we strictly control data access permissions. Data access activities are monitored and audited in real\-time to safeguard your data against unauthorized acquisition by any third\-party channels.

BytePlus will continue to invest in research to explore the development of reliable artificial intelligence systems that consistently adhere to our policies and human intent. We aim to help ensure that AI\-generated content is healthy and safe for all users and will incorporate user feedback to achieve responsible innovation. Should you have any questions or suggestions, please do not hesitate to contact us at any time. Thank you for your trust and support in BytePlus!
