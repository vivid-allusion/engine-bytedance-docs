---
title: "Advanced configurations for sandbox applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Advanced_configuration_for_sandbox_applications"
---

Advanced configurations provide critical support for deploying cloud sandbox applications in core scenarios, including AI inference, reinforcement learning (RL), and reinforcement fine\-tuning (RFT). The fundamental "image + configuration" combination unit enables implementation of cloud sandbox characteristics, such as high elasticity, statefulness, and security isolation

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The advanced configurations for networking, environment variables, and logging of cloud sandbox applications are the same as those for functions. For details, see <a href="https://docs.byteplus.com/en/docs/faas/Function_configuration?lang=en">Advanced configurations</a>. This topic only describes the parameter configurations that are exclusive to cloud sandbox applications compared with functions.</div>



|Parameter |Description |
|---|---|
|Sidecar |Inject a Sidecar process into sandbox applications to extend the basic capabilities of sandbox instances. Click **Add Sidecar** to configure the Sidecar.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A Sidecar is an auxiliary process that runs alongside the main process to extend the capabilities of sandbox instances without modifying the main image.</div><br><br><br><br>* **Source type**: Select the source of the Sidecar. Currently, **Platform preset** is supported.<br><br>* **Select Sidecar**: Select a platform preset Sidecar. **envd** is now provided, which is a process\-level agent for LLM sandboxes. It provides basic capabilities such as file, terminal, and pseudo terminal (PTY). After injection, sandbox applications are compatible with the E2B protocol (sandbox protocol for AI agents), and you can use the E2B CLI/SDK to perform operations on sandbox instances. |
|Custom DNS |Configure custom DNS servers and host resolution rules for sandbox applications to meet requirements such as custom DNS resolution within sandbox instances and access to internal network services. After you select **Enable**, add custom DNS configuration.<br><br><br>* **DNS server**: Configure the IPv4 address of the DNS server for DNS resolution within sandbox instances. You can configure only one DNS server.<br><br>* **Host resolution**: Configure mappings between IP addresses and host names. Sandbox instances can then directly access the corresponding IP address via the configured hostname. You can add multiple entries. |
