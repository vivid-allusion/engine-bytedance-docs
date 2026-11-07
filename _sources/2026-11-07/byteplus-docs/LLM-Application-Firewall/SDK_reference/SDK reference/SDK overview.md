---
title: "SDK overview"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/SDK_overview"
---

The LLM Application Firewall SDK is a content security and compliance governance component designed for large language model applications, providing end\-to\-end compliance inspection and secure response capabilities from input prompts to model outputs. You can use this SDK to bind business assets (identified by **AppID**) with a protection policy, access the service address by region (**myUrl**/**region**), and perform content inspection and generate secure responses in either non\-streaming or streaming mode.

<span id="4e557cd9"></span>
## SDK introduction

The LLM Application Firewall SDK encapsulates the latest version of the API, uses an access key (AccessKey) to identify the caller, and provides features such as automatic signing to make it convenient to create and manage resources via the API.

Proxy service configuration is also supported. If your LLM application uses a proxy server to forward client data (such as user input) and receive and return server data (such as model responses), you can configure proxy\-related parameters during SDK initialization to meet business requirements.

<span id="900a5fbe"></span>
## Core features


* **Text content compliance inspection (non\-streaming)** : Submit the complete context at once for deep semantic analysis, which is suitable for scenarios requiring overall semantic understanding; the call returns inspection results and decision types (such as "observe" and "block") via the **Moderate** interface.

* **Text content compliance inspection (streaming)** : During model streaming responses, submit content in chunks for inspection to reduce overall wait time; control session lifecycle via `UseStream = 1 or UseStream = 2`, supporting scenarios where generation and inspection occur simultaneously.

* **Image content compliance inspection (non\-streaming):**  Inspect image content to avoid undesirable content such as gore, violence, and pornography, ensuring compliance and security and preventing model misuse.

* **Document content compliance inspection (non\-streaming)** : Inspect document content to avoid undesirable content such as gore, violence, and pornography, ensuring compliance and security and preventing model misuse.

* **Multimodal hybrid detection**: A single request can simultaneously submit multiple texts, images, or documents for compliance detection, improving detection efficiency.

* **Safe response generation**: When the detection result requires a "safe response", use the returned `MsgID` to call the **Generate **  API to obtain a safe and friendly response. The result is returned in a streaming format as paragraphs, suitable for scenarios that require automatic correction of output.


&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">When using streaming detection, you must wait until detection is fully completed (after the last submission with usestream=2) and the result is returned before calling the <code>Generate</code> API; otherwise, the call may fail.</div>


<span id="53f13062"></span>
## Version compatibility

The following lists the features supported by different SDK versions of the LLM Application Firewall. Before using the SDK, ensure that the SDK version matches the required features.


|Updates |Programming language |SDK version and GitHub address |
|---|---|---|
|Hallucination content protection and session management |python |[V3.0.49 and later versions](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/3.0.49) |
||Java |[V0.1.63 and later versions](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/0.1.63) |
||Go |[V1.0.67 and later versions](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/v1.0.67) |
|* Detection of proxy service data and document content<br><br>* Hybrid multimodal detection for simultaneous analysis of text, image, and document content. |python |[V3.0.26 and later versions](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/3.0.26) |
||Java |[V0.1.42 and later versions](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/0.1.42) |
||Go |[V1.0.45 and later versions](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/v1.0.45) |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">SDK versions prior to the ones listed only support text and image detection.</div>
