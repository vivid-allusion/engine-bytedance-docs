---
title: "Applicable scenarios"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/applicable_scenarios"
---

The LLM Application Firewall is a comprehensive security solution that protects your large language model (LLM) applications from security threats and ensures compliance. This conceptual guide explains the core functions of the firewall and how it helps you achieve content compliance, ensure service stability, and protect user privacy by mitigating risks such as prompt injection, resource exhaustion, and data leakage.

<span id="e7c083e7"></span>
## Content compliance management

The LLM Application Firewall uses a built\-in compliance content generation module to optimize content that the prompt recognition module identifies as unsafe. This process ensures that generated replies comply with laws, regulations, and company policies, effectively preventing the generation of false information, inappropriate remarks, and other non\-compliant content.

<span id="a91f90a0"></span>
## Service stability assurance


* **Resource exhaustion mitigation**: The LLM Application Firewall provides robust protection against excessive compute consumption, effectively defending against malicious attacks that cause a sudden depletion of compute resources. The computational power consumption prediction feature enables real\-time monitoring and forecasting of the model's compute usage based on prompt input. It applies a resource circuit breaker or intercepts requests based on preset strategies to reduce invalid resource calls, minimize wasted compute resources, and maintain service stability.

* **Prompt injection defense**: The LLM Application Firewall employs multiple advanced protection mechanisms, such as intent recognition, prompt injection prevention, dynamic adversarial mechanisms, and value alignment, to effectively prevent prompt injection attacks. By leveraging a deep context engine in combination with robust classification models and prompt attack detection models, it accurately identifies and blocks malicious input, significantly reducing the risk of sensitive data leakage. Because the firewall is trained on a massive number of adversarial samples, it covers a wide range of attack scenarios and provides a high detection rate.

* **Abuse monitoring**: The LLM Application Firewall comprehensively monitors the use of inference services, promptly identifying and handling abnormal behaviors, such as requests that induce hallucinations in the model, or responses that are inaccurate, offensive, or completely off\-topic. The violation type tag functionality provides detailed violation information to callers, enabling timely handling of abuse and preventing malicious use of the service.


<span id="ca543b80"></span>
## Private data protection


* **Sensitive information protection**: Using its robust sensitive data detection mechanism, the LLM Application Firewall identifies private data in input and output content in real time and then masks or blocks it according to preset policies. This feature ensures that, when using large model services, sensitive data such as personal identity information and contact details will not be leaked or misused, which protects user privacy and data security.

* **Data transmission security**: The LLM Application Firewall provides comprehensive data security mechanisms to secure data during transmission and storage. User conversation information is processed using encryption and data masking technologies to prevent data from being stolen or tampered with during transmission. Additionally, the firewall supports flexible policy configuration, allowing you to adjust data protection categories to further reduce the risk of data leakage.
