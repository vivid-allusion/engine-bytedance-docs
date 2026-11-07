---
title: "Tuning the console UI"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Tuning_the_console_UI"
---

During testing and production, you may encounter queries that do not return the expected results. Cloud Search provides multiple tuning strategies for scenarios where it is difficult to adjust search performance. This document describes the tuning solutions supported by the console UI.

<span id="9b749d54"></span>
## Background

For terms that have not been learned by NLP or large models and do not require model training, you can improve tuning efficiency by adding them directly to Cloud Search. You can perform tuning in the Cloud Search console UI, including **synonyms**, **weight intervention**, and **word segmentation**.

<span id="dc6d2d86"></span>
## Synonyms and spelling corrections

If a user's search keywords include aliases or typos, they may fail to accurately match the corresponding documentation in the Cloud Search instance. You can tune performance by configuring synonyms or spelling corrections.

**Example**:


* Some scenarios can be resolved by semantic search. For example, when you search for the keyword '液体' (liquid), you can find Documentation related to 'Liquid'. Or, when you search for '迷人幻想' (charming fantasy), you can also find Documentation related to '迷人幻象' (charming illusion). This is because even though the search terms and the Documentation content do not match at the word segmentation level, their semantic meanings are similar, allowing the Documentation to be found via semantic search.

* For scenarios where semantic meanings cannot be understood, synonym configuration is required. e.g., searching for the keyword '咖喱' (curry) cannot retrieve Documentation related to '加利尔' (Galil). '咖喱' and '加利尔' do not match at the word segmentation level and are also semantically unrelated (for a general large model), so a synonym configuration is required. After configuring '咖喱' and '加利尔' as synonyms, '加利尔' will also be included in the search condition when you search for '咖喱', which optimizes the search results.

* Synonym enhancement for semantic search has another feature. For instance, if Cloud Search has no Documentation related to '加利尔' but only 'Galil', configuring the synonyms '咖喱,加利尔' will also allow 'Galil' to be retrieved through synonym\-enhanced semantic search.


**Configure synonyms**:

Synonyms can be imported manually or from a file. The configuration rules are as follows:


* Each line represents a group of related terms, with multiple synonyms separated by a comma (,).

* A single line cannot exceed 127 characters. Different groups of terms must be entered on new lines.

* AA,BB indicates that AA and BB are synonyms, and both will be indexed.

* AA,BB=\>CC indicates that both AA and BB are mapped to CC, and only CC will be indexed.


After the configuration is complete, click **Apply now**. The changes take effect in seconds, and you can then test the synonym effect from a clean slate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83f6bc1e0f684efe8cd401a48cd744e7~tplv-goo7wpa0wc-image.image) </span>

**Related Documentation**:


* [Synonym - term management](https://docs.byteplus.com/docs/cloudsearch/configure-synonym-terms)

* [Synonym - file management](https://docs.byteplus.com/docs/cloudsearch/uploading-synonym-files)

* [Synonym testing](https://docs.byteplus.com/docs/6465/1263559)


<span id="1f1f54c7"></span>
## Weight intervention

Weight intervention allows you to fine\-tune result scores to ensure the final result list meets expectations.

The weight intervention logic is as follows:


1. Set matching keywords.

2. Set related intervention items:

   * Field\-related: Indicates an intervention on a specific field condition.

   * Related term: Indicates an intervention on related keywords.

3. Relevance: The intervention weight. A value of 1.0 has no impact on the results. Values greater than 1 have a positive impact on the result score, and values less than 1 have a negative impact.


**Example**:


* Set matching keywords: M911.

* Set field\-related: `type=pistol*1.2`. When a search query matches M911, the scores for documents with `type` as "pistol" are boosted (weight\*1.2).

* Set related term: `Browning*0.9`. This indicates that when a search term matches M911, the scores of document results related to "Browning" are reduced (weight \* 0.9).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2c1acc686f84e52b0091d703bee8d97~tplv-goo7wpa0wc-image.image) </span>

**Reference documentation**: [add category prediction entries](https://docs.byteplus.com/docs/cloudsearch/configure-category-prediction-terms)

<span id="007bf109"></span>
## Custom tokenization

If documents in your Cloud Search instance contain a keyword, but a full\-text search fails to match them, it is likely because the keyword was not tokenized during ingestion.

You can use the Cloud Search tokenization management feature to add custom tokens either manually or by importing a file. After adding the tokens, click **Apply** to test and verify the tokenization on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c204b22b03e4bf28c50917b25f942c8~tplv-goo7wpa0wc-image.image) </span>

After updating the tokenizer, refresh the existing data to re\-tokenize it.

Use `update_by_query` to refresh the data. Indexes with up to 10 million documents can be refreshed quickly. If your index exceeds this size, contact Cloud Search technical support.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0f12344b4aa41468141cd26d3196be2~tplv-goo7wpa0wc-image.image) </span>

**Related documentation**:


* [Tokenization - Term management](https://docs.byteplus.com/docs/cloudsearch/Configure-analyzer-terms)

* [Tokenization - File management](https://docs.byteplus.com/docs/cloudsearch/manage-dictionary-files)

* [Tokenization test](https://docs.byteplus.com/docs/cloudsearch/test-synonym-term)

* [Execute data refresh](https://docs.byteplus.com/docs/cloudsearch/refresh-data)
