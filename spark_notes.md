* `StringIndexer` runs entirely on the driver
* `OneHotEncoder` creates dummy variables out of inputs
* `HashingTF` can be used to hack around the issue, works on a column of sentences
* `RFormula` 

### Spark - Don't Use the Defaults!
* Configuring Spark correctly is crucial
* Understanding how Spark works internall is critical to writing efficient and function Spark code
* In Spark 2+, `PYSPARK_DRIVER_PYTHON=ipython pyspark` 
* Lower `num_partitions` to reduce 
#### Key Spark Components
* Resilient Distributed Dataset (RDD)
* Partitions
*
* Shuffle
The process of repartitioning data (sometimes across JVM processes or node executors); it a process of data transfer between stages
Avoid shuffling. Leverage across existing partitions. Leverage partial data transfer.
* Stages
### YARN Changing the Defaults



### Misc
* cross-validation rule of thumb: use between 5 and 10 folds
* upsampling and downsampling


### Automatic Feature Selection
* Chi-squared test of significance - more manual
* regularization

### Logistic Regression Notes
* `productid` and `customerid` useless without interactions or non-linear effects


### Stratified Sampling
* `sampleBy() in Spark
* A method of sampling from a population that includes creating homogenous subgroups from the population and then sampling the subgroups.
* Strata must be mutually exclusive and collectively exhaustive (excluding no population element)
#### Benefits
* Simple random sampling or systemic sampling is applied to each strata 
* Improves the representativeness of the sample by reducing sampling error
* Weight mean may have less variability than the arithmic mean of a random sample
* Method for reducing variance when when Monte Carlo methods are used to estimate population statistics from a known population
* Why do we want to use stratified sampling? Really downsampling?

### GitHub

`git rev-parse --verfiy HEAD` or `git rev-parse HEAD` will display the commit hash of the current branch
`git log --pretty=format:'%H' -n 1` use `'%h'` for short commit


### Homebrew

`brew doctor`
`brew list`
`brew uninstall`
`brew missing`
