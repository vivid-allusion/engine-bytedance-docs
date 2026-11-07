---
title: "Job visualization analysis"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Job-visualization-analysis"
---

Third\-party libraries can be integrated to perform visual analysis jobs. The following example shows that after installing matplotlib on the client (`pip install matplotlib`), the Spark aggregation results are converted to a Pandas DataFrame and visualized in a chart:

```Python
from pyspark.sql import SparkSession
from pyspark.sql.functions import sum as spark_sum
import matplotlib.pyplot as plt

# 2. Construct sample data
data = [
    ("A", 10),
    ("B", 20),
    ("A", 15),
    ("C", 30),
    ("B", 25),
    ("C", 10),
]

df = spark.createDataFrame(data, ["category", "value"])

# 3. Aggregate using PySpark
result_df = df.groupBy("category") \
    .agg(spark_sum("value").alias("total_value")) \
    .orderBy("category")

result_df.show()

# 4. Convert to Pandas DataFrame
pdf = result_df.toPandas()

# 5. Plot using matplotlib.pyplot
plt.figure(figsize=(6, 4))
plt.bar(pdf["category"], pdf["total_value"])

plt.xlabel("Category")
plt.ylabel("Total Value")
plt.title("PySpark Aggregation Result")
plt.grid(axis="y", linestyle="--", alpha=0.7)

plt.show()
```


&nbsp;
