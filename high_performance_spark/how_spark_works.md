# How Spark Works
#### Spark vs. MapReduce
* Spark is the successor to Apache MapReduce as it can be used for distributed data processing with Hadoop.
* Unlike MapReduce, Spark does not need to be run with Hadoop.
* Spark uses lazy evaluation for within memory computations are unique

## Spark in the Big Data Ecosystem
* Spark is an open-source framework for parallel data processing that generalizes to different data types and sizes
* Performs computations on Spark JVMs (Java Virtual Machines) that exist only within the Spark application; or within a single JVM on a single machine in local mode 
* Spark is often used with a distributed storage system (HDFS, Cassandra, S3) and a cluster manager (Standalone Cluster Manager, Hadoop YARN, Apache Mesos)

#### Cluster Manager
Cluster manager orchestrates the distribution of Spark applications across the cluster
* handles starting and distributing Spark executors across distributed system according to configuration parameters set by Spark application
* does not distribute data across executors for computation (Spark execution engine does this)
NOTE: Standalone cluster manager is included in Spark but requires install Spark on each node of the cluster


## Spark Core
* Spark provides a high-level query language to process data; users write a program for the _driver_ or master node on a cluster computing system
* Uses lazy evaluation, in-memory storage and immutability to be fault-tolerant, easy-to-use, scalable and efficient
* Spark Core has APIs in R, Scala, Java, and Python

### RDDs
* Core spark data abstraction is _Resilient Distribution Datasets (RDDs)_, which are a representation of statically typed, lazily evaluated, distributed collections
* RDDs had predefined transformations or functions that are applied to an entire dataset included `map`, `join` and `reduce` to manipulate data and I/O functions to read/write between distributed storage systems and Spark JVMs
* _RDDs_ are representations of data sets that are immutable, distributed collections of objects that are stored on the executors or worker nodes
* RDDs are comprised of objects called _partitions_; partitions may be computed on separate nodes (but not necessarily)
* Lazily evaluated: transformations are only computed when the final RDD data needs to be computed (during write out to storage or collecting an aggregate to the drive); partitions computed when action is called
* RDDs can stay loaded in memory on the executor nodes throughout the life of an application for faster access in repeated computations
* Immutable: transforming an RDD returns a new RDD

#### Lazy Evaluation
* _Actions_ are Spark operations that return something other than an RDD (return output to storage layer with `copyToHadoop` or bring data back to driver with `count` or `collect`)
NOTE: RDD interface is not available in R
* Actions trigger the scheduler, which builds a directed acyclic graph (DAG) based on dependencies between RDD transformations
* Actions are evaluated by working backwards to define a series of steps it has to take to produce each object in the final distributed dataset (each partition) -> execution plan 
* Scheduler computes the missing partitions for each stage until it completes the results 
NOTE: Transformations are not 100% lazy, e.g. `sortByKey` must evaluate the RDD to determine range data so it uses a transformation and action

## Spark SQL 
* Provides an interface for DataFrames and Datasets 
* Has a different query optimizer than Spark Core

## Spark MLlib 
* Mostly written on Spark API
* Built on top of RDDs using Spark Core
* To be deprecated by Spark ML

## Spark ML 
* Provides higher-level API than MLlib
* scikit-learn inspired
* Supports DataFrames and Datasets
* Easier creation of machine-learning pipeline than with MLlib
* Built on top of Spark SQL DataFrames
* Spark 1.2 onward

## Spark Streaming 
* Uses scheduling of Spark Core for streaming analytics on minibatches of data
* Unique considerations such as window sizes used for batches

## GraphX 
* Graph processing framework
* Immature 

## Third-Party Libraries
* Found at http://spark-packages.org/
* Can be included at runtime with `spark-submit` or `spark-shell` or as dependencies to `maven` or `sbt` project

