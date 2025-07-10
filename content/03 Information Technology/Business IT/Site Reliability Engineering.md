[Google SRE - What is Toil in SRE: Understanding Its Impact](https://sre.google/sre-book/eliminating-toil/)
[Google SRE - System Design: Non-Abstract Large System Design](https://sre.google/workbook/non-abstract-design/)

# What Is NALSD?

This chapter presents a NALSD approach: we begin with the problem statement, gather requirements, and iterate through designs that become increasingly sophisticated until we reach a viable solution. Ultimately, we arrive at a system that defends against many failure modes and satisfies both the initial requirements and additional details that emerged as we iterated.

NALSD describes a skill critical to SRE: the ability to assess, design, and evaluate large systems. Practically, NALSD combines elements of capacity planning, component isolation, and graceful system degradation that are crucial to highly available production systems. Google SREs are expected to be able to start resource planning with a basic whiteboard diagram of a system, think through the various scaling and failure domains, and focus their design into a concrete proposal for resources. Because these systems change over time, it’s vitally important that an SRE is able to analyze and evaluate the key aspects of the system design.

# Why “Non-Abstract”?

All systems will eventually have to run on real computers in real datacenters using real networks. Google has learned (the hard way) that the people designing distributed systems need to develop and continuously exercise the muscle of turning a whiteboard design into concrete estimates of resources at multiple steps in the process. Without this rigor, it’s too tempting to create systems that don’t quite translate in the real world.

This extra bit of work up front typically leads to fewer last-minute system design changes to account for some unforeseen physical constraint.

Please note that while we drive these exercises to discrete results (e.g., number of machines), examples of sound reasoning and assumption making are more important than any final values. Early assumptions heavily influence calculation results, and making perfect assumptions isn’t a requirement for NALSD. The value of this exercise is in combining many imperfect-but-reasonable results into a better understanding of the design.

# What Qualifies as Engineering?

Engineering work is novel and intrinsically requires human judgment. It produces a permanent improvement in your service, and is guided by a strategy. It is frequently creative and innovative, taking a design-driven approach to solving a problem—the more generalized, the better. Engineering work helps your team or the SRE organization handle a larger service, or more services, with the same level of staffing.

Typical SRE activities fall into the following approximate categories:

**Software engineering**

Involves writing or modifying code, in addition to any associated design and documentation work. Examples include writing automation scripts, creating tools or frameworks, adding service features for scalability and reliability, or modifying infrastructure code to make it more robust.

**Systems engineering**

Involves configuring production systems, modifying configurations, or documenting systems in a way that produces lasting improvements from a one-time effort. Examples include monitoring setup and updates, load balancing configuration, server configuration, tuning of OS parameters, and load balancer setup. Systems engineering also includes consulting on architecture, design, and productionization for developer teams.

**Toil**

Work directly tied to running a service that is repetitive, manual, etc.

**Overhead**

Administrative work not tied directly to running a service. Examples include hiring, HR paperwork, team/company meetings, bug queue hygiene, snippets, peer reviews and self-assessments, and training courses.

# Is Toil Always Bad?

Toil doesn’t make everyone unhappy all the time, especially in small amounts. Predictable and repetitive tasks can be quite calming. They produce a sense of accomplishment and quick wins. They can be low-risk and low-stress activities. Some people gravitate toward tasks involving toil and may even enjoy that type of work.

Toil isn’t always and invariably bad, and everyone needs to be absolutely clear that some amount of toil is unavoidable in the SRE role, and indeed in almost any engineering role. It’s fine in small doses, and if you’re happy with those small doses, toil is not a problem. Toil becomes toxic when experienced in large quantities. If you’re burdened with too much toil, you should be very concerned and complain loudly. Among the many reasons why too much toil is bad, consider the following:

**Career stagnation**

Your career progress will slow down or grind to a halt if you spend too little time on projects. Google rewards grungy work when it’s inevitable and has a big positive impact, but you can’t make a career out of grunge.

**Low morale**

People have different limits for how much toil they can tolerate, but everyone has a limit. Too much toil leads to burnout, boredom, and discontent.

Additionally, spending too much time on toil at the expense of time spent engineering hurts an SRE organization in the following ways:

**Creates confusion**

We work hard to ensure that everyone who works in or with the SRE organization understands that we are an engineering organization. Individuals or teams within SRE that engage in too much toil undermine the clarity of that communication and confuse people about our role.

**Slows progress**

Excessive toil makes a team less productive. A product’s feature velocity will slow if the SRE team is too busy with manual work and firefighting to roll out new features promptly.

**Sets precedent**

If you’re too willing to take on toil, your Dev counterparts will have incentives to load you down with even more toil, sometimes shifting operational tasks that should rightfully be performed by Devs to SRE. Other teams may also start expecting SREs to take on such work, which is bad for obvious reasons.

**Promotes attrition**

Even if you’re not personally unhappy with toil, your current or future teammates might like it much less. If you build too much toil into your team’s procedures, you motivate the team’s best engineers to start looking elsewhere for a more rewarding job.

**Causes breach of faith**

New hires or transfers who joined SRE with the promise of project work will feel cheated, which is bad for morale.

# Conclusion

If we all commit to eliminate a bit of toil each week with some good engineering, we’ll steadily clean up our services, and we can shift our collective efforts to engineering for scale, architecting the next generation of services, and building cross-SRE toolchains. Let’s invent more, and toil less.