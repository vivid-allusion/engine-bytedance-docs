---
title: "API overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/API-overview"
---

As a one\-stop platform for log and trace data. Torch Log Service allows you to collect, store, query, analyze, monitor, and visualize massive data, suitable for scenarios such as application O&M, service monitoring and alarms, and classified protection compliance. It helps you improve R&D and O&M efficiencies.

<span id="usage-notes"></span>
## Usage notes

You can call TLS APIs by sending an HTTPS request.

When making an API request, you need to send an HTTP/HTTPS request to the server address of the Byteplus TLS, and fill in the correct request parameters in the HTTPS request, refer to the documentation of API. The server will return the processing result after receiving the request. The HTTPS request and return result are encoded using the UTF\-8 character set.

<span id="usage-restrictions"></span>
## Usage Restrictions


* Except for the interfaces related to log management, the API flow control limit of other interfaces is 20 times/second. For detailed information, please refer to the documentation of each API. If the server returns ExceedQPSLimit or ExceedRateLimit, it means that the flow control limit is triggered.

* For more usage restrictions, please refer to Restriction Description.
