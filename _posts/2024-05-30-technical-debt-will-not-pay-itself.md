---
layout: post
title: Technical debt will not pay itself
tags: technical debt engineering culture architecture
image: /public/images/disneyland-paris-april-2023.png
description: Discover how to manage technical debt effectively in software development. Learn strategies to balance short-term gains with long-term code quality and sustainability
image-caption: Disneyland Paris, April 2023. @babafemio
---

In software development, technical debt refers to the future cost incurred when choosing an easy solution now instead of using a better approach that would take longer. Every software product engineering effort accumulates technical debt. A software product rarely comes out as we envisioned it the first time. We start with what is very clear to us, what is achievable with our resources, and within the time constraints we have to go the market. As a result, we make compromises, not shortcuts, but well-thought-out trade-offs to enable us to get to the point where we can ship the product. Many quotes encourage us to do this, and rightfully so: "Perfect is the enemy of the good," "Revenue delayed is revenue not earned," and so on come to mind very quickly. While these trade-offs are necessary, they lead to the inevitable accumulation of technical debt.

<!--more-->

Technical debt is that shadowy figure in the distance, always looming and growing with every new technical decision you make. Similar to mounting credit card bills leading to compounding interest and financial strain, it's an inescapable reality, but it is not the problem. The real challenge for software teams is determining who pays, how it will be paid, and when it will be paid down. 

### Who pays?
The question of who pays for technical debt is straightforward, even though teams sometimes expect it to simply vanish. Technical debt will only disappear with a deliberate effort to address it. If a team tries to resolve inefficient code by adding more computing resources, they are not paying down technical debt; they are merely increasing costs unnecessarily when they could be saving costs. Effective management of technical debt requires the product team to take responsibility. 

Creating a separate team solely responsible for managing technical debt may seem like a sensible solution. But when technical debt becomes someone else's problem, developers may feel less accountable for the quality of their code and more inclined to take shortcuts (real ones, this time) or prioritize short-term outcomes over long-term maintainability of the codebase. Therefore, creating a separate team for this 'dirty work' can inadvertently encourage the accumulation of more debt and foster poor software engineering practices and is not recommended.

>We start with what is very clear to us, what is achievable with our resources, and within the time constraints we have to go the market. As a result, we make compromises, not shortcuts, but well-thought-out trade-offs to enable us to get to the point where we can ship the product

### How do we pay?
Understanding how to tackle technical debt requires recognizing its diverse origins, some of which may come as a surprise. The most overlooked one is the good old passage of time. As software libraries evolve to patch up performance issues and security vulnerabilities, the version you have implemented in your code has inevitably become outdated. And not because software decays (thankfully!). Another form of technical debt arises when you choose not to over-engineer the product initially at high costs, instead sensibly choosing to enhance the architecture as the product achieves success over time and not do it. When code is poorly written or has inherent inefficiencies because it was expedient at the time. Those quick fixes and temporary workarounds linger and create additional layers of technical debt, which keep building up. Finally, if your team makes a significant technology architecture decision and platform, you will have technical debt in all products on the old platform.

In the end, technical debt isn't just about bad code—it's a mix of evolving technology, architectural decisions, rushed code, quick fixes, and the occasional major revamp. Understanding these sources is critical to addressing technical debt and keeping your codebase fresh. For example, once it becomes clear that your framework is outdated, schedule the work to do the upgrades. Similarly, plan to evolve the architecture and implement it if you have chosen to go with a simple architecture to start, and the product begins to groan under the weight of its success. This is the way.

>Similar to mounting credit card bills leading to compounding interest and financial strain, it's an inescapable reality, but it is not the problem. The real challenge for software teams is determining who pays, how it will be paid, and when it will be paid down. 

### When do we pay?
In this article, we assume there is a consensus that we must address technical debt. We understand that paying it off can lead to cost savings, productivity improvements, and increased revenues. So, the next question is when should we tackle it? Deciding when to address technical debt is challenging because we are constantly faced with conflicting priorities and limited resources. This dilemma is one of the most significant debates within product teams: Should we add new features or upgrade our development framework version? Should we enhance the UI to entice and attract more users or improve the database architecture to prevent crashes when the user base grows? 

Balancing immediate business needs with long-term technical health is tricky but crucial. For example, adding a highly requested feature might drive new income in the short term. However, ignoring an outdated platform or framework could lead to more severe issues down the line, such as system failures or security vulnerabilities. To make informed decisions, product teams should evaluate the impact of technical debt on their current operations and future scalability. Tools like cost-benefit analysis can help product teams make informed decisions and prioritize tasks effectively. For instance, if slow performance due to technical debt is causing customer churn, addressing this issue should take precedence. On the other hand, if the technical debt is not immediately impacting the user experience, it might be feasible to schedule the repayment alongside new feature development. To make this real and effective, you must put the improvement efforts on the roadmap and stick to the timelines.

>Creating a separate team for this 'dirty work' can inadvertently encourage the accumulation of more debt and foster poor software engineering practices and is not recommended

In conclusion, paying down technical debt is not a one-time event but an ongoing journey that requires commitment, collaboration, and some investment. That last part is critical because being intentional about addressing technical debt requires investment in time and resources. By prioritizing technical debt repayment and introducing architectural runway work in the backlog, product teams can build a solid foundation for future growth and innovation, ensuring the long-term success of their software products.


