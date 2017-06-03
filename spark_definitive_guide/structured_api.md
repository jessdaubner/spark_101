# Structured API (DataFrame and Datasets)
* Spark has two distinct types structured APIs: DataFrames and Datasets
* The DataFrame API is the "untyped API" and can be used across languages
* DataFrames do have types but only operate on _Spark_ types at _runtime_ 
* Each record or row in the DataFrames API consists of a `Row` object that are available across languages and have types, but only Spark types, not native language types
* The Dataset API enables users to define their own data types to represent each record in the dataset with "case classes or Java Beans" and types are checked at _compile time_
* The Dataset API is the "typed API" and is only available to JVM based languages (Scala and Java)
* DataFrame and Dataset are distributed tables with rows and columns
* Each column must have the same amount of rows as the other columns (values can be null)
* Each column must have type information
* DataFrames and Dataset are representations of immutable, lazily evaluated plans that specify how to perform a series of transformations to generate the correct output 
* Performing an action on a DataFrame instructs Spark to execute the transformations that represent the DataFrame
* Lower-level API (RDDs) do not have schemas 

* Spark is effectively its own programming language
## Spark Value Types
* Spark maintains its own type information, stored as a schema, which enables it to perform optimizations during the execution process
* The majority of operations are performed on _Spark types_ not Python types

* Columns can have simple types (`IntegerType`, `StringType`) or complex types (`ArrayType`, `null`, `Map`)
* `Row` objects are the most general way of getting data into and out of Spark. Each record in a DataFrame must be of `Row` type
* Using Scala or Java allows you to define your own JVM types that consist of Spark types to use in place of Rows. You must use an _Encoder_, which are only available in Scala with case classes, and Java with Java Beans. Some Spark types already include Encoders. 

`from pyspark.sql.types import *`

Spark Type | Python Value Type | Python API 
Byte-Type |
Short-Type | 

## Spark Execution
A single structured API query from user code to executed code:
1. Users writes DataFrame/Dataset/SQL code and submits it through the console or a job
2. Spark convert user code to a _Logical Plan_
3. Spark transforms the _Logical Plan_ to a _Physical Plan_
4. Spark executes the _Physical Plan_ on the cluster

### Logical Plan
* The logical plan represents a set of abstract transformations (does not refer to executors or the driver)
* 
### Physical Plan
* The Physical Plan, aka Spark plan, specifies how the logical plan will be executed on the cluster
* Generates different 
The _Catalyst Optimizer_ determines how the user's code should be executed and lays out the physical plan for doing do
:
