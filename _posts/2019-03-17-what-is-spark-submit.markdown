---
layout: post
title: "What is Spark-Submit?"
categories: [spark, data analytic]
tags: [spark, spark-submit, analytic]
---

### What is spark-submit?
{: style="text-align: justify"}
`spark-submit` script in Spark's `bin` directory is used to launch applications on cluster. 

### Example
    spark-submit --master="yarn" --deploy-mode="cluster" 
    --executor-memory=2G --executor-cores=1 --num-executors=64 
    --class="org.apache.spark.examples.SparkPi" 
    --driver-memory=32G --driver-cores=4

`--master` define where spark will executed.  
`--deploy-mode` define mode of deploy, usually used when master using `mesos` url or `yarn`.  
`--executor-memory` define amount of memory that will used per executor process.  
`--executor-cores` define amount of cores that will used per executor process.  
`--num-executors` define number of executor process that will used.  
`--class` define main class that will executed by spark-submit.  
`--driver-memory` define amount of memory that will used for the driver process.  
`--driver-cores` define amount of cores that will used for the driver process.  

### What is different between driver and executor?
- Driver is responsible for task scheduling
- Executor is responsible for executing tasks in your job

### How to define number of driver-memory and executor-memory
{: style="text-align: justify"}
- **If the job is based purely on transformations** like `rdd.saveAsTextFile` or `rdd.saveToCassandra`... then the memory needs of the driver will be very low.
- **If the job requires the driver to participate in the communication** like some Machine Learning processing that need to materialize results and broadcast them on the next iteration using operation like `.collect`, `.take` etc, then the drivers need enough memory to allocate such data.

### Tips
- use small executor cores with many number executor is better than big executor cores with small number of executor.
- If You are use many number executor cores, You don't need to much amount of executor memory.
