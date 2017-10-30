---
title: DevOps - Build and deploy a collection of micro-services
description: Explore how to manage your database upgrades
ms.assetid: 
ms.prod: vs-devops-build-deploy-collection-micro-services
ms.technology: vs-devops-articles
ms.manager: willys
ms.date: 18/10/2017
ms.author: rodrigoantunes
author: rodrigoantunes
---

> 
> #**THIS IS DRAFT.1 - WORK IN PROGRESS **
>

# What are Microservices?
A monolithic application puts all its functionality into a single process, and scales it by replicating the monolith on multiple servers.
A multi tier application separates its functionality into tiers - tipically three -, and scales each layer  by replicating on multiple servers.
A microservices architecture puts each element of functionality into a separate service, and scales it by distributing those services across servers, replicating as needed.

“Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure.”  -- Melvyn Conway, 1967
Cross-functional teams, organized around capabilities (Conway's Law)

SOA 
- Services are interfaces of a large monolith
- Orchestration is often required and tend to contain business logic
- Spans across the enterprise

Microservices
- Services are individually developed and deployed
- Does not require integration technology, logic resides in microservices
- Can be limited to an individual project

# Microservices Patterns
API Gateway
- Challenges this pattern solves:
-- Granularity of services is often more fine grain than what client would need
-- Different type of clients need different data
-- Protocol used by services differ greatly. E.g. AMQP, WebSocket etc.
-- Partitioning of services should be hidden from the clients 
- Solution:
-- API Gateway act as an entry point for all access to Microservices by encapsulating the internal system design and provides:
-- API that is tailored for each client 
-- Security features such as authentication, token cache etc.  
-- Protocol transition 
-- Load balancing 

Service Discovery
- Challenges this pattern solves:
-- Services addresses change dynamically due to auto scaling 
-- Discovering services is inheriting more challenging as more services are added
- Solution:
-- Discover services dynamically using service registry (database of available services) that will locate the instance of service to call
--- Client Side Discovery 
--- Server Side Discovery 

Deployment Patterns
When Deploying Microservices have to consider following:
- Each service is independently scalable and deployable 
- Deployment should be automated, fast and reliable
- Service usage of resources (CPU, memory etc.) should be configurable 
- Scale out by running multiple instances per service

# Containers and Microservices
Docker

# Build and deploy
demo stuff


# Microservices Real World Case Studies
http://tinyurl.com/NetflixMicroservices 
http://tinyurl.com/SoundCloudMicroservices 
http://tinyurl.com/NginxMicroservices 



> Authors: Rodrigo Antunes | Find the origin of this article and connect with the ALM Rangers [here](https://github.com/ALM-Rangers/Guidance/blob/master/README.md)
 
*(c) 2017 Microsoft Corporation. All rights reserved. This document is
provided "as-is." Information and views expressed in this document,
including URL and other Internet Web site references, may change without
notice. You bear the risk of using it.*

*This document does not provide you with any legal rights to any
intellectual property in any Microsoft product. You may copy and use
this document for your internal, reference purposes.*
