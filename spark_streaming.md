# Spark Streaming
Spark DStreams are made up of RDDs
Hadoop: HDFS - distributed file system for storing data, MapReduce - parallel processing batch framework
Real-time processing
Data is received as a stream, with a discrete entity (tweet, log message)
Entities are available over a period of time
Uses same APIs and concept as batch processing in Spark

## RDDs - Core Programming Abstraction 
* All operations in Spark are performed on _in-memory_ objects
* RDDs are collections of entities - rows, records  
* RDD in Spark is analougous to Collection object in Java; can be assigned to a variable and methods can be invoked on it 
* Methods perform transformations or return values 

## Characteristics of RDDS
* Partitied - rows are split across nodes in the cluster (e.g. like file partitions in Hadoop), processing occurs in parallel, data is stored in-memory on each node
* Immutable - transformations create new RDDs with updated entities; actions - read data from RDD  
* Resilient - can be reconstructed in case of node failure; every RDD keeps track of every operation that occured on it from the beginning of time (lineage, dependency graph for all parent RDDs); transformations are not executed until an action is called; RDDs are lazily evaluated 

* Stand-alone Spark installation does not require YARN or Hadoop 
* ("without hadoop" installation means its not tied to a specific version of Hadoop) 
* Still need Hadoop installed b/c Spark references packages from the Hadoop installation
* `map` performs a transformation on every row 
* `flatMap` converts a single row of input to multiple rows 

## Discretized Streams (DStreams)
* Stream of entities is represented as a discretized stream or DStream class
* DStream is a sequence of RDDs
* Entities in the stream are grouped into batches; each batch is one RDD
* Each batch is formed based on a _batch interval_
* DStreams are immutable, transformations create new transformations
* Within DStreams, Spark does _batch processing on individual RDDs_  

`SparkContext` sets up internal services and a connection to Spark from our application 
`StreamingContext` main entry point for Spark streaming functionality 
* StreamingContext(SparkContext, batchInterval) - set batch interval for all DStreams created by the StreamingContext
