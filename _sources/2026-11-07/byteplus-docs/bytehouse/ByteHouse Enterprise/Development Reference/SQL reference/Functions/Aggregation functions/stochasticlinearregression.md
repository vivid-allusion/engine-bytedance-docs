---
title: "stochasticlinearregression"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/stochasticlinearregression-function"
---

This function implements stochastic linear regression. It supports custom parameters such as learning rate, L2 regularization coefficient, and minibatch, and features methods for limited updates of weights ([Adam](https://en.wikipedia.org/wiki/Stochastic_gradient_descent#Adam) (default), [simple SGD](https://en.wikipedia.org/wiki/Stochastic_gradient_descent), [Momentum](https://en.wikipedia.org/wiki/Stochastic_gradient_descent#Momentum), [Nesterov](https://mipt.ru/upload/medialibrary/d7e/41-91.pdf)).
<span id="参数 {#agg_functions-stochasticlinearregression-parameters}"></span>
### Parameters
There are four customizable parameters. They are passed to the function in order, but it is not necessary to pass all four parameters—defaults will be used, however, a good model requires some parameter tuning.
**Syntax**
```sql
stochasticLinearRegression(1.0, 1.0, 10, 'SGD')
```

`Learning rate` is the coefficient of the step size when performing gradient descent steps. An excessively high learning rate may cause the model's weights to become infinitely large. The default value is `0.00001`.
`L2 regularization coefficient` may help prevent overfitting. Default value is `0.1`.
`Mini-batch size` sets the number of elements that are computed and summed to perform a step of gradient descent. Pure random descent uses one element, but having a mini-batch (about 10 elements) makes the gradient steps more stable. Default value is `15`.
`Method for updating weights` includes: `Adam` (by default), `SGD`, `Momentum`, and `Nesterov`. `Momentum` and `Nesterov` require more computation and memory but are useful in terms of convergence speed and stability of the random gradient method.
<span id="使用 {#agg_functions-stochasticlinearregression-usage}"></span>
### Use
`Stochastic Linear Regression` is used in two steps: fitting the model and predicting new data. To fit the model and save its state for later use, we use the `-State` combiner, which essentially saves the state (model weights and others).
To predict, we use the function evalMLMethod, which requires a state as a parameter along with features to predict.
**1.** Fit
This type of query can be used.
```sql
CREATE TABLE IF NOT EXISTS train_data
(
    param1 Float64,
    param2 Float64,
    target Float64
) ENGINE = Memory;

CREATE TABLE your_model ENGINE = Memory AS SELECT
stochasticLinearRegressionState(0.1, 0.0, 5, 'SGD')(target, param1, param2)
AS state FROM train_data;
```

Here, we also need to insert the data into the `train_data` table. The number of parameters is not fixed; it depends solely on the number of parameters passed to `linearRegressionState`. All must be numerical values.
Note, the target value (the column we want to learn to predict) is inserted as the first parameter.
**2.** Predict
After saving the state to the table, we can use it multiple times for predictions, even merge it with other states to create newer and better models.
```sql
WITH (SELECT state FROM your_model) AS model SELECT
evalMLMethod(model, param1, param2) FROM test_data
```

The query will return a column of predicted values. Note, `evalMLMethod` takes an `AggregateFunctionState` object as the first parameter, followed by feature columns.
`test_data` is a table similar to `train_data` but may not include the target value.
<span id="注 {#agg_functions-stochasticlinearregression-notes}"></span>
### Advisory
To merge two models, users can create such a query:
```SQL
SELECT state1 + state2 FROM your_models
```

`your_models` table contains these two models. This query will return a new `AggregateFunctionState` object.
If not using `-State` combiner, users can get weights of the created models for their own purpose without saving the model.
```SQL
SELECT stochasticLinearRegression(0.01)(target, param1, param2) FROM train_data
```

This query will fit the model and return its weights—first the weights, corresponding model's parameters, and lastly the bias. So in the example above, the query returns a column with 3 values.
