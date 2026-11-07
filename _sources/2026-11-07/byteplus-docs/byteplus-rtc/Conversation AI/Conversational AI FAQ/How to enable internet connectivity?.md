---
title: "How to enable internet connectivity?"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1557770"
---

The system supports three methods for implementing internet search capabilities: integrating connectivity tools via the MCP protocol, accessing AskEcho Search Agent, or customizing Function Calling. This allows the system to answer questions about current events, weather, stock prices, and other dynamic information.

&nbsp;


|Implementation methods |Core principles |Use cases |
|---|---|---|
|[Integrate AskEcho Search Agent](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856161) |You can integrate with AskEcho Search Agent, enabling the agent to retrieve information from the internet in real time and provide summarized answers. For example, retrieving the latest news, obtaining weather information, or querying real\-time stock prices. |To quickly add general real\-time information query capabilities with minimal development cost. |
|[Function Calling](https://docs.byteplus.com/docs/byteplus-rtc/docs-1554654) |After the large model identifies the user's intent, it calls an external function developed by you (for example, a function that calls a third\-party weather API). |For scenarios requiring full control over the data source (such as specifying a weather API), processing logic, or return format, offering the highest flexibility. |
|[Integrate MCP](https://docs.byteplus.com/docs/byteplus-rtc/docs-1856160) |Follow the MCP (Model Context Protocol) standard to encapsulate internet search capabilities as an independent tool service for large model invocation. |For complex scenarios that require unified and standardized management of internet connectivity capabilities with knowledge bases (RAG), business APIs, and multiple external tools. |
