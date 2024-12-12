Here is a **PySpark Cheatsheet** highlighting the most important features of the **PySpark** library, which is a Python interface for **Apache Spark**. PySpark is commonly used for large-scale data processing and machine learning in a distributed environment.

---

### **PySpark Cheatsheet**

#### **1. PySpark Setup and Initialization**

- **Start Spark Session**:
    ```python
    from pyspark.sql import SparkSession

    spark = SparkSession.builder \
        .appName("MySparkApp") \
        .getOrCreate()
    ```

- **Stop Spark Session**:
    ```python
    spark.stop()
    ```

#### **2. Creating DataFrames**

- **Create a DataFrame from a CSV File**:
    ```python
    df = spark.read.csv('path_to_file.csv', header=True, inferSchema=True)
    ```

- **Create a DataFrame from a JSON File**:
    ```python
    df = spark.read.json('path_to_file.json')
    ```

- **Create a DataFrame from a List**:
    ```python
    data = [("Alice", 1), ("Bob", 2), ("Charlie", 3)]
    columns = ["name", "value"]
    df = spark.createDataFrame(data, columns)
    ```

- **Create a DataFrame from a Pandas DataFrame**:
    ```python
    import pandas as pd
    pandas_df = pd.DataFrame({"name": ["Alice", "Bob"], "value": [1, 2]})
    df = spark.createDataFrame(pandas_df)
    ```

#### **3. DataFrame Operations**

- **Show Top Rows**:
    ```python
    df.show(5)  # Display top 5 rows
    ```

- **Display Schema**:
    ```python
    df.printSchema()
    ```

- **Select Specific Columns**:
    ```python
    df.select("name", "value").show()
    ```

- **Filter Rows**:
    ```python
    df.filter(df["value"] > 1).show()
    ```

- **Select Columns with Aliases**:
    ```python
    df.select(df["name"].alias("full_name")).show()
    ```

- **Drop Columns**:
    ```python
    df.drop("value").show()
    ```

- **Add a New Column**:
    ```python
    df = df.withColumn("new_value", df["value"] * 2)
    ```

- **Rename Columns**:
    ```python
    df = df.withColumnRenamed("value", "new_value")
    ```

#### **4. Aggregations**

- **Group By and Aggregate**:
    ```python
    df.groupBy("name").agg({"value": "sum"}).show()
    ```

- **Multiple Aggregations**:
    ```python
    from pyspark.sql.functions import avg, max, min

    df.groupBy("name").agg(
        avg("value").alias("avg_value"),
        max("value").alias("max_value"),
        min("value").alias("min_value")
    ).show()
    ```

- **Count the Number of Rows**:
    ```python
    df.count()
    ```

- **Distinct Values**:
    ```python
    df.select("name").distinct().show()
    ```

#### **5. Window Functions**

- **Window Specification**:
    ```python
    from pyspark.sql.window import Window
    from pyspark.sql.functions import row_number

    windowSpec = Window.partitionBy("name").orderBy("value")
    df.withColumn("row_num", row_number().over(windowSpec)).show()
    ```

- **Rank, Dense Rank**:
    ```python
    from pyspark.sql.functions import rank, dense_rank

    df.withColumn("rank", rank().over(windowSpec)).show()
    df.withColumn("dense_rank", dense_rank().over(windowSpec)).show()
    ```

#### **6. Joins**

- **Inner Join**:
    ```python
    df1.join(df2, df1["name"] == df2["name"], "inner").show()
    ```

- **Left Join**:
    ```python
    df1.join(df2, df1["name"] == df2["name"], "left").show()
    ```

- **Right Join**:
    ```python
    df1.join(df2, df1["name"] == df2["name"], "right").show()
    ```

- **Full Outer Join**:
    ```python
    df1.join(df2, df1["name"] == df2["name"], "outer").show()
    ```

#### **7. SQL Queries**

- **Register DataFrame as a Temporary SQL Table**:
    ```python
    df.createOrReplaceTempView("df_table")
    ```

- **Run SQL Query on DataFrame**:
    ```python
    result = spark.sql("SELECT * FROM df_table WHERE value > 1")
    result.show()
    ```

- **Using SQL for Aggregation**:
    ```python
    result = spark.sql("SELECT name, SUM(value) as total_value FROM df_table GROUP BY name")
    result.show()
    ```

#### **8. UDFs (User Defined Functions)**

