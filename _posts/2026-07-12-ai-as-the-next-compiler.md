---
layout: post
title: AI as the next compiler
tags: [ai engineering-leadership compilers specification-driven-development vibe-coding rust abstraction ai-agents llm technology professional-growth]
image: /public/images/zambezi-river-zambia-april-2026.png
description: AI is the next compiler evolution — a framework for engineers to embrace AI as a co-pilot while remaining the critical system architect, anchored in specification-driven development.
image-caption: Zambezi River, Zambia, April 2026 @babafemio
---

Let's start with the unvarnished truth: the AI conversation feels less like a technology discussion and more like a professional crisis.

<!--more-->

As engineers, we are asking the same question: 

* Is AI taking my job, or is it fundamentally redefining it?
* How are we supposed to process the sheer shock of it?
* And what do we make of "vibe coders?" The thought that what used to take months of dedicated effort can now be churned out in days, sometimes by people who haven’t accumulated a fraction of the experience we have?

To help resolve these questions, not just for myself but also as we build our AI strategy framework at [Interswitch Group](https://interswitchgroup.com/){:target="_blank"}, I immersed myself and took a course on "vibe coding." (Yes, there is a course on it on [O'Reilly](https://www.oreilly.com/live-events/vibe-coding-for-problemsolvers/0642572202071/){:target="_blank"}!)

To be fair, the instructor warned that you shouldn't deploy AI output directly into production. But he did mention a spectrum: as Generative AI models get better, the line between "fun experiment" and "safe, deployable production code" is getting terrifyingly thin.

So I put it to the test. I started building a personal tool, an email agent in Rust, a modern programming language I’ve been fascinated by because of its performance and my background in C/C++. Through this exercise, I learned not just about AI, but that software development is not merely evolving; it is radically ascending.

## Understanding AI as the next compiler

This process reminds me that programming has always been about abstraction. We moved from punch cards to Assembly, then to high-level languages. [The birth of Fortran](https://www.ibm.com/history/fortran){:target="_blank"}, IBM's account of how the first commercial compiler brought **high-level languages** to the masses captures this arc vividly. Now we have moved to human-level languages, and the "compiler" is hosted by your current inference provider. Similarly, software engineers once worked at a terminal and submitted “jobs” to the mainframe computer.

Right now, most of us feel like we’re back in the era when Assembly language was king, and programming languages like C and BASIC came on the scene. We are witnessing a Cambrian explosion of power, in which someone (maybe not a seasoned expert) can build in weeks what once took a dedicated team years.

And ironically, software engineers have always been looking for ways to simplify work and improve productivity. When Unix was first being written in Assembly, they were realising they wouldn't live very long if life continued at that pace. As soon as the first mature C compiler emerged, the need for Assembly *vanished after the C compiler itself was rewritten in C*.

But here is the truth that cannot be abstracted away: **the engineer who deeply understands the low-level nuances and the core principles will always build the best-performing, most reliable software.**

## Experience remains the bottleneck

I learned this the hard way on my personal project. Even with a beautifully crafted prompt, the AI model did not build the best software. The first pass was riddled with technical debt. It didn't inherently care about performance or best practices, let alone robust, secure coding standards.

I had to *carefully* challenge its decisions and continually recommend stronger, more refined approaches. My experience, judgment, and taste guided the tool until we both agreed it was genuinely well-built.

Don't get me wrong; humans cannot match the compressed knowledge of a modern LLM's syntax and nuanced understanding. But what we do possess is the ability to enforce system design, manage complexity, and understand the *why* behind the code, not just the *how*.

And while we love the idea of outsourcing the grunt work such as documentation, boilerplate, and endless unit tests, our value remains in understanding those systems deeply enough to critique the AI's output.

## The engineer’s mandate

We need our most experienced engineers to do one thing: **embrace AI and regard it as the next evolution of the compiler.**

The world needs robust, reliable software more than ever, especially now that anyone can generate code. Our role is evolving from simply producing code to ensuring the overall quality and reliability of entire systems. Embrace a mindset of empowered responsibility. AI is your co-pilot, but you remain the Captain.

Here is a framework to get started and reclaim your role as the critical system thinker:

1. **Identify a "pet” project:** Choose a system or utility you've always wanted to build but never had the time for. This project should require more than just prompt-feeding; it should require design.
2. **Lead with specification, not code:** Don't ask the AI to build the project; ask it to help you build the spec. Use AI to generate a detailed specification document using Specification-Driven Development (SDD). This forces iteration through every requirement and turns the AI into a thinking partner, while you remain the architect. Crucially, prompt it to include the necessary tests and security checks at this stage.
3. **Iterate and elevate:** Ask the AI to implement the solution, but do it piece by piece. Treat it like an Agile sprint: get a solid, testable foundation before moving on.
4. **Systematise or scale the gain:** Once you have a working prototype, ask yourself: *How can the architecture or the process used here improve a product or service in my day job?*

The goal is not to write fewer lines of code, but to elevate the quality and reliability of the solutions we deliver. Embrace AI not just as a productivity hack, but as the engine for the next generation of robust, thoughtful software.

Let’s build. 
