# Spark Application Parameters Overview 

Yarn: The default cluster manager; allocates resources on the cluster
* Yarn default memory allocation is max(384, .07 * spark.executor.memory).

_Driver_:
* _Application master_ is a non-executor container with the special ability to request containers from YARN. It runs on the driver in cluster mode. The `driver-memory` and `driver-cores` give more resources to the application master.

_Executor_: a JVM instance on a node; a single node can have multiple executors; the containers that run tasks assigned by the driver
* `num-executors`: Total number of exectors running on nodes of the cluster 
* `executor-cores`: The number of executor cores is the number of concurrent tasks an executor can run. More is not necessarily better.
* `executor-memory` controls the executor heap size

### Setting `executor-cores`, `executor-memory` and `num-executors` 
1. Set `executor-cores` to 5 (NOTE: ability of executor, NOT the cores a system, i.e., still 5 cores even if you have 32 cores in the CPU)
2. Determine the number of executors per node, (total cores on node - 1 core for OS/Hadoop Daemons) / cores per executor 
3. Determine memory per executor, (Available GB RAM - 1GB for OS/Hadoop Daemons) / number of executors and multiple this number by .93 to account for the default Yarn memory overhead on each node


#### Resources
* [How to Tune Spark Executor Number Cores and Executor Memory]: http://stackoverflow.com/questions/37871194/how-to-tune-spark-executor-number-cores-and-executor-memory
* [How to Tune Your Apache Spark Jobs Part 2]: http://blog.cloudera.com/blog/2015/03/how-to-tune-your-apache-spark-jobs-part-2/
