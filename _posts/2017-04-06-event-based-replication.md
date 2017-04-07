---
layout: post
title:  "Event Based Database Replication In Airavata Cont...."
date:   2017-04-06 13:50:39
---

<h1>Event Based Database Replication In Airavata Cont....</h1>

While working through [previously discussed](https://ajinkya-dhamnaskar.github.io/2017/03/23/event-based-replication.html) approach we discoved that the Topic Routing implementation of 
RabbitMQ resonate with our requirement. As discussed earlier, consider below diagram, Service A publishes db event to 'DB Event Exchange', event manager intercepts that message and lookup for corresponding subscriber services in zk. As service_B and service_C are interested in events from service A, event manager pushishes message to exchange with routing keys 'service_B' and 'service_c'. That way message gets routed to correponding services. If multiple instances of the same service are listening to a queue only one of them reacts. 

<p align="center"><img src="../../../assets/db-event.png" alt="Service Discovery"></p>

We had to send multiple messages to exchange with different routing keys (service_B, service_C). Here, if DB event manager fails to send message with any of the routing keys, sytem would be in unstable state.
RabbitMQ allow us to design routing key in a such a way that message can be routed to multiple queues through an exchange.
Above case can be handled by sending message with routing key 'service_B.service_C', this way DB event manager is sending just one message and RabbitMQ then guarantees delivery to mutiple queues.   

With this new tweak, we just need one publisher at DB event manager and messages can to sent by altering routing keys, 
for example, if new service node service_D gets added, message would be sent with routing key 'service_B.service_C.service_D' using the same exchange and inturn the same publisher.

<p align="center"><img src="../../../assets/db_event_routing.png" alt="Service Discovery"></p>

Gourav and I have completed this part in airavata and created a [pull request](https://github.com/apache/airavata/pull/105)
<hr/>

<h2>Github Commits</h2>
My contribution is tracked under [pull request](https://github.com/apache/airavata/pull/105).



