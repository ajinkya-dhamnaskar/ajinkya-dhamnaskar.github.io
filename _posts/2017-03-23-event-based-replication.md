---
layout: post
title:  "Event Based Database Replication In Airavata Cont...."
date:   2017-03-23 13:50:39
---

<h1>Event Based Database Replication In Airavata Cont....</h1>

In the [previous](https://ajinkya-dhamnaskar.github.io/2017/03/09/event-based-replication.html) approach, we were creating a lot of queues, but then we came across TOPIC implementation of RabbitMQ which would essentially offload event manager from creating large number of queues.
We discovered that TOPIC implementation of RabbbitMQ can also be used as a work-queue with a few tweaks. We have been able to implement this approach, let's discuss implentation details,   

Services simply publish message to 'DB Event Exhange' but with the routing key 'db.event.queue' which redirects message to 'db.event.queue'. Db Event Manager listens to this queue and act on message based on message type.   

If it's a service discovery message, it simply updates zk node structure. Consider following depicted case, where service B and service C are interested in events from service A. Both these services sends service discovery message to DB Event Manager which in turn updates zk node structure as shown.

<p align="center"><img src="../../../assets/service-discovery.png" alt="Service Discovery"></p>

In case of DB Event message, it simply fetches all interested subscribers from zk and sends message through same exchange but using multiple routing keys. This designs offloads DB Event manager at the suscriber front, as DB event manager need not to create subcriber for each service any more.   

Consider below diagram, Service A publishes db event to 'DB Event Exchange', event manager intercepts that message and lookup for corresponding subscriber services in zk. As service_B and service_C are interested in events from service A, event manager pushishes message to exchange with routing keys 'service_B' and 'service_c' respectively.

<p align="center"><img src="../../../assets/db-event.png" alt="Service Discovery"></p>

Here, we are using same exchange for control messages and db events but with different routing keys.
<hr />

<h2>Github Commits</h2>
My contribution is tracked [here](https://github.com/ajinkya-dhamnaskar/airavata/commits/user-profile)

<hr />
<h2>Alternate Solution - AKKA</h2>
Gourav and I are exploring AKKA alternative for the same. Where each service can be considered as an Actor. 
Each Actor maintains its own mailbox and reacts to the messages as they come.

<p align="center"><img src="../../../assets/akka-approach.png" alt="Service Discovery"></p>

In our case, services and DB Event Manager both can be considered as actors. DB Event publishing service sends message to DB event actor and DB event actor in turn sends messages to corresponding actors based on saved mapping.
AKKA's inherent design resonate with our problem, but we are still in POC phase. We are working through some challages such as remote actor discovery, actor failure, multiple instances of the same actor(service) etc.
