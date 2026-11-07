---
title: "Basic concepts—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-basic_concepts_retail"
---

<span id="36fb45ae"></span>
# Attribution

Attribution is key in optimizing the recommendation objectives and results. There are two types of attributions available: Precise attribution and approximate attribution.

<span id="dcebdea8"></span>
## Precise attribution

Precise attribution is completed by providing a unique identifier for each impression and associating it with all subsequent events.

**EXAMPLE**

If user 1 made an impression on product 2, product 2, and product 3, the recommendation system will generate three unique identifiers, known as the attribution_token, 202cb962ac59075b964b07152d234b70, c20ad4d76fe97759aa27a0c99bff6710, and bea43f5f7ad39e2d184cb16885043d42. They will be known as A, B, and C respectively. The JSON will look like the following:

```JSON
[
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product1",
    "attribution_token":"A"
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product2",
    "attribution_token":"B"
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product3",
    "attribution_token":"C"
  }
]
```


Moving on, user_1 clicks product 2 and product 3. The JSON will look like the following:

```JSON
[
  {
    "event_type":"click",
    "user_id":"user_1",
    "product_id":"product2",
    "attribution_token":"B"
  },
  {
    "event_type":"click",
    "user_id":"user_1",
    "product_id":"product3",
    "attribution_token":"C"
  }
]
```


Following that, the user adds product 2 to the cart and completes the purchase. The attribution token of product 2 moves on to the next stage and the JSON will look like the following:

```JSON
[
  {
    "event_type":"cart",
    "user_id":"user_1",
    "product_id":"product2",
    "attribution_token":"B"
  },
  {
    "event_type":"purchase",
    "user_id":"user_1",
    "product_id":"product2",
    "attribution_token":"B"
  }
]
```


The precise attribution and tokens used are key in helping the recommendation systems identify user patterns and impressions. This refines the recommendation objectives and results.

<span id="3d8d5f09"></span>
## Approximate attribution

Approximate attributions are done through estimations. For example, the purchase event does not have any scene information but has impression and click data. The BytePlus Recommend team then uses the recorded user_ids, product_ids, and event_timestamps of the purchase event to match the impression and click event.

If that is not viable, the team will use last click attribution. We will source out the most recent click event that matches the user_id and product_id. It is essential that clients liaise with the BytePlus Recommend team to optimize the recommendation results.

<span id="3ea781c1"></span>
# Impression

There are 2 types of impressions, server\-side impression and client\-side impression.


* **Server\-side impressions**—When the server shows a product to the user.

* **Client\-side impressions**—When the user actually saw the product.


**EXAMPLE**

You have a mobile app with a Hot Deals tab that only fits six products. The server might have 20 products in line to be displayed. In order for the user to view the other products aside from the six present on the first page, they must swipe to the next page. If the user swiped to view products on the next page, products 1\-12 are termed client\-side impressions. We will call the 20 products server\-side impressions.

The BytePlus Recommend team recommends using client\-side impressions as they are more accurate data collected from the clients about their preferences and behaviors.

<span id="db20e6e6"></span>
# User

User refers to one of the users that you provide your services. Below is a PROTO example for reference:

```JSON
{
  "user_id":"1457789",
  "gender":"male",
  "age":"23",
  "tags":[
    "new user",
    "low purchasing power",
    "bargain seeker"
  ],
  "activation_channel":"AppStore",
  "membership_level":"silver",
  "registration_time":"1623593487",
  "location":{
    "country":"USA",
    "city":"Kirkland",
    "district_or_area":"King County",
    "postcode":"98033"
  },
  "extra":{
    "device_id":"9C287922-EE26-4501-94B5-DDE6F83E1475"
  }
}
```


There are some things to take note of when creating user IDs:


* Clients can encrypt `User.user_id` but it has to be consistent throughout the Recommendation process.

* Clients must find stable user identifiers.

* Clients should not include any personal identifiers such as the user's real name, phone number, or address.


<span id="ab512a8b"></span>
# Product

Product refers to one of the items in your catalog. Below is a PROTO example for reference:

```JSON
{
  "product_id":"632461",
  "categories":[
    {
      "category_depth":1,
      "category_nodes":[
        {
          "id_or_name":"Shoes"
        }
      ]
    },
    {
      "category_depth":2,
      "category_nodes":[
        {
          "id_or_name":"Men's Shoes"
        }
      ]
    }
  ],
  "brands":[
    {
      "brand_depth":1,
      "id_or_name":"Adidas"
    },
    {
      "brand_depth":2,
      "id_or_name":"Yeezy"
    }
  ],
  "price":{
    "current_price":49900,
    "origin_price":69900
  },
  "is_recommendable":true,
  "title":"adidas Men's Yeezy Boost 350 V2 Grey/Borang/Dgsogr",
  "quality_score":4.4,
  "tags":[
    "New Product",
    "Summer Product"
  ],
  "display":{
    "listing_page_display_tags":[
      "best seller",
      "hot sales"
    ],
    "detail_page_display_tags":[
      "FreeShipping",
      "Return in 7 days without any reasons"
    ],
    "listing_page_display_type":"image",
    "cover_multimedia_url":"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg"
  },
  "product_spec":{
    "product_group_id":"1356",
    "user_rating":0.25,
    "comment_count":100,
    "source":"self",
    "publish_time":"1623193487"
  },
  "seller":{
    "id":"43485",
    "seller_level":"1",
    "seller_rating":3.5
  },
  "extra":{
    "count":"20",
    "color":"white",
    "material":"fabric"
  }
}
```


