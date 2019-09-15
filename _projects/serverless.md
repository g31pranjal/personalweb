---
title : "An experimental evalutation of functions and MapReduce paradigm on Serverless computing architecture"
enddate : 2019-04-25T09:30:00Z+0530
date : 2019-02-10T23:00:00+0530
author : in-arena
desc : Benchmarked various performance metrics of lambda functions execution on Serverless computing architecture using a set of workloads. Studied scalibility, computation and network overhead, and system latency. Also developed a simple map reduce job by chaining lambda functions.
keyword : serverless, kubernetes, open-faas, distributed-systems 
layout : projectTemplate
---

*This was done as part of the Final Project for the cource CS 798: Advanced Topics in Computer Science: Distributed Sysetms.*

### # Evaluation of different workloads:

In the first part of the project we experimentally study the various performance metrics associated with running functions on a Serverless computing architecture. We used a setup consisting of [Docker Containers](https://www.docker.com/) for encapsulating workloads, [Kubernetes](https://kubernetes.io/) network on a 6 node cluster for container orchestration and the [Open-FaaS](https://www.openfaas.com/) framework to listen to function execution requests. We designed 4 workloads that is representative of different scenarios of functions utilization. These were as follows: 
1. **Ping**: Simple function call that basically does nothing. The aim of running this workload is to measure network latency overhead (if any) in the serverless environment. We did two variants of experiments using this workload: hot-start (relevant containers were up and running on nodes), and cold-start (no dockers were running on any of the nodes).
2. **Computation Intensive**: This workload does heavy computation like creating factorial of a very big number. The idea with this workload was to study computation overhead that incurred on nodes.
3. **I/O Intensive**: Does a lot of I/O request to the underlying NFS. Idea is to measure the network latency and throughput for huge data transfers. 
4. **Scalability**: Finally we design a workload to study the automatic and manual scalability of the architecture. We essentially carry the experiment by generating varied number of requests to the Open-FaaS API and note down the response time and request drops.

### # MapReduce

In this part of the project, we take a simple workload and solve it using the [MapReduce](https://www.ibm.com/analytics/hadoop/mapreduce) paradigm on the serverless architecture. Our task was to count the frequency for each unique word that appeared in a multi-billion text corpus. We design a 1-stage reducer job which was loosely inspired by this [Amazon AWS article](https://aws.amazon.com/blogs/compute/ad-hoc-big-data-processing-made-simple-with-serverless-mapreduce/). Out system design is as illustrated:

<br>
<img style="display: block; width : 65%; margin : auto" src="/assets/img/serverless-1.png">

### # Results

We report important metrics like the round trip time, I/O overhead and latency, computation overhead and finally an analysis on how the system scales with the change in number of nodes in the cluster and requests per second. Finally we draw important inferences with respect to the scaling policy and end-to-end system workflow.

The results are too large to be put here. See the <a href="/assets/serverless-report.pdf" target="_blank">project report</a>.


### # Team: 
[Shreesha Addala](https://www.linkedin.com/in/shreeshaaddala/) and me :)