# Spark: The Definitive Guide
## Introduction 
* Spark is a distributed programming model, where the users specifies _transformations_, which build a directed-acyclic-graph (DAG) of instructions, and _actions_, which begin the process of executing the instructions of the graph as a single job.
* Spark is the most active Apache project
* A job is broken down into stages and tasks to execute across the cluster.
* Data is stored as DataFrames or Datasets.
* To create a new DataFrame/Dataset, the users calls a transformation.
* To start a compution or convert to native language types, the user calls an action.
* Tool for processing data and managing the resources of a cluster of computers

### Two APIs: Unstructured and Structured
Spark APIs follow the standard [MAJOR].[MINOR].[MAINTENANCE]

#### Unstructured (RDDs, Accumulators, Broadcast variables)
* Low-level, meant for manipulating raw java objects (unstructured data like documents)

#### Structured (DataFrames, Datasets and Spark SQL)
* High-level, for semi-structured and structured data types 
* Optimized to work with data in a spreadsheet-like interface
* Most of the same user-facing operatings can be used for _batch_ and _streaming_ computations

### Spark applications consist of two processes
#### Driver
Driver process is the heart of the Spark application and maintains all relevant information during the lifetime of the application.
* sits on the driver or master node 
* contains language bindings
* responsible for three things
....1. maintaining information about the Spark application
....2. responding to user program
....3. scheduling work across executors
* the driver is represented through `SparkSession`

#### Executors
Executors sit on worker nodes and are responsible for two things:
1. executing code assigned to it by the driver
2. reporting the state of the computation back to the driver node

### Cluster Manager
* The cluster manager controls physical machines and allocates resources to Spark applications
* Options are standalone, default cluster manager, YARN, or Mesos

#### Local Mode
* Since the driver and executor are processes, they can be run locally
* In this case the workers are threads on your local machine

### Supported Languages
* Spark is written in Scala; hence, Scala is the "default" language
* Python supports most of what Scala supports
* Java, SQL and R are also supported

### Partitions
* In order to leverage the resources of the machines in the cluster, data is broken into chunks, called partitions
* A _partition_ is a collection of rows that sit on one physical machine in the cluster
* A DataFrame consistes of zero or more partitions
* Spark operates on each partition in parallel unless an operation calls for a _shuffle_

### Shuffle
* A shuffle occurs when multiple machines need to share data
* Break up tasks (data + computation) and give them to the executors as efficiently as possible 

### Computations
Computations are organized into two categories: transformations and actions

### Transformations
* Core data structures are immutable (they cannot be changed once created)
* Transformation specify how to modify an existing DataFrame into a new DataFrame
* Spark uses _lazy evaluation_, meaning it waits until the last minute to excute code and make the plan run as efficiently as possible across the cluster

### Actions
* Actions instruct Spark to compute a result from a series of transformations; actually triggers the computation
* Transformations are not executed until an action is called on a DataFrame or one of its derivatives
* Example: `count()`, `take()`
* There are three kinds of actions:
....1. Actions to view data in console
....2. Actions to collect data to native objects
....3. Actions to write to output data sources

### Spark UI
* Users can monitor the progress of their Spark job through the UI
* Spark UI is available on port 4040 of the master/driver node (in local mode: http://localhost:4040)
* Spark UI maintains information on the state of the Spark job, environment and cluster state 
* Very useful for tunning and debugging Spark jobs

### SparkSession
* `SparkSession` is the entry point for performing work the cluster; the user-facing part of the Spark application
* Used to parallelize collections and create DataFrames directy from a file or set of files
```python
df = spark.read.json("path/to/file")
df.take(2) # returns array of Row objects
df.sort("count")

df2 = (spark
       .read
       .option('inferSchema', 'true')
       .option('header', 'true')
       .csv('path/to/file'))
```
* Use `explain()` on a `DataFrame` to view the Spark transformation (true optimized physical execution) plan; the logical combination of transformations Spark will run on the cluster; use it to make sure code is as optimized as possible!
* Physical plan shown by `explain()` will show `partial_sum` and other commutative actions that are performed partition by partition
* Logical plan defines _lineage_ for the DataFrame so that Spark can recompute any partition of a DataFrame back to a robust data source (file or database)
* Spark is always building up a directed acyclic graph of transformations resulting in immutable objects that we can call an action on to see the results
* `.option()` specifies how to read a file format and take advantage of the structure of the file (e.g., `inferSchema` and `header` for csv files) 
 
```python
jsonSchema = (spark.read.format('json')
              .load('path/to/file')
	      .schema)
print(jsonSchema)
```
* Schemas can be explicitly set instead of inferred (aka schema on read) to avoid errors (with `.schema()`and lessen computational time

## Abstractions
* Core abstractions are Resilient Distributed Datasets (RDDs), DataFrames, Datasets, SQL Tables
* All abstractions represent distributed collections of data 

### DataFrames
* A DataFrame is a table of data with rows and columns
* The list of columns and their types is called a _schema_ and can be accessed with `printSchema()` or `describe`; analogous to the way schema is used with databases to describe the data types of columns in a table
* Pandas DataFrames and R DataFrames can be converted to Spark DataFrames
* DataFrames are the easiest and most efficient Spark abstraction

### SQL
* Spark SQL enables uses to register DataFrames as a table or view (temporary table) and query it using SQL
* There is no performance difference between writing SQL queries and writing DataFrame code as both are computed using the same underlying plan
* A SQL query against a DataFrame returns another DataFrame
```python
# create a table from a DataFrame
df.createOrReplaceTempView("df_table")

sqlWay = spark.sql("""
SELECT first_column, COUNT(1)
FROM df 
GROUP_BY first_column
""")

dataFrameWay = df.groupBy('first_column').count()

# plans are the same
dataFrameWay.explain()
sqlWay.explain()
```

```python
from pyspark.sql.functions import max
spark.sql.select("select max("count") from df).take(1)
df.select(max("count")).take(1)

maxSql = spark.sql("""
SELECT country_name, sum(count) AS country_total
FROM flight_df
GROUP BY country_name
ORDER BY sum(count) DESC
LIMIT 5""")
maxSql.collect()

from pyspark.sql.functions import desc
maxDF = (flight_df
         .groupBy('country_name')
	 .sum('count')
	 .withColumnRenamed('sum(count)', 'country_total')
	 .orderBy(desc('country_total'))
	 .limit(5)
	 .collect())
```
* Most DataFrame methods take a String (a column name), a Column Type or an expression (columns = expressions)
* `limit()` filters by position (lazily) instead of by value

