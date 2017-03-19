> #**WORK IN PROGRESS** - DO NOT DISTRIBUTE
> 
> Article 2500 - 3500 words
> 
> Images - high-quality, 737 pixels wide
>
> DRAFT.1 milestone - March 31, 2017
> 
> -----------------------------------------

#Introduction

##Value for the reader to read this eBook
For many years, we've been evaluating and implementing Agile practices across our geographically distributed, part-time, and volunteer-based teams. While we shared our learnings in the [Managing Agile OSS Projects with Microsoft VSO](https://blogs.msdn.microsoft.com/microsoft_press/2015/04/09/free-ebook-managing-agile-open-source-software-projects-with-microsoft-visual-studio-online/) eBook, we realized we're not done. We need to scale, and more importantly, deliver value to our developer community quickly. 

We embarked on a cultural shift that allowed us to "rub DevOps" on our operational processes, and embrace self-organized, self-managed and autonomous teams. This article explores self-organized teams, our journey, and behavioral patterns we have observed. 

> Whether you read the entire article or cherry-pick topics, please bear in mind that there is no silver bullet, or one size fits all. The patterns and recommendations covered herein may or may not apply to your organization. If they do, we hope we'll enable a successful transformation for your teams. If not, we'd appreciate your candid feedback, so that we can update this article. 

##Value proposition
// edward
###Go straight to what worked
// edward
###Avoid the pain of what didn't work
// edward
###Road-map to create similar results in your org
// edward
##Intended audience
// edward
##Why transform?
// edward
###Part-time, geographically distributed teams
// edward
###DevOps
// edward
###Competition
// edward
###Evolution @@@NEED TO REVISE THIS HEADING FOR CLARITY @@@
// edward

##What's a ...

Teams are a grouping of individuals who are dependent on each other to pursue a common vision, achieve a common goal, and deliver a valuable solution to its users. Our teams are made up of 6-9 part-time volunteers, each with a unique set of skills and real-world experience, working together for a reasonable period, typically three to four 3-week sprints.

Before we started our transition, we relied on traditional **managed** teams. The program manager (PM) set the vision, selected the projects, and managed the unified process and all teams. The structured hierarchy relied on top-down management and bottom-up reporting between the program manager and the project leads (PL), leaving team members with limited authority.

![Managed versus self-organized teams](./_img/our-journey-of-transforming-to-a-devops-culture/our-journey-teams.png)

With **self-organized** teams, the traditional hierarchy and chain-of-command is disappearing. 

- The role of the program manager has evolved from management to enablement. 
- The project lead is still pivotal in driving the team's energy and momentum, but no longer reports to the PM.
- Each team shares the point-of-contact (PC) responsibility, enabling shared status knowledge and continuous collaboration.

###Self-organizing team?

