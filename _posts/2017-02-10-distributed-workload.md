---
layout: post
title: Distributed Workload Management  
date:   2017-02-10 13:50:39
---
<h1>Distributed Workload Management</h1>

The motivation for this came from possible enhancements in Apache Airavata. We are tying to address and possibly come up with solution for distributed workload management. This is a hot button concern in distributed environment and there isn't any one solution, we need to come up with own solution based on application need. The crux is how micro-services communicate and work with each other? sounds easy? but it gets convoluted as we think through different building blocks and their boundaries.([reference](https://github.com/airavata-courses/spring17-workload-management/wiki))

<h2>Potential Solutions</h2>
<p>
As I said there isn't any trademark solution, each has its own pros and cons. Even though it is designed considering Apache Airavata, we have tried to keep it as generic as possible.   
We had to go through quite a few iterations to come up with this solution. There is huge chuck of possible solutions, we tried which best suit are requirements.   
First, we started with state-full vs state-less design and obvious inclination was always towards state-less. This design decisions motivated us to think trough centralized vs decentralized architecture.   
Still, there are quite a few implementation concerns we are yet to address like which messaging infrastructure will best serve the need.
</p>

Here are the pages which explain all of this in detail, 
* A state-full design : [LINK](https://github.com/airavata-courses/spring17-workload-management/wiki/1.-A-state-full-design-for-workload-management)
* A state-less design : [LINK](https://github.com/airavata-courses/spring17-workload-management/wiki/2.-A-state-less-design-for-workload-management)
* Final Design : [LINK](https://github.com/airavata-courses/spring17-workload-management/wiki/%5BFinal%5D-Centralized-architecture-for-workload-management)
* Messaging infrastructures : [LINK](https://github.com/airavata-courses/spring17-workload-management/wiki/Messaging-infrastructures)  
<hr />

<h2>Solution Evaluation</h2>
Above WiKi links best explains each solution and its pros and cons. Thanks to dev@airavata.apache.org and class discussions We have been able to come towards the architectural consensus. 

<h2>Conclusion</h2>
As we have decided to move ahead with [final design](https://github.com/airavata-courses/spring17-workload-management/wiki/%5BFinal%5D-Centralized-architecture-for-workload-management), we are building POC to uncover possible corner cases. During this we shall need to evaluate and take critical implementation decisions, any suggestions regarding messaging infrastructure, communication models would be very helpful. 
<hr />

<h2>Github Commits</h2>
We are still working on prototype. We have started implentation and have completed most of the individual tasks and are planing to integrate soon. My contribution towards the poc is tracker [here](https://github.com/airavata-courses/spring17-workload-management/commit/3fa373f72b63a511f8d70c3e11808d1ba1f118e9)
<hr />

<h2>Airavata Dev List Discussion</h2>

Below are the links to dev@airavata.apache.org discussions,   
* Clearing doubts regarding term workload distribution and evaluating designs based on CAP : [LINK](http://mail-archives.apache.org/mod_mbox/airavata-dev/201702.mbox/%3CCAOhYq0tQo8nry0PDYVy5pRhh-MQn8TdU%2BeQWYv2iWZ_XZr211Q%40mail.gmail.com%3E)
* Answering implementation and CD/CI concerns  : [LINK](http://mail-archives.apache.org/mod_mbox/airavata-dev/201702.mbox/%3CCAOhYq0twGd6-LH9am323Ex1qyhLewWQ9%3D%2Bu4e2YtORG5Xzzvcw%40mail.gmail.com%3E)

