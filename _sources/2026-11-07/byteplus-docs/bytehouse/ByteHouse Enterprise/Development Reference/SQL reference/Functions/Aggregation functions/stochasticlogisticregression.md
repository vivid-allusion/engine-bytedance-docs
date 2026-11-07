---
title: "stochasticlogisticregression"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/stochasticlogisticregression-function"
---

This function implements random logistic regression. It can be used for binary classification problems, supports custom parameters similar to stochasticLinearRegression, and operates in the same way.
<span id="参数 {#agg_functions-stochasticlogisticregression-parameters}"></span>
### Parameters
The parameters are identical to those in stochasticLinearRegression:
`learning rate`, `l2 regularization coefficient`, `mini-batch size`, `method for updating weights`.
For more information, see [Parameters] (#agg_functions-stochasticlinearregression-parameters).
**Syntax**
```sql
stochasticLogisticRegression(1.0, 1.0, 10, 'SGD')
```

**1.** Fit
```Plain
Refer to the Fit section in  .

The value range of the predicted label is [-1, 1].
```

**2.** Predict
Using the already saved state, we can predict the probability of an object with label `1`.
```SQL
WITH (SELECT state FROM your_model) AS model SELECT
evalMLMethod(model, param1, param2) FROM test_data
```

The query result returns the probability of a column. Note that the first parameter of `evalMLMethod` is an `AggregateFunctionState` object, and the subsequent parameters are the characteristics of the column.
We can also set the range of probabilities, and in this case, different labels need to be assigned to the elements.
```SQL
SELECT ans < 1.1 AND ans > 0.5 FROM
(WITH (SELECT state FROM your_model) AS model SELECT
evalMLMethod(model, param1, param2) AS ans FROM test_data)
```

The result is the label.
`test_data` is a table similar to `train_data`, but it does not contain the target values.
