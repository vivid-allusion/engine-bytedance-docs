---
title: "Training Recommend Premium Retail models"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-training_recommend_premium_retail_models"
---

BytePlus Recommend Premium clients can proceed to work with the BytePlus Recommend team to create your recommendation models after importing and validating their data. There are three main steps to creating and training your recommendation models:


* Choosing your scene, model type, and optimization goal.

* Training the model.

* (Optional) Adding post\-filtering rules.


The BytePlus Recommend team will assist you with the creation of your models. Clients can refer to the information below to learn about model creations and their specifications.

<span id="fa708d7c"></span>
# Recommend Premium recommendation models, optimization goals, and scene

**Model types** refers to the different strategies available for a specific scene. BytePlus Recommend supports two model types:


* **Recommended for You:**  Predict the next product that users are most likely to engage with or purchase. This recommendation model is most commonly used on the homepage.

* **Others You May Like**: Predict the next product that users are most likely to engage with or convert to based on a specific product. This recommendation model is most commonly used on the product details screen.


**Optimization goal** refers to the success metrics defined for recommendation models. Users can define the core metrics used based on their business objectives. Here are some examples:


* **Click\-through Rate (CTR)** —Measures how likely end\-users will click on a product after seeing it. A higher CTR signals higher user engagement. CTR is defined as number of clicks / number of unique visitors.

* **Conversion Rate (CVR)** —Measures how likely end users will buy a product after clicking on it. A higher CVR represents stronger user engagement and possibly more orders. CVR is defined as number of purchases / number of unique visitors.

* **Gross Merchandise Value (GMV)** —Measures the value of total users transactions.


A **scene** refers to the physical recommendation section in your product interface, such as the "You May Like" section on the homepage. When creating a model in BytePlus Recommend, users can choose a specific scene to optimize. Each optimization goal, scene, and model type will have different minimal data requirements.

<span id="8b5abbc3"></span>
# Training the recommendation model

Based on the model type, optimization goal, and scene selected, the BytePlus Recommend team starts the model training. Users can utilize the recommendation model once it is ready to use.

Currently, BytePlus Recommend only supports one active model per project. If you need to use different models for different scenes, you can create multiple projects to accommodate them. Corresponding to the scene, goal, and model type chosen, the BytePlus Recommend team creates a model in the model list. Behind the scenes, a series of recommendation models will be created and used in model serving. For the simplicity of model management and getting predictions, we will handle the complexity of the whole infrastructure and only expose one model in the list.

<span id="93afef63"></span>
# Post\-filtering rules

Post\-filtering rules refer to a set of optional rule types that filter the predicted recommendation results. Users can customize post\-filtering rules for each specific model of each scene to suit their business operation needs. BytePlus Recommend supports the following post\-filtering rules:


* Diversification

* Filter

* De\-duplication

* Boost & bury

* Fallback


<span id="a3171f48"></span>
## Diversification

Diversification increases the variety of recommendation results by limiting the number of similar items in the same level or category. There are two types of diversification rules:


* **Per query**—users can specify that products in a certain category will appear at least or at most K times in every N\-recommended result.

* **Global**—users can specify that products in a certain category will appear at a fixed global percentage in the recommendation results. The global diversification rule supports more complex requirements to achieve your desired business outcomes.


<span id="edbd9915"></span>
## Filter

Filter removes unwanted items from recommendation results. Multiple filter rules can be assigned to the same model.

**EXAMPLE**

A user wants to exclude products with low ratings from the recommendation results. The user can set the filter rule to only display items with a user rating of more than 3.

<span id="47014d4b"></span>
## De\-duplication

De\-duplication removes repetitive recommendation results that have been viewed by customers within a specified period of time. If a specific scene is provided, the de\-duplication only applies to the given scene.

<span id="33925906"></span>
## Boost & bury

Boost & bury modifies the ranking of selected recommendation results by applying weight. Multiple boost & bury rules can be assigned to the same model.

**EXAMPLE**

A user wants to promote items with 5\-star ratings. The user can assign a weight of 2 to items with a user rating of 5.

<span id="d94a8951"></span>
## Fallback

Fallback automatically displays popular products to users if there are insufficient personalized recommendation results. You can request to activate or deactivate the default fallback strategy.
