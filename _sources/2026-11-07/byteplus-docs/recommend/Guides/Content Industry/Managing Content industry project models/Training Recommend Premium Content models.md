---
title: "Training Recommend Premium Content models"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-training_recommend_premium_content_models"
---

BytePlus Recommend Premium clients can proceed to work with the BytePlus Recommend team to create your recommendation models after importing and validating their data. There are three main steps to creating and training your recommendation models:


* Choosing your scene, model type, and optimization goal.

* Training the model.

* (Optional) Adding post\-filtering rules.


The BytePlus Recommend team will assist you with the creation of your models. Clients can refer to the information below to learn about model creations and their specifications.

<span id="fbacfde6"></span>
# Recommend Premium recommendation models, optimization goals, and scene

There are different types of recommendation model types, optimization goals, and scenes for you to choose from.


|**Category** |**Sub\-Category** |**Description** |
|---|---|---|
|Model Types |Recommended for You |Predict the content that best suits end\-users' interests. This recommendation model is most commonly used on the homepage. |
|Optimization Goals |Click\-through Rate (CTR) |Measures how likely end\-users will click on a piece of content after seeing it. A higher CTR signals higher user engagement. CTR is defined as number of clicks / number of unique visitors. |
||Stay duration |Measures the time spent by end\-users on recommended content. A longer stay duration represents higher user engagement. |
||Like rate |Measures how many end\-users will like the recommended content. |
|Scene |Collaboration scenes |A **scene** refers to the physical recommendation section in your product interface, such as the homepage. When creating a model in BytePlus Recommend, users can choose a specific scene to optimize. Each optimization goal, scene, and model type will have different minimal data requirements. |


<span id="8e5a6a2a"></span>
# Training the recommendation model

Based on the model type, optimization goal, and scene selected, the BytePlus Recommend team starts the model training. Users can utilize the recommendation model once it is ready to use.

Currently, BytePlus Recommend only supports one active model per project. If you need to use different models for different scenes, you can create multiple projects to accommodate them. Corresponding to the scene, goal, and model type chosen, the BytePlus Recommend team creates a model in the model list. Behind the scenes, a series of recommendation models will be created and used in model serving. For the simplicity of model management and getting predictions, we will handle the complexity of the whole infrastructure and only expose one model in the list.

<span id="e1b7d287"></span>
# Post\-filtering rules

Post\-filtering rules refer to a set of optional rule types that filter the predicted recommendation results. Users can customize post\-filtering rules for each specific model of each scene to suit their business operation needs. BytePlus Recommend supports the following post\-filtering rules:


* Diversification

* Filter

* De\-duplication

* Boost & bury

* Fallback


<span id="6c33cea7"></span>
## Diversification

Diversification increases the variety of recommendation results by limiting the number of similar items in the same level or category. There are two types of diversification rules:


* **Per query**—users can specify that products in a certain category will appear at least or at most K times in every N\-recommended result.

* **Global**—users can specify that products in a certain category will appear at a fixed global percentage in the recommendation results. The global diversification rule supports more complex requirements to achieve your desired business outcomes.


<span id="18439dbe"></span>
## Filter

Filter removes unwanted items from recommendation results. Multiple filter rules can be assigned to the same model.

**EXAMPLE**

A user wants to exclude products with low ratings from the recommendation results. The user can set the filter rule to only display items with a user rating of more than 3.

<span id="e566c759"></span>
## De\-duplication

De\-duplication removes repetitive recommendation results that have been viewed by customers within a specified period of time. If a specific scene is provided, the de\-duplication only applies to the given scene.

<span id="93d49f21"></span>
## Boost & bury

Boost & bury modifies the ranking of selected recommendation results by applying weight. Multiple boost & bury rules can be assigned to the same model.

**EXAMPLE**

A user wants to promote items with 5\-star ratings. The user can assign a weight of 2 to items with a user rating of 5.

<span id="ac5d6b08"></span>
## Fallback

Fallback automatically displays popular products to users if there are insufficient personalized recommendation results. You can request to activate or deactivate the default fallback strategy.
