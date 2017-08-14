# spark-radar
Radar implements a new scheduler for spark streaming on heterogeneous clusters. On the one hand, Radar gets each task's size from HDFS or BlockManager. On another hand, Radar evaluates each node's capability by exploiting the recurring characteristics of spark streaming. Being aware of tasks' size and nodes' capability, Radar can make much better scheduling decisions.

## How to use ?

Now, Spark-Radar is based on Spark-2.1.1, so you can get the documentation from Spark homepage (http://spark.apache.org/). This is only the source code of Radar. So you need to compile Radar using mvn or sbt first. Then, you can deploy Radar on a heterogeneous cluster and run heterogeneous tasks on it to test its performance.

### System Overview

![image](https://github.com/u2009cf/spark-radar/blob/master/image/system%20architecture.png)

In radar, we design a new scheduler based on tasks' size and node capability. Traditional locality-aware scheduler is not suitable for heterogeneous tasks and shared clusters. We propose to add two eyes for scheduler. One is tasks' size which we can get from HDFS. Another is node's capability which we can get by exploiting the recurring characteristics of spark streaming batches. We make scheduling decisions according to the following principles: (1) large task first which we can amortize the large tasks' impact on stage execution time through multi waves, (2) fast nodes large tasks and slow nodes small tasks which we can achieve better load balancing, (3) choose task in corresponding location of node capability order for this node.

#### Evaluation Results

Radar can avoid 86.57% speculative tasks, lower 20.96% latency and save about 10% resources in Tencent production clusters.
