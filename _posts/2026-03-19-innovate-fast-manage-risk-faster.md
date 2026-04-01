---
layout: post
title: Innovate fast, manage risk faster
tags: technology security ai ai-tools opencode privacy risk-management llm ai-agents data-security free-tier hidden-costs
image: /public/images/charles-bridge-museum-prague-january-2026.png
description: Exploring the tension between rapid AI innovation and security, revealing how free AI tools can expose your system to unexpected data collection risks.
image-caption: Charles Bridge Museum, Prague, January 2026 @babafemio
---

So, in the spirit of experimenting with some of the tools I have been reading about and their amazing capabilities, I installed Opencode over the weekend. While I struggled to get my local LLMs to perform, in frustration, I selected "Kimi2.5 Free" and asked it to build a website I was working on, and I had spent some time preparing a PLAN.MD file for. The process ran for about 30 minutes, and in the end, it created a complete website with made-up content that was compelling enough to go live with. But during the process, I noticed something: it was running commands in the shell of my laptop and using the results to determine new steps to take, and all... 

All this was very interesting.

<!--more-->

But I started getting curious about the free model I was using and checked out the documentation and pricing on Opencode, and I saw that the same Kimi2.5 had a price tag of $0.60/3.00 (input/output) per million tokens, but there was still a free one, so I kept looking. So, at the bottom of the page was an explanation about the Kimi2.5 Free option. It said the model would be available for a limited time and that the model provider was using the free tier to gather feedback to improve the model. And I thought, interesting, again!

Later on, when I was thinking about what I had achieved and which inference provider I should pitch my tent with for the big tasks my home AI rig cannot handle [yet], it just dawned on me that I was actually paying for the "free" model. Still, I was paying with data from my laptop. I then remembered all those commands it was running and shipping the output of "ls" to only God knows where. Nothing was stopping it from running "ifconfig", "ps ax", or God forbid, downloading malware that would provide it with a constant stream of data from my computer...

For now, no more free. I need to conduct serious due diligence to choose the right inference platform while I continue building out my home lab to handle larger models.

Stay safe out there.
