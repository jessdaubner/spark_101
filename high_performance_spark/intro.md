## Optimizing Spark Perforance
* Time and resources gained from tuning code for performance are enoromous
* Performance is not only about running faster but running at all
* Keep an eye towards the structure of data and requirements of cluster from the onset
* Spark is highly configurable and exposed at a higher level than other frameworks
* Must understand specific use case, data, and system (e.g, the oft repeated advice to avoid `groupByKey` for fear of OOM exeptions is not necessarily applicable for data with few duplicates)

## Learn Spark in Scala 
* Serious performant Spark development is most easily achieved in Scala
* To be a Spark expert you need to know a little Scala anyway
* Understanding the Spark codebase is key to becoming advanced Spark user
* Methods in the `RDD` class closely mimic Scala collections API
* `map`, `filter`, `flatMap`, `reduce` and `fold` are almost the same as Scala equivalents
* Spark is a functional framework and relies heavily on immutablility and lambda definition
* Scala development is much easier than Java for Spark (Java doesn't have a REPL, inline function definitions and lambda expressions are more difficult in Java)
* Scala is more performant that Python: Scala is statically typed and the cost of JVM communication from Python to Scala can be very high
* To use cutting-edge Spark functionalty you need to be in the JVM; Python support for Spark Streaming and ML are especially behind
* Spark SQL minimizes performance differences between non-JVM languages
* Disadvantage of Scala is that there are few specialized data science libraries (i.e., numpy doesn't exist in Java and Scala)

