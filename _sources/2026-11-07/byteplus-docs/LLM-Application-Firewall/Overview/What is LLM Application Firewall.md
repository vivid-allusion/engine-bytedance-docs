---
title: "What is LLM Application Firewall"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/What_is_LLM_Application_Firewall"
---

The LLM Application Firewall is a security service designed to protect the inputs and outputs of your large language model (LLM) applications. It defends against common threats like those in the OWASP LLM Top10, including prompt injection and resource exhaustion, while also preventing sensitive data leaks. This document provides an overview of its core protection capabilities to help you determine if it meets your AI security requirements.

<span id="bb683367"></span>
## Highlights

<span id="9359161a"></span>
### **Simplified deployment**

The deployment solution is flexible, requires no complex system modifications, and adapts to various business scenarios.

<span id="9359161a"></span>
### **Layered protection**


* Monitors and prevents excessive consumption of computing resources to avoid system failures caused by resource exhaustion.

* Identifies and blocks prompt injection attacks in real time to protect LLM services from AI impersonation, instruction hijacking, and prompt leaking.

* Analyze model usage, enforce role definitions, and prevent inappropriate output.

* Accurately identify data security risks and prevent the leakage of sensitive content, such as personal information and business data.


<span id="9359161a"></span>
### **Intelligent optimization**

Uses advanced algorithms to generate compliant and safe alternative responses, effectively mitigating potential risks.

<span id="fd18ae36"></span>
## Protection capabilities

<span id="58138f06"></span>
### Resource exhaustion mitigation

Computational resource exhaustion is an attack where malicious prompts are sent to an LLM, causing a rapid depletion of its computational resources and resulting in service degradation or unavailability. The LLM Application Firewall can identify prompts with high GPU resource consumption and promptly log or block related requests to ensure business stability.

<span id="58138f06"></span>
### Prompt injection protection

The LLM Application Firewall automatically identifies potential risks in malicious prompts to prevent prompt injection, privilege escalation, and similar attacks. This system ensures that model outputs comply with safety standards through real\-time monitoring and interception mechanisms.

<span id="58138f06"></span>
### Model abuse prevention

By continuously analyzing the model's input and output data, the LLM Application Firewall can identify risks such as misconfigured roles or outputs that violate the content policy. This proactive monitoring helps ensure the model operates as intended and prevents its misuse.

<span id="58138f06"></span>
### Sensitive data disclosure prevention

The LLM Application Firewall uses advanced text risk and sensitive information detection algorithms to identify and filter sensitive data in model outputs, ensuring data security and compliance.

<span id="58138f06"></span>
### General topic control

For specific business scenarios, the LLM Application Firewall can perform compliance checks on input content by topic, using provided samples and rule descriptions. This helps enterprises control model output, preventing the disclosure of inappropriate information and avoiding public relations risks. For example, it can block responses to inquiries about internal financial reports or negative corporate news to prevent unfair competition or reputational damage.
