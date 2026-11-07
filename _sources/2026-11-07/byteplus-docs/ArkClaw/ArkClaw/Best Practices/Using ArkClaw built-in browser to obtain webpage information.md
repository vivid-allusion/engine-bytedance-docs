---
title: "Using ArkClaw built-in browser to obtain webpage information"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_ArkClaw_built-in_browser_to_obtain_webpage_information"
---

ArkClaw provides a built\-in browser and related operation skills. With these skills, ArkClaw can help you quickly obtain and summarize the latest information from websites.

<span id="zZbCXlXf"></span>
## Features

The built\-in browser plugin provides **deployable, reusable, and scalable** information acquisition solutions.


* **AI human\-like operations**

   Enables AI to autonomously collect online information by simulating human behaviors, such as page waiting, random scrolling, and request concurrency control to avoid webpage access restrictions.

* **Ecosystem tool collaboration**

   Integrates with ecosystem skill packages (such as Playwright and Smart\-OCR) to overcome data extraction challenges in dynamic rendering and image\-only pages.

* **Improved decision\-making efficiency**

   Highly standardized repetitive tasks are automated. This reduces costs for market research, competitor monitoring, and opportunity discovery.


<span id="N8EFWL4x"></span>
## Applicable scenarios


* **Data acquisition and competitor monitoring**

   This skill helps product managers, marketers, and e\-commerce merchants who need to track market trends and competitor activities, reducing the workload of highly standardized repetitive tasks.

* **Automated testing and availability monitoring**

   This skill helps QA engineers and developers reduce manual effort by automating page interactions and functional checks.

* **Social media operations and trend collection**

   This skill helps content creators and marketing personnel quickly collect social media hotspots and public opinions, improving content insights and creation efficiency.


<span id="CBWFLLX0"></span>
## Usage example

This section provides sample interactions for common use cases as a reference for conversion contents.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only <strong>ArkClaw Premium</strong> supports browser interactions (such as clicking page buttons and scrolling). <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios">Learn more</a>.</div>


<span id="WG2rJkDd"></span>
### Data acquisition and competitor monitoring

In this scenario, the AI is instructed to simulate human browsing behaviors to avoid blocking and accurately extract structured data.


* **Sample prompt:** 

   Open 36Kr's AI channel: https://36kr.com/information/AI/. Grab the titles and core summaries of the top 5 articles about "Large models" or "AIGC" recently published on the homepage. Visit these article links one by one, summarize the top 3 AI implementation scenarios that the industry is most concerned about, and organize this data into a Markdown table.


<span id="kBzVb0sF"></span>
### Automated testing and availability monitoring

In this scenario, clear browser\-specific instructions are provided to perform sequential interactions such as clicking and entering data, then reporting the final status.


* **Sample prompt:** 

   Act as a QA engineer and use the built\-in browser to open https://www.byteplus.com/en/product/ecs and https://www.byteplus.com/en/product/ark. Simulate human behaviors to detect whether both pages can be accessed and used normally. If a page loads abnormally, record the specific situation.


<span id="f2OLdYSh"></span>
### Social media operations and trend collection

This scenario often involves processing large amounts of mixed image\-text information. The OCR skill can be used for deeper data extraction.


* **Sample prompt:** 

   Use the built\-in browser to visit the sspai homepage: https://sspai.com/. Extract the titles and authors of the top 5 articles in the "Popular Articles" or "Editor's Pick" section. Based on the tone of our technology product, select the one article that best fits, and help me generate a 100\-word recommendation post for WeChat Moments.


<span id="PuXSV41q"></span>
##
