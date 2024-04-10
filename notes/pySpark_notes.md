# PySpark Notes
For version 3.5.1.

## Documentation
- [Official PySpark docs](https://spark.apache.org/docs/latest/api/python/index.html)

## How to suppress Spark output in Jupyter notebooks  
1. In terminal, create a default profile:
```
ipython profile create
```
  - The command above will print out two file paths for the config files it generated.
  - **Copy the second path**, the one ending with ipython_kernel_config.py, and paste it in the command below.

2. Write to the kernel config file to turn off the capture flag:
```
echo "c.IPKernelApp.capture_fd_output = False" >> \
  "<REPLACE THIS WITH THE FILE PATH FOR ipython_kernel_config.py>"
```

Source: [this SO answer](https://stackoverflow.com/a/70613254/23800771)


## Tutorials
- [17 min intro tutorial](https://www.youtube.com/watch?v=YvTzvZh3yTE)

## Notes on [Official PySpark docs](https://spark.apache.org/docs/latest/api/python/index.html)
### Quickstart: DataFrame
PySpark DataFrames are lazily evaluated. They are implemented on top of [RDDs (resilient distributed datasets)](https://spark.apache.org/docs/latest/rdd-programming-guide.html#overview). When Spark transforms data, it does not immediately compute the transformation but plans how to compute later. When actions such as collect() are explicitly called, the computation starts.

#### Initializing a SparkSession
PySpark applications start with initializing SparkSession (one session per application):
```
from pyspark.sql import SparkSession
  
spark = SparkSession.builder.getOrCreate()
```

#### DataFrame Creation  
- A PySpark DataFrame can be created via `SparkSession.createDataFrame` by passing it one of the following:
  - a list of lists, tuples, dictionaries and pyspark.sql.Rows
  - an RDD consisting of such a list
  - a pandas DataFrame
- `SparkSession.createDataFrame` takes the schema argument to specify the schema of the DataFrame. When it is omitted, PySpark infers the corresponding schema by taking a sample from the data.
- Creating a PySpark DataFrame from a pandas DataFrame:
  ```
  spark_df = spark.createDataFrame(pandas_df)
  ```
- Creating a PySpark DataFrame from other inputs: [see examples in the docs](https://spark.apache.org/docs/latest/api/python/getting_started/quickstart_df.html#DataFrame-Creation)

#### Viewing Data
- Show top rows: `spark_df.show(5)`
- Print columns: `spark_df.columns`
- Print schema: `spark_df.printSchema()`
- Print dataframe summary (like Pandas): `spark_df.describe().show()`
- Collect the distributed data: `df.collect()`
  - shows data and its metadata
  - `DataFrame.collect()` collects **all** of the distributed data from executors to the driver side, and makes it available as **local** data in Python. This can throw an out-of-memory error when the dataset is too large to fit in the driver side (i.e. locally).
  - In order to avoid throwing an out-of-memory exception, use `DataFrame.take()` or `DataFrame.tail()` instead.
- Get N rows of the distributed data: `df.take(N)`
  - shows data and its metadata based on the N rows
- **Convert PySpark dataframe to Pandas dataframe:** `pandas_df = spark_df.toPandas()`

  