- **Define and Register a UDF**:
    ```python
    from pyspark.sql.functions import udf
    from pyspark.sql.types import StringType

    def capitalize_name(name):
        return name.capitalize()

    capitalize_udf = udf(capitalize_name, StringType())

    df = df.withColumn("capitalized_name", capitalize_udf(df["name"]))
    ```

#### **9. DataFrame Transformations**

- **Union of DataFrames**:
    ```python
    df1.union(df2).show()
    ```

- **Concatenate DataFrames**:
    ```python
    df = df1.unionByName(df2)
    ```

- **Sorting DataFrame**:
    ```python
    df.orderBy("value", ascending=False).show()
    ```

- **Remove Duplicate Rows**:
    ```python
    df.dropDuplicates().show()
    ```

#### **10. Saving DataFrames**

- **Save DataFrame to CSV**:
    ```python
    df.write.csv('path_to_output.csv', header=True)
    ```

- **Save DataFrame to Parquet**:
    ```python
    df.write.parquet('path_to_output.parquet')
    ```

- **Save DataFrame to Delta**:
    ```python
    df.write.format("delta").save("path_to_delta_table")
    ```

#### **11. Reading and Writing to/from Different Formats**

- **Read Parquet**:
    ```python
    df = spark.read.parquet("path_to_file.parquet")
    ```

- **Read Delta Table**:
    ```python
    df = spark.read.format("delta").load("path_to_delta_table")
    ```

- **Write DataFrame to Delta Table**:
    ```python
    df.write.format("delta").mode("overwrite").save("path_to_delta_table")
    ```

#### **12. Handling Missing Data**

- **Fill Missing Values**:
    ```python
    df.fillna(0).show()  # Fill with 0
    df.fillna({"column1": 0, "column2": "unknown"}).show()
    ```

- **Drop Rows with Missing Values**:
    ```python
    df.dropna().show()
    ```

#### **13. PySpark MLlib (Machine Learning)**

- **VectorAssembler (for Feature Engineering)**:
    ```python
    from pyspark.ml.feature import VectorAssembler

    assembler = VectorAssembler(inputCols=["col1", "col2"], outputCol="features")
    df = assembler.transform(df)
    ```

- **Logistic Regression**:
    ```python
    from pyspark.ml.classification import LogisticRegression

    lr = LogisticRegression(featuresCol="features", labelCol="label")
    model = lr.fit(df)
    predictions = model.transform(df)
    predictions.show()
    ```

- **Random Forest Classifier**:
    ```python
    from pyspark.ml.classification import RandomForestClassifier

    rf = RandomForestClassifier(featuresCol="features", labelCol="label")
    rf_model = rf.fit(df)
    predictions = rf_model.transform(df)
    predictions.show()
    ```

#### **14. PySpark Streaming**

- **Create Streaming DataFrame**:
    ```python
    from pyspark.sql.functions import expr

    streaming_df = spark.readStream.format("socket").option("host", "localhost").option("port", 9999).load()
    ```

- **Write Streaming DataFrame to Console**:
    ```python
    query = streaming_df.writeStream.outputMode("append").format("console").start()
    query.awaitTermination()
    ```

---

### **Common PySpark Operations Summary**

| **Operation**                        | **Syntax**                                              |
|--------------------------------------|---------------------------------------------------------|
| **Create SparkSession**              | `spark = SparkSession.builder.appName("MyApp").getOrCreate()` |
| **Show DataFrame**                   | `df.show()`                                             |
| **Select Columns**                   | `df.select("col1", "col2")`                             |
| **Filter Rows**                      | `df.filter(df["value"] > 10)`                            |
| **Group By**                         | `df.groupBy("col1").agg({"col2": "sum"})`                |
| **Join DataFrames**                  | `df1.join(df2, df1["col1"] == df2["col1"], "inner")`     |
| **SQL Query**                        | `spark.sql("SELECT * FROM df_table WHERE value > 1")`    |
| **Window Function**                  | `windowSpec = Window.partitionBy("col1").orderBy("col2")` |
| **Save to CSV/Parquet**              | `df.write.csv("output.csv")`                             |
| **Fill Missing Values**              | `df.fillna(0)`                                          |
| **Apply UDF**                        | `df.withColumn("new_col", udf_function(df["col"]))`      |

---

This cheatsheet provides a quick reference to the essential features of **PySpark** for working with data, performing aggregations, window functions, SQL queries, machine learning, and streaming. It’s useful for both beginners and those working on large-scale data processing.