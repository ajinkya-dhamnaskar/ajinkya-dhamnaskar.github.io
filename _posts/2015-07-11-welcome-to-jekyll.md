---
layout: post
title:  "Event Based Database Replication For Microservices"
date:   2017-02-17 13:50:39
categories: jekyll
---

<h1>Event Based Database Replication For Microservices</h1>

<p>The goal of this project is to explore possible ways to manage data across micro-services. The outcome would eventually be applied to address possible enhancements in Aapche Airavata. Having said that we shall try to keep this as generic as possible. This will eventually lead to find best possible way to manage data across different micro-services without compromising any of the key attributes of micro-service.</p>

<p>The whole purpose of the micro-service architecture is separation of concerns and independence. The key here is to make your service independent of surrounding but,</p>


<ul>
<li>How?</li>
<li>Can micro-service has its private database?</li>
<li>If so, what if micro-services working together need to share data?</li>
<li>Is it a good idea to allow micro-service query data from other than its private database?</li>
<li>Can we maintain such data is shared database?</li>
</ul>

<hr />

<h2>Possible Challages</h2>

<p>All the problems stated above can be addressed by maintaining everything in one database. But certainly it is not a good idea considering maintainability and portability of both database and micro-service. Micro-service should be responsible to maintain only required data. But as we think through, it would lead to a data sharing problem. If one micro-service requires data created by other, it would need to make either direct remote database call or CPI call to a micro-service who owns that data. But again here micro-service is depending on other services for its own existence, if any of these is not available micro-service would fail to process request.</p>

<hr />

<h2>Potential Solutions</h2>
<ul>
<li>2-Phase Commit</li>
<li>Event Driven replication</li>
</ul>

<hr />

<p>Here we will explore Event Driven replication considering its advantages in distributed environment. Gourav and I started finding possible solutions and have implemented proof of concept for the same.</p>
<p>Please refer below links which detail our finding and instructions to work through the implementation.</p>


[Event Driven Approach](https://github.com/airavata-courses/spring17-microservice-data-management/wiki/An-Event-Driven-Architecture-Explained)
[Prototype](https://github.com/airavata-courses/spring17-microservice-data-management/wiki/Event-Driven-DB:-Steps-to-Run-Prototype)


<h2>Github Commits</h2>
<p>I started contributing to Gourav's [EventDrivenDBMicroservices](https://github.com/gouravshenoy/EventDrivenDBMicroservices) repository. After formal introduction in front of class I moved entire project under [spring17-microservice-data-management](https://github.com/airavata-courses/spring17-microservice-data-management). Due to this move personal commits are lost. My commits are directly on master as most of the part that I did was completed in previous repository, below are the links for my contribution,</p>

<ul>
<li>Commits to airavata-courses repository : [LINK](https://github.com/airavata-courses/spring17-microservice-data-management/commits/master)</li>
<li>Commits to Gourav's repository : [LINK](https://github.com/gouravshenoy/EventDrivenDBMicroservices/commits)</li>
</ul>
