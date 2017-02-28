---
layout: post
title: Distributed Workload Management  
date:   2017-02-26 13:50:39
---
<h1>Distributed Workload Management</h1>
As discussed in previous [Distributed Workload Management](https://ajinkya-dhamnaskar.github.io/2017/02/10/distributed-workload.html)
blog, this one is mainly about prototype implementation for [final design](https://github.com/airavata-courses/spring17-workload-management/wiki/%5BFinal%5D-Centralized-architecture-for-workload-management)   

So far, we have been able to implement all the tasks, I worked on following;
* Environment Setup [LINK](https://github.com/airavata-courses/spring17-workload-management/tree/develop/workers/DataStaging)
* Data Staging [LINK](https://github.com/airavata-courses/spring17-workload-management/tree/develop/workers/DataStaging)   

both these tasks require remote system interaction, so we decided to club them in a single jar.   
We have implemented SCP and SFTP protocols in both the tasks. 

I contributed to [messaging infrastructure] (https://github.com/airavata-courses/spring17-workload-management/tree/develop/Messaging).
We started with pub-sub rabbitmq model but as we moved further we got to know worker model better suits our requirement. Worker model guarantees,
message consumption by single worker at a time, if worker fails to process, the message gets queued again for other waiting workers.    
I also implemented priority provisioning for rabbitmq messages, this would help alter message priority based on user need. 

Gourav and I worked on scheduler, we are yet to come to consensus regarding responsibilities of scheduler, do we need database? how can we support delayed job submission? in 
hackillinois when we presented workflow issue in front of students they came up with an interesting match making scheduling algorithm, we might consider using the same, 
I shall explain this algorithm in next blog after reviewing its correctness.    

As far as orchestrator is concerned we are yet to make significant move, for now we have written simple stub which mocks orchestrator functionalities.
Amruta is working on graph db, but still we are exploring some grey patches such as what each node represents? and how different nodes can be mapped with each other?
what role orchestrator plays in terms of task context creation and DAG manipulation? 

<hr />

<h2>Github Issues</h2>
Below are the issues created by me;
* [Environment Setup Task](https://github.com/airavata-courses/spring17-workload-management/issues/11)
* [Implement Data Staging task](https://github.com/airavata-courses/spring17-workload-management/issues/10)
* [Comment on "Implement a database service for DAG"] (https://github.com/airavata-courses/spring17-workload-management/issues/3#issuecomment-282820397)

<hr /> 

<h2>Github Commits</h2>
My git commits are tracked [here](https://github.com/airavata-courses/spring17-workload-management/commits/develop)
<hr />
