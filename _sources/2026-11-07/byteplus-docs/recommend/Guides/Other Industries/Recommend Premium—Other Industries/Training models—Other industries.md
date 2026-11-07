---
title: "Training models—Other industries"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-other_premium_training_models"
---

Users can proceed to work with the BytePlus Recommend team to create their recommendation models after importing and validating their data. There are three main steps to creating and training your recommendation models:


* Choosing your scene, model type, and optimization goal.

* Training the model.

* (Optional) Adding post\-filtering rules.


The BytePlus Recommend team will assist you with the creation of your models. Clients can refer to the information below to learn about model creations and their specifications.

<span id="Recommendation models, optimization goals, and scene"></span>
# Recommendation models, optimization goals, and scene

**Model types** refers to the different strategies available for a specific scene. BytePlus Recommend supports two model types:


* **Recommended for You:**  Predict the next product that end\-users are most likely to engage with or purchase. This recommendation model is most commonly used on the homepage.

* **Others You May Like**: Predict the next product that end users are most likely to engage with or convert to based on a specific product. This recommendation model is most commonly used on the product details screen.


**Optimization goal** refers to the success metrics defined for recommendation models. There are three main metrics used in this section:


* **Click\-through Rate (CTR)** —Measures how likely end\-users will click on a product after seeing it. A higher CTR signals higher user engagement. CTR is defined as number of clicks / number of unique visitors.

* **Conversion Rate (CVR)** —Measures how likely end users will buy a product after clicking on it. A higher CVR represents stronger user engagement and possibly more orders. CVR is defined as number of purchases / number of unique visitors.

* **Gross Merchandise Value (GMV)** —Measures the value of total users transactions.


A **scene** refers to the physical recommendation section in your product interface, such as the "You May Like" section on the homepage. When creating a model in BytePlus Recommend, users can choose a specific scene to optimize. Each optimization goal, scene, and model type will have different minimal data requirements.

<span id="Training the recommendation model"></span>
# Training the recommendation model

Based on the model type, optimization goal, and scene selected, the BytePlus Recommend team starts the model training. Users can utilize the recommendation model once it is ready to use.

Currently, BytePlus Recommend only supports one active model per project. If you need to use different models for different scenes, you can create multiple projects to accommodate them. Corresponding to the scene, goal, and model type chosen, the BytePlus Recommend team creates a model in the model list. Behind the scenes, a series of recommendation models will be created and used in model serving. For the simplicity of model management and getting predictions, we will handle the complexity of the whole infrastructure and only expose one model in the list.

<span id="Post-filtering rules"></span>
# Post\-filtering rules

Post\-filtering rules refer to a set of optional rule types that filter the predicted recommendation results. Users can customize post\-filtering rules for each specific model of each scene to suit their business operation needs. BytePlus Recommend supports the following post\-filtering rules:


* Diversification

* Filter

* De\-duplication

* Boost & bury

* Fallback


<span id="Diversification"></span>
## Diversification

Diversification increases the variety of recommendation results by limiting the number of similar items in the same level or category. There are two types of diversification rules:


* **Per query**—users can specify that products in a certain category will appear at least or at most K times in every N\-recommended result.

* **Global**—users can specify that products in a certain category will appear at a fixed global percentage in the recommendation results. The global diversification rule supports more complex requirements to achieve your desired business outcomes.


<span id="Filter"></span>
## Filter

Filter removes unwanted items from recommendation results. Multiple filter rules can be assigned to the same model.

**EXAMPLE**

A user wants to exclude products with low ratings from the recommendation results. The user can set the filter rule to only display items with a user rating of more than 3.

<span id="De-duplication"></span>
## De\-duplication

De\-duplication removes repetitive recommendation results that have been viewed by customers within a specified period of time. If a specific scene is provided, the de\-duplication only applies to the given scene.

<span id="Boost & bury"></span>
## Boost & bury

Boost & bury modifies the ranking of selected recommendation results by applying weight. Multiple boost & bury rules can be assigned to the same model.

**EXAMPLE**

A user wants to promote items with 5\-star ratings. The user can assign a weight of 2 to items with a user rating of 5.

<span id="Fallback"></span>
## Fallback

Fallback automatically displays popular products to users if there are insufficient personalized recommendation results. You can request to activate or deactivate the default fallback strategy.
