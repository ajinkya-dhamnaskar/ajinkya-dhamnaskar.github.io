---
layout: post
title:  "Event Based Database Replication In Airavata"
date:   2017-03-09 13:50:39
---


<h1>Event Based Database Replication In Airavata</h1>

This is in continuation to the earlier [blog](https://ajinkya-dhamnaskar.github.io/2017/02/17/event-based-replication.html). The proposed solution will be used to solve data replication problem in airavata. As a by-product of registry refactoring, user_profile and sharing module have been detached and qualified as independent microservices. The purpose of this context is to design event based data replication in aformentioned case. The goal is to design scalable, portable and managable event driven component to accomodate any new segregation on the fly. 

First, we thought of having event communication logic in every microservice, but we soon ran into a problem of replication of same logic at every microservice. Also, if new service is interested in events from one service, we would need to change publisher to accomodate new changes which is kind of unacceptable to a microservice. 

The better way to handle these problems was to have centralized event manager which is responsible for maintaining publisher - subscriber map.  

<p align="center"><img src="../../../assets/airavata_event_driven_data_replication.png" alt="Example Image"></p>

Let's use the example illustrated in above figure to understand proposed designed. Assume, when new user is added to the system, some of the user profile attribute need to be replicated in sharing and application service. User profile service publishes and event with oprations type(CRUD)and entiry type. DB Event Manager processes event queue and acknoledges back to publisher, so User service is now free to commit trasaction. Now its event manager's responsibility to deliver this event to interested services. 

Whenever, new service is interested in event related to any entity, it simply shows its interest by sending message to event manager, event manager then adds this service in a local map against particular enitity.

DB event manager uses local map to identify corresponding subscribers in this case sharing_sub and application_sub and sends user creation event on respectives queues. 

Now, the challange here is to employ some parmanent chaching logic to avoid any loss of this mapping incase event manager crashes. We are using ZK as a parmanent cache to store this mapping, so when event manager comes up it can restore mapping using ZK node state. 

There can be multiple instances of a same service listening to a queue but only one would react to the message as we are using work queue model.  

ZK creates a publisher entity node, any service which is interested in this entity will have node inside publisher entity. Here, user is a parent directoy (publisher entity) and all the nodes inside user are interested services(subscribers). 
