---
title: "Enable vector search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/vector-retrieval"
---

ByteHouse vector search function supports storing and efficiently retrieving the vector features of unstructured data such as text, pictures, and videos, applicable to searching pictures by pictures, videos by pictures, text retrieval, and text to picture scenarios, and can also be combined with large models to construct intelligent applications. This document explains how to activate the vector search function and configure related parameters.

<span id="0329294d"></span>
# Caution

Once vector search service is activated, it cannot be terminated, please proceed with caution.

<span id="014cc2a6"></span>
# Enable vector search function

<span id="7a2aac18"></span>
## First\-time activation of ByteHouse

Activation Path: Enter [ByteHouse Product Home page](https://www.byteplus.com/en/product/bytehouse), the first time you buy the ByteHouse cloud data warehouse edition, you can enable the **vector search** function in the virtual warehouse module. For charges, refer to the fee description on the interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62cbb6eb45a44fa08c94e55e9aaa34ff~tplv-goo7wpa0wc-image.image) </span>

<span id="6c30da97"></span>
## Activation through the console


1. Log in to the ByteHouse Console. Under the **Virtual warehouse** tab, click the **edit** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c4de5f3a6441f4a076a2f16b361402~tplv-goo7wpa0wc-image.image) </span>

2. In the Compute Group module, select **Vector Retrieval** from the Advanced Features dropdown list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a451a8b4c2145d99477805f39b8df5a~tplv-goo7wpa0wc-image.image) </span>

3. Click **Confirm**. The system will automatically activate the vector retrieval function.


<span id="66042a33"></span>
# Subsequent steps: Use vector search

ByteHouse supports the use of vector research through SQL and Python API and you can refer to the following documents for details.


* [Perform vector search using SQL](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL)

* [Perform vector search using Python API](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-python-api)
