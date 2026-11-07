---
title: "Features"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/features"
---

The LLM Application Firewall is a security service that protects your large language model (LLM) applications from common security threats. This conceptual guide explains its core protection mechanisms, including how it mitigates resource exhaustion attacks, detects prompt injections, filters sensitive data, and ensures compliant content generation to enhance your application's security and stability.

<span id="c653dcc9"></span>
## Protection against resource exhaustion attacks

Resource exhaustion refers to the amount of computing resources used by a server when performing computational tasks. Attackers can sharply increase an LLM's resource consumption by sending it specially crafted inputs. After an attack, requests that would normally take a few seconds can require extensive computation, potentially leading to service outages. The LLM Application Firewall can identify these resource\-intensive prompts and apply configured policies to maintain service availability.


* **Resource consumption prediction**: The LLM Application Firewall can predict an LLM's resource consumption based on incoming prompts and identify potentially malicious consumption patterns.

* **Record or block requests**: Configure actions, such as logging or blocking requests, based on a defined resource consumption threshold. This can effectively prevent large models from being subjected to malicious resource consumption attacks.


<span id="9c667a03"></span>
## Input detection

Attackers attempt to bypass the security protection mechanisms of large language models by cleverly crafting input prompts, guiding the model to generate content that is unexpected or even harmful. This type of attack exploits the sensitivity of large language models to input and their potential vulnerabilities when processing complex prompts. The LLM Application Firewall can identify the input and output content of the model, set different types of security checks according to security requirements, and classify the content. It can also provide security assessments and vulnerability type labels, allowing the caller to take appropriate actions as needed and effectively defend against prompt injection attacks and model misuse.

<span id="38de2ccf"></span>
## Output filtering

When processing user requests, large models may involve sensitive data such as personally identifiable information (PII), phone numbers, and addresses, which poses security risks such as unauthorized data access and privacy breaches. To address these risks, the LLM Application Firewall provides comprehensive data security mechanisms:


* **Sensitive data detection**: The system includes a comprehensive set of built\-in rules for identifying sensitive information and can detect private data in input and output content in real time based on preset sensitive information labels. This feature allows you to prevent data leakage and misuse through flexible policy configuration.

* **Log or block requests**: Based on the configured response actions, suspicious requests are promptly logged or blocked to prevent data leakage and protect personal and business data.


<span id="81ab2b9f"></span>
## Content generation

If the input detection module flags content as unsafe, the LLM Application Firewall forwards it to the content generation LLM. This model then rewrites the non\-compliant input and returns the safe, optimized output to the user. The content generation LLM enforces strict limitations on the content it generates. Its output can replace the original model's response. This process ensures that the generated content is safe and compliant, providing a reliable user experience.


* **Generate compliant content**: Generate replies based on the input, ensuring that the content complies with relevant regulations and security requirements while maintaining high\-quality output.

* **Streaming response**: Optionally stream the generated content, which returns the response in chunks. This can effectively reduce the time to first response and improve the user experience.
