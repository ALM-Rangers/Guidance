---
title: DevOps - Manage database upgrades
description: ?
ms.assetid: 547cbec5-e619-4eea-ad0b-2b4d19393280
ms.prod: vs-devops-manage-database-upgrades/
ms.technology: vs-devops-articles
ms.manager: douge
ms.date: 05/05/2017
ms.author: ruimelo
author: ruimelo
---

> 
> #**THIS IS DRAFT.1 - WORK IN PROGRESS **
> 

# Manage database upgrades

Are you planning to upgrade your production database? You probably have a few questions, such as:

- How can I include my databases in the DevOps process?
- How can I automate the database upgrades?
- How can I overcome known challenges and risks?

This topic aims to answer this and give you a few recipes to manage your upgrades.

## Automation is key

Databases are a complex set of artifacts that usually require a significant amount of effort to deploy. They evolve with your solutions, both structure and data wide. It's crucial that you include them in your DevOps process.

Automation provides a trustworthy strategy for deploying change. It promotes consistency, improves traceability, removes human error, and enables your database to mature with your solution.

## Considerations

Databases present a unique set of upgrade challenges. With other artifacts, for example web services or web applications, you can use clusters and load balancing to deploy to a subset of servers. Let's explore some of the considerations you need to consider when planning your database upgrade, such as:

- Dealing with multiple environments
- Deploying schema and data
- 24x7 availability
- Backwards compatibility
- Database recovery

### Dealing with multiple environments

Your databases may contain different data for each environment.

- **Users accessing the databases** - it's typical for applications to be implemented in segregated environments, using different domains, and enforcing  access.
- **Environment specific configuration data** - configuration data, for example web services endpoints and linked server destinations, may be stored in the databases, and require different values in each environment.

### Deploying schema and data

When updating your database, you could deploy schema and data changes.

- **Modify the database schema** - add new tables, append columns to tables, or create and update indexes.
- **Creating and updating data** - insert new data into tables, update existing data, and validate that data has been correctly modified.

### 24x7 availabiltity

Deploying database changes to high-availability and critical systems, for example financial or military systems, is a challenge.

- **Downtime has significant impact** - user dissatisfaction or worse, a sense of distrust in the platform. 
- **Backups and restore are not a recovery option** - every action must be part of a forward moving process.

### Backward compatibility

It's likely that your databases need to support multiple versions of your solution. You need to maintain backward compatibility with all existing versions and support recovery for each.

### Database recovery

When something goes terribly wrong, for example data corruption, it's important that you're able to recover your database and data. You typically roll-forward by performing operations that restore previous version of your database, undo and validate data changes.

For example, a change may require a column to change its type. Your roll-forward strategy could be to create a new column with the new type, cast the old column values to the new type, and fill update the new column.

- **If you never delete the old column** - delete only the new column and revert any code (for example views and store procedures) which refers to the new column. This scenario becomes complex if new values are added to the new column during the roll-forward.
- **If you delete the old column** - re-create the old column and cast the values back. Once again, the scenario becomes complex if new values are added to the new column, risking cast back failure to the old column.

## Solutions

Based on the considerations we covered, let's look at some of the solutions you can consider to automate the deployment of your database.

- Data-Tier Applications
- Custom approaches
	- Manually generate scripts	14
	- Version databases and script differences
	- Build different versions of databases and script differences
	- Use Red Gate data tools

### Data-Tier Applications

A data-tier application (DAC) is a logical database management entity that defines all the artifacts contained in the database. For example: tables, views, stored procedures and login objects. You use a portable package (DACPAC) to deploy schema changes, or a @ (BACPAC) to deploy schema and data changes. (For more information, read [data-tier applications](https://docs.microsoft.com/en-us/sql/relational-databases/data-tier-applications/data-tier-applications).)

### Custom approaches
@

#### Manually generate scripts
@

#### Version databases and s@cript differences
@

#### Build different versions of databases and script differences
@

#### Use Red Gate data tools
@

##Reference information
- [Rollbacks with Automated Database Deployments](http://www.codeaperture.io/2016/09/18/rollbacks-with-automated-database-deployments/)
- [Avoiding Database Migration Pitfalls with Continuous Software Delivery](https://devops.com/avoiding-database-migration-pitfalls-with-continuous-software-delivery/)
- [Closing the Gap Between Database Continuous Delivery and Code Continuous Delivery](https://devops.com/closing-gap-database-continuous-delivery-code-continuous-delivery/)
- [How to Automate the Database for DevOps Success](https://blog.xebialabs.com/2016/11/03/devops-database-automation-yes-you-can/)
- [How Database Administration Fits into DevOps](https://www.infoq.com/news/2016/01/database-administration-devops)
- [How Do Databases Fit Into DevOps?](https://www.devopsguys.com/2015/02/19/how-do-databases-fit-into-devops/)
- [Redgate Data Tools in Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/03/07/redgate-data-tools-in-visual-studio-2017/)
- [Using Visual Studio database projects in real life](https://weblogs.asp.net/gunnarpeipman/using-visual-studio-database-projects-in-real-life)

> Authors: Rui Carrilho de Melo, Rodrigo Antunes, João Paulo Rodrigues | Find the origin of this article and connect with the ALM Rangers [here](https://github.com/ALM-Rangers/Guidance/blob/master/README.md)
 
*(c) 2017 Microsoft Corporation. All rights reserved. This document is
provided "as-is." Information and views expressed in this document,
including URL and other Internet Web site references, may change without
notice. You bear the risk of using it.*

*This document does not provide you with any legal rights to any
intellectual property in any Microsoft product. You may copy and use
this document for your internal, reference purposes.*