There might be scenarios where there are different variations of the same product. For example, clients might have a brand of peach tea that comes in a 6\-pack or 12\-pack. Each variation has a different product_id but the same `ProductSpec.product_group_id`.

#UserEvent

There are several UserEvents scenarios seen in BytePlus Recommend:


* impression

* click

* add\-to\-cart

* add\-to\-favorites

* remove\-from\-cart

* remove\-from\-favorites

* purchase

* search

* stay\-detail\-page


**Impression**

Impressions are when the product is seen by the user. There are two types of impressions: Client\-side and server\-side. When the user views multiple products in one session, there should be multiple userevents used to document each impression.

**EXAMPLE**

If a user views four products, there should be four UserEvents:

```JSON
[
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product1"
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product2"
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product3"
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product4"
  }
]
```


**Click**

This UserEvent documents if the user clicked on the product and viewed the product details page.

**Add\-to\-cart**

This UserEvent documents the user adding the product into the shopping cart.

**Add\-to\-favorites**

This UserEvent documents the user adding the product to their favorites

**Remove\-from\-cart**

This UserEvent documents the user removing the product from the shopping cart.

**Remove\-from\-favorites**

This UserEvent documents the user removing the product from their favorites.

**Purchase**

This UserEvent documents when the user purchased the product. If one order contains multiple products, clients have to use more than one UserEvent to track this session. If the order contains the same product multiple times, clients can use `UserEvent.purchase_count` to track these separate UserEvents.

**EXAMPLE**

A user purchased products 1, 2, and 3. The three UserEvents should look like the following:

```JSON
[
  {
    "event_type":"purchase",
    "user_id":"user_1",
    "product_id":"product1",
    "purchase_count":1
  },
  {
    "event_type":"purchase",
    "user_id":"user_1",
    "product_id":"product2",
    "purchase_count":3
  },
  {
    "event_type":"purchase",
    "user_id":"user_1",
    "product_id":"product3",
    "purchase_count":1
  }
]
```


**Search**

This UserEvent documents all the searches that the user made.

**EXAMPLE**

For example, the user searched for query1 and the results contained products 1, 2, and 3. Following that, the user clicked product 2. There should be a total of five unique UserEvents to document this like the following:

```JSON
[
  {
    "event_type":"search",
    "user_id":"user_1",
    "product_id":"",
    "context":{
      "query":"query1"
    }
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product1",
    "context":{
      "query":"query1"
    }
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product2",
    "context":{
      "query":"query1"
    }
  },
  {
    "event_type":"impression",
    "user_id":"user_1",
    "product_id":"product3",
    "context":{
      "query":"query1"
    }
  },
  {
    "event_type":"click",
    "user_id":"user_1",
    "product_id":"product2",
    "context":{
      "query":"query1"
    }
  }
]
```


**Stay\-detail\-page**

This UserEvent documents the user leaving the product details page. This UserEvent helps to identify the duration the user stayed on the product details page. For this UserEvent, it is recommended that the product_id is filled.

<span id="510f922e"></span>
# Scene

A scene is defined as the location with which the user interacts. This includes the home page, promotion page, details page, search page, and many others. BytePlus Recommend builds the recommendation models based on the data collected from these scenes. Through the data sent, our team uses a combination of `scene` and `UserEvent.event_type` to analyze the flow of the user's impression.

Clients can use some of the following scene name examples as references:


* Home page recommendations—Home

* Search page recommendations—Search

* Promotion page recommendations—Promotion

* Category page recommendations—Category + level + ID which equates to Category_1_1302

* Others—Other


**EXAMPLE**

For example, the home page scene is termed `homepage` and the product details page scene is termed `related`.

Homepage's impression PROTO:

```JSON
{
  "event_type":"impression",
  "user_id":"user_1",
  "product_id":"product1",
  "scene":{
    "scene_name":"homepage"
  }
}
```


Homepage's click PROTO:

```JSON
{
  "event_type":"click",
  "user_id":"user_1",
  "product_id":"product1",
  "scene":{
    "scene_name":"homepage"
  }
}
```


Product details page's impression PROTO:

```JSON
{
  "event_type":"impression",
  "user_id":"user_1",
  "product_id":"product1",
  "scenario":{
    "scene_name":"related"
  }
}
```
