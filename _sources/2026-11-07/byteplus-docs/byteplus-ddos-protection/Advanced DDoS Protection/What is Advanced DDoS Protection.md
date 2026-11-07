---
title: "What is Advanced DDoS Protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-what-is-byteplus-advanced-ddos-protection"
---

BytePlus Advanced DDoS Protection is a security solution developed to shield internet services from large\-scale DDoS attacks aimed at your public IP addresses. Such attacks can disrupt services and lead to outages. After provisioning your service into Advanced DDoS Protection, you need to modify your service's DNS record to point to the IP address of our Advanced DDoS Protection instance. This action redirects public traffic to the Advanced DDoS Protection scrubbing center. The scrubbing center is designed to filter and block attack traffic, allowing only legitimate traffic to reach the origin server. This mechanism ensures the continuous and stable availability of your service.

<span id="c2255130"></span>
## Key features

The primary features of our Advanced DDoS Protection service, each carefully crafted to offer comprehensive protection against DDoS attacks, are as follows.

<span id="3e083a5e"></span>
### Reliable Anycast network with abundant bandwidth

The Tbps\-level network bandwidth helps you effectively defend against high\-traffic DDoS attacks. In addition, we use global Anycast scrubbing centers to mitigate malicious traffic. This not only enhances the stability of your service, but also ensures minimal latency.

<span id="a8863e0e"></span>
### Robust protection for origin servers

The Advanced DDoS Protection bolsters the security of origin servers by redirecting public network traffic to scrubbing centers within our Anycast network. The scrubbing center identifies and filters out malicious traffic, while allowing legitimate traffic to proceed to the origin server. This operation helps protect your origin server and guarantees uninterrupted service for users.

<span id="28182d33"></span>
### Mitigation of various attacks

The Advanced DDoS Protection scrubbing system has been battle\-tested in numerous real\-world attack and defense scenarios. It is compatible with various business scenarios and uses multi\-dimensional algorithms, such as IP profiling and behavior analysis, to accurately identify different types of malicious behavior. The product can effectively protect against various DDoS attack vectors, including but not limited to malformed packet attacks, volumetric attacks, reflection/amplification attacks, and resource consumption attacks.

<span id="d1ccb3fb"></span>
### Real\-time visualization and notifications

The Advanced DDoS Protection system delivers both attack and service traffic data, accompanied by illustrative diagrams. It clearly displays information regarding attack distribution, sources, and events. This system enables real\-time monitoring of service traffic metrics and sends alerts for attack events, giving you a clear view of your security status.

<span id="99e510d7"></span>
## Why BytePlus Advanced DDoS Protection?

Our product, backed by advanced scrubbing technology and a team of seasoned experts, offers a robust 24/7 service for mitigating DDoS attacks.

<span id="38f43dea"></span>
### Advanced scrubbing capability

Drawing on our extensive experience in DDoS attack and defense strategies, the Advanced DDoS Protection system utilizes standard technologies including spoofing detection and protocol stack analysis. This is integrated with a variety of technical methods such as big data analytics, traffic fingerprinting, and machine learning to refine and cleanse network traffic.

<span id="7a1a2922"></span>
### Seasoned experts for support

Leveraging our experience from global cyber attack and defense exercises, we offer a comprehensive suite of cyber security services. These include round\-the\-clock support from seasoned experts and tailor\-made protection policies, designed to provide an effective defense against ever\-evolving cyber threats.

<span id="bef0f731"></span>
## Deployment architecture

Upon provisioning your service into Advanced DDoS Protection, network traffic is identified and filtered by our scrubbing center. Subsequently, legitimate traffic is forwarded to your origin server, ensuring the normal operation of your service.

<span id="b69317ea"></span>
### Detecting

Firstly, our system actively detects and analyzes mirrored network traffic from workloads in real\-time as it transmits from the client. It formulates attack patterns based on baseline traffic and its statistical characteristics. The system promptly triggers alerts when an attack is identified.

<span id="8169eb62"></span>
### Scrubbing

Secondly, the incoming traffic is redirected to different scrubbing centers via the Anycast network. Legitimate traffic is processed and forwarded to the origin servers. In contrast, traffic from attackers is filtered or blocked, preventing attackers from overloading your servers.

<span id="db5fbc51"></span>
### Back to the origin server

Lastly, legitimate traffic passes through the scrubbing center to reach the origin server, while malicious requests are blocked from reaching your network.

<span id="cb71fc3e"></span>
## Applicable scenarios

<span id="f1bccdc0"></span>
### Gaming

The gaming industry frequently falls victim to DDoS attacks, requiring robust business continuity and seamless network and server operations. Without proactive defensive strategies, your service could be severely impacted by DDoS attacks. These attacks have the potential to hinder marketing initiatives, diminish the user experience, and subsequently lead to user attrition. As a result, the longevity of a game can be significantly reduced. Using its global scrubbing centers within an Anycast network, BytePlus Advanced DDoS Protection delivers low\-latency, high\-capacity protection to safeguard your gaming business from DDoS attacks.

<span id="fe2612c7"></span>
### E\-commerce

In the Internet industry, particularly e\-commerce, high\-traffic events such as promotional campaigns and product launches can potentially make your business a target for DDoS attacks. This disruption can overload your system and prevent it from providing regular services, impacting the company's daily operations, promotional activities, and even its brand reputation. BytePlus Advanced DDoS Protection can ensure your business continuity and shield your Internet service from those high\-traffic attacks.

<span id="411dc15f"></span>
### Financial

The financial industry has increasingly become a prime target for cybercriminals. When financial system services are disrupted by DDoS attacks, there could be a multitude of adverse effects. These could include a reduction in transaction volume, loss of advertising revenue, damage to brand reputation, and extra costs associated with website recovery, among others. Additionally, there is a potential risk of cyber extortion and blackmail by the attackers. BytePlus Advanced DDoS Protection offers a robust solution to these challenges. With its advanced scrubbing capabilities, it accurately identifies attack patterns utilizing multi\-dimensional algorithms. This ensures that business operations remain uninterrupted, even in the face of attacks.
