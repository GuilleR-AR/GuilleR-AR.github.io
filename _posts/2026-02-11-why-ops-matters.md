---
layout: post
title: OPS Role in the Company
subtitle: What we bring to the table
tags: [opinion]
comments: true
mathjax: true
author: Guille R
---

| ⚠️ DISCLAIMER                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| My intent with writing this is to help breaking some preconceptions of the role itself, it is not looking to rant against some role in particular and looks to shed some light on it to start making some much needed change |


# Intro

A bit of context on why I decided to write this post: after joining new Ops teams and during interviews, I've often noticed our role is misunderstood. The overall impression from some managers on other teams—and sometimes even from our own Ops managers—is that we are mainly gatekeepers who enforce order above all else. That isn't the whole picture. I'll try to define, from my perspective, what Ops is really about.


# What is Ops?

Defining the Ops role can seem simple but is often confusing. When I explain what I do to people outside the field, it's not always easy. A useful analogy is this: if developers design the plane, Ops are the ground crew and the air traffic controllers who make sure it doesn't crash and that it reaches its destination. It's a helpful comparison, but incomplete. Put another way, Ops is primarily a support function—a behind-the-scenes role where we operate in the background and are often taken for granted until something breaks.
If we go about it in more detail, here are some of the tasks we are often trusted upon:
- Maintance of the configuration of servers in the Cloud or on-prem:
    This is often done at a large scale and we seek to automate and standarize all servers to simplify the workload and to help with predictibiliy of them
- Internal tools support and configuration:
    There are multiple tools or services to be able to deploy an application on production, beign servers in the cloud, a place where the code gets stored, CI-CD platforms, authentications, monitoring, etc. These can be selfhosted or PaaS, depending on the org and devops team size. 

- Provide access to different environments and tools:
    Providing access to the right environment and tools, this sounds simple enough, but it is a bit more complicated since if everyone has access to everything with admin access it is bound to have issues.
  
- Production reliability:
    Depending on the company's culture the resolution of a prod incident might fall on the developers or ops, regardless of this OPS is the responsible of keeping the service up for customers.

- Monitoring and alerting:
    Setting up alerts that can predict when a service is going to have issues or is currently experiencing it 

- Security:
    Even though many companies often have a security team, the implementation of fixes tends to fall on the ops team for services, configurations and permissions. If there isn't a dedicated security team sometimes this gets absorved by OPS.


# Who is Ops?

A key trait for anyone in Ops is flexibility: the ability to use tools you didn't build yourself. While many Ops tools involve code (scripting, Infrastructure as Code, automation), the core strength of Ops is jumping into an unfamiliar problem and making progress quickly. That requires humility, curiosity, and persistence—admitting you don't know something, researching it, learning, and following through until it's resolved. To summarize: Devs write the code; Ops provide and operate the tools, platforms, and processes that run that code.


# Why Ops Matters?
When Ops does its job well, most people don't notice — but we're the first to be called when things fail. This isn't a request for praise; it's meant to highlight why the role deserves more recognition. Good Ops work reduces downtime, enables faster delivery, and helps teams move confidently.
Another important point is that DevOps engineers often support multiple teams. A problem one team encounters will likely affect others, so an infrastructure or deployment issue a developer faces may already have been solved by the DevOps team.

# Conclusion

This is just my Point of View of the purpose of my role, not sure if it is all that accurate, specially because I'm probabbly a better DevOps than a writer, but regardless of that it is just food for thought and maybe next time you interact with someone from the Ops department some of these things come to mind. 

### Final Advise

Please if you create a ticket make sure to include all the relevant information without us asking, I'll guarantee they will be answered faster and we will take it more seriously. 