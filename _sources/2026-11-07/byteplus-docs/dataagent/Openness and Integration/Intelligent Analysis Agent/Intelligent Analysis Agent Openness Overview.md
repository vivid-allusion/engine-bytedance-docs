---
title: "Intelligent Analysis Agent Openness Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Analysis_Agent_Openness_Overview"
---

The Intelligent Analysis Agent currently supports third\-party invocation or integration through methods such as OpenAPI and iFrame. This document provides a brief introduction to the openness capabilities of the Intelligent Analysis Agent.


|Openness capabilities |Data query support |In\-depth research support |Description of openness capabilities & applicable scenarios |Operation guide |
|---|---|---|---|---|
|OpenAPI |Supported |Supported |* The Intelligent Analysis Agent provides a standard OpenAPI interface.<br><br>* Applicable to users with strong development capabilities and scenarios requiring flexible third\-party invocation of the Intelligent Analysis Agent's capabilities. |[API Release History](https://docs.byteplus.com/docs/dataagent/API_Release_History) |
|iFrame\-H5 |Supported |Supported |* The Intelligent Analysis Agent provides H5 iFrame integration capabilities based on JWT\-Token + iframe. When integrating via iFrame, a JWT\-Token must also be provided.<br><br>* All applications that support iFrame integration can be integrated, including web and mobile applications, such as Feishu, DingTalk, and many others. |[Intelligent Analysis Agent Third-Party Integration Guide](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide) |
|iFrame\-SDK |Supported |Supported |* The Intelligent Analysis Agent provides an iFrame integration SDK.<br><br>* By encapsulating the SDK, this integration method supports secure access without carrying the JWT\-Token in the `queryString` of the GET request, making it suitable for scenarios with security access requirements. |[JS SDK Integration Solution](https://docs.byteplus.com/docs/dataagent/JS_SDK_Integration_Solution) |
|Feishu bot |Supported |Not supported |* For users of the Feishu application, the Intelligent Analysis Agent can be directly integrated into the Feishu bot. |[Lark Integration](https://docs.byteplus.com/docs/dataagent/Lark_Integration_) |