As suggested by the [Scrum Guide](http://www.scrumguides.org/scrum-guide.html) our "*self-organizing teams choose how best to accomplish their work, rather than being directed by others outside the team*". None of our teams are the same and there is no secret sauce to become a self-organized team. 

Some key observations within our environment:

- It's not a once-off transition! We're continuously observing, learning, adapting, and evolving our environment.
- Every team member must self-organize! There is no central control or micro-management. 
- Team members must trust and respect each other! Members who are not engaged or go dark, drain the energy from self-organized teams.

###Self-managing team?

Self-managing teams not only choose how best to accomplish their work, but also how to manage their engineering process. Building upon organizational processes, these teams adapt their process within the boundary and context of their team.

Some key observations within our environment: 
- Many teams standardize on [Kanban](https://www.visualstudio.com/en-us/docs/work/kanban/kanban-basics), focusing on moving their work from left (new) to right (done), and relying on PM enablement to minimize bottlenecks. 
- Successful self-managed teams actively monitor and evolve their process. 

###Cross-functional team?

Cross-functional teams "*have all competencies needed to accomplish the work without depending on others not part of the team*" - [Scrum Guide](http://www.scrumguides.org/scrum-guide.html). Once cross-functional teams embrace self-organization and self-management, they become an inspiring autonomous team within teams.

> [!NOTE]
> 
> Mature self-organizing, self-managed, and cross-functional teams thrive on **autonomy**, **mastery**, and **purpose** as discussed in [DRiVE - by Daniel H.Pink](https://www.youtube.com/watch?v=KgGhSOAtAyQ). 

#Pillars

Our teams rely on a common infrastructure, based on [Visual Studio Team Services](https://www.visualstudio.com/team-services/), and four pillars to transition to and effectively evolve as self-organized, self-managed, and cross-functional teams. We'll refer to these pillars when we discuss patterns we have observed with our teams.

![Pillars for self-organized teams](./_img/our-journey-of-transforming-to-a-devops-culture/our-journey-pillars.png)

##Vision | Mission

Our overall goal is to *continuous delivery of value to our end users*. For each project, we define a crisp vision and a captivating mission, aligned with our overall [mission](https://aka.ms/vsarmission) statement. It's important that we create a meaningful purpose and motivation for our teams, so that everyone knows what and believes in what we're doing, and has the feeling of doing something great for the larger community.

##Framework | boundaries

Teams choose what to work on, how to best accomplish their work, and how to manage their engineering process. While this creates the ideal and effective environment for the team, it's important to create clear boundaries of responsibility, information flow, monitoring, and allowable **drift** from the overall program. Our common infrastructure enables teams to focus on their mission and learn to rely on stable progress monitoring, debt, adoption blocker, compliance, and overall program management to create stability. 

##Authority

> "*The price of greatness is responsibility*" - Winston Churchill

Autonomy, independence, and freedom comes with responsibility and accountability. We're all accountable to the community, teams we're collaborating with, and peers. We succeed or fail as a team! Responsibility and accountability is not something we can enforce or establish in a person. It's something we assume and expect from all our team members, outlined in our [manifesto](https://aka.ms/vsaraboutus) of core values.

##Reflection

In our eBook [Managing Agile OSS Projects with Microsoft VSO](https://blogs.msdn.microsoft.com/microsoft_press/2015/04/09/free-ebook-managing-agile-open-source-software-projects-with-microsoft-visual-studio-online/) we emphasized the need for continuous reflection, adaption, and improvements. It's important to continuously evolve, find ways to improve as an individual and as a greater whole. 

> "*"Information is the oxygen of the modern age. It seeps through the walls topped by barbed wire, it wafts across electrified borders.*" - Ronald Reagan

Reflection is an opportunity for all of us to inspect ourselves, plan for improvements, and share our learnings. It's a pillar that must be embraced by all stakeholders, from individual team member, to the overall program. Reflection fuels improvement and innovation if nurtured, and withers if ignored!

#Our journey

>It's important to highlight that the WHY, WHAT, WHEN is an ongoing process

##Why we transformed
// ruimelo
##When we transformed (should be when we started as transformation is ongoing)
// ruimelo
##How we transformed
// ruimelo
###Planning
// ruimelo
###Investigation
// ruimelo
###Go, Go, Go
// ruimelo
##Value ... was (is) it worth it?
// ruimelo

#Patterns
##The team that...
//?
###Goes from zero to isolated success
// willys
###Goes from zero to cross-team success
// willys
###Implodes with over-ambition
// willys
###Fizzles out over time
// willys
###Never get's started
// willys

#Continuing the transformation
##What's next?
//?
##Tools and technologies?
//?

#Transforming in your org
##Clarify the WHY you need to transform ... don't fix what's not broken
// edward
##Clarify the WHAT you need to transform
// edward
##Clarify the WHEN you will transform
// edward
##Baby steps + iterate, no big bang 
// edward

#References
- [How our community evolved](https://blogs.msdn.microsoft.com/visualstudioalmrangers/2016/09/16/how-has-the-ranger-community-evolved-over-the-past-10-years-and-whats-the-future-plan/)
- [What are self organizing teams](http://www.infoq.com/articles/what-are-self-organising-teams)
- [getKanban](https://getKanban.com)

> Authors: Edward Fry, Rui Melo, Willy Schaub
 
*(c) 2017 Microsoft Corporation. All rights reserved. This document is
provided "as-is." Information and views expressed in this document,
including URL and other Internet Web site references, may change without
notice. You bear the risk of using it.*

*This document does not provide you with any legal rights to any
intellectual property in any Microsoft product. You may copy and use
this document for your internal, reference purposes.*
