# Using Cassandra with Spark 
---
## Cassandra Basics
Clustering keys are different than primary keys (primary key and clustering keys together uniquely define a row)

## Cassandra-Spark Connector API
### Common Method for Data Retrieval
* `cassandraTable(keyspace, table)` - Returns an RDD that contains all rows from a Cassandra table in a specified keyspace. This method is called on a _SparkContext_ object.
* `withAscOrder` / `withDescOrder`
```
select(columns)
cassandraTable(keyspace, table)
where(condition, [parameters])
withAscOrder | withDescOrder
limit(n)
```
* Push as much as the filtering to Cassandra as possible

### Data Type Conversions
* Cassandra Row API
* You must know the Cassandra type before you can read a value and know which native Scala/Python type it converts too
