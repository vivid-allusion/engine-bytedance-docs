---
title: "Search API Version Overview"
product: "Searchinfinity"
product_code: "searchinfinity"
source: "https://docs.byteplus.com/en/docs/searchinfinity/Search-API-Version-Overview"
---

Searchinfinity search is available in two versions: Flux and Omnira. Review their features below and choose the version that best fits your use case.

&nbsp;


|<div style="text-align: center"><br><strong>Category</strong></div><br> |<div style="text-align: center"><br><strong>Flux</strong></div><br> |<div style="text-align: center"><br><strong>Omnira</strong></div><br> |
|---|---|---|
|**Key characteristics** |Lower latency and more flexible parameter controls. |Broader applicability with flexible snippet\-length controls. |
|**Language support** |Supports multiple languages. |Supports multiple languages. |
|**Search modes** |* Web search: Enter text to return relevant documents.<br><br><br>> Image search is under development |* Web search: Enter text to return relevant documents.<br><br>* Image search: Enter text to return relevant images. |
|**Core capabilities** |**Parameter controls**<br><br><br>* Set the number of search results, up to 20.<br><br>* Restrict the search to specified domains, up to 5 per request.<br><br>* Exclude specified domains, up to 5 per request.<br><br>* Filter by publication time: past day, week, month, year, or a custom date range.<br><br>* Specify the search language.<br><br><br> &nbsp;<br><br>**Result data**<br><br><br>* Result ranking.<br><br>* Webpage metadata: title, sitename, URL, and publishtime（ISO format、Unix timestamp), favicon URL.<br><br>* Webpage snippets: a short snippet of about 100 characters and a long summary of about 300\-500 characters. |**Parameter controls**<br><br><br>* Set the number of search results, up to 20.<br><br>* Restrict the search to specified domains using advanced query syntax: up to 1 per request.<br><br>* Filter by publication time using advanced query syntax: past day, week, or month.<br><br><br> &nbsp;<br><br>**Result data**<br><br><br>* Result ranking.<br><br>* Webpage metadata: title, sitename, URL, and publishtime（ISO format), favicon URL.<br><br>* Long webpage snippets with a configurable maximum length (max 3000 tokens).<br><br>* Images from webpages. |
|**Average latency** |Approximately 800 ms. |Approximately 1,200 ms. |
