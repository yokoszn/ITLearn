---
title: Configuration Management
---
[[Configuration Management 101]]
[[Configuration Management 201]]

## A Brief History of Configuration Management[¶](https://www.opsschool.org/config_management.html#a-brief-history-of-configuration-management "Link to this heading")

Configuration management as a distinct sub-discipline of operations engineering has roots in the mid-1990s. Prior to then, even sites with a large number of users like universities and large ISPs had relatively few Unix systems. Each of those systems was generally what today’s operations community calls a “snowflake system” (after the phrase “a precious and unique snowflake”). They were carefully hand-built to purpose, rarely replaced, and provided a unique set of services to their users.

The rise of free Unix-like Operating Systems and commodity x86 hardware, coupled with the increasing demands to scale booming Internet services meant the old paradigms of capturing configuration were no longer adequate. Lore kept in text files, post-bootstrap shell scripts, and tales told around the proverbial campfire just didn’t scale. Administrators needed automation tools which could stamp out new machines quickly, plus manage configuration drift as users made changes (deliberately or accidentally) that affected the functioning of a running system.

The first such tool to gain prominence was CFEngine, an open-source project written in C by Mark Burgess, a CS professor at Oslo University. CFEngine popularized the idea of _idempotence_ in systems administration tasks, encouraging users to describe their system administration tasks in ways that would be convergent over time rather than strictly imperative shell or perl scripting.

```
Todo

a specific example of convergent over time might help
```
In the early 2000s, the systems administration community began to focus more intensely on configuration management as distributed systems became both more complex and more common. A series of LISA papers and an explosion in the number and sophistication of open-source tools emerged. Some highlights and background reading:

- Steve Traugott’s isconf3 system and paper [“Bootstrapping an Infrastructure”](http://www.infrastructures.org/papers/bootstrap/bootstrap.html) provided a concrete model for repeatable, scalable provisioning and config management.
    
- CERN released and wrote about [Quattor](http://quattor.org/index.html) which they used to build and administer high-performance compute clusters at larger scale than most sites at the time had dealt with.
    
- Alva Couch from Tufts University and Paul Anderson from University of Edinburgh, laid out theoretical underpinnings for configuration management in a [joint session at LISA’04](http://static.usenix.org/event/lisa04/tech/talks/couch.pdf)
    
- Narayan Desai’s [bcfg2 system](http://bcfg2.org) provided a hackable Python CM project with early support for advanced features like templating and encrypted data
    
- Recapitulating Luke Kanies’ [departure from cfengine](http://rootprompt.org/article.php3?article=10981) to start Puppet, Adam Jacob created Chef in 2008 to address [fundamental differences](http://www.akitaonrails.com/2009/11/18/chatting-with-adam-jacob) with Puppet (primarily execution of ordering and writing user code in Ruby vs a DSL).
    

By 2008, provisioning and configuration management of individual systems were well-understood (if not completely [“solved”](http://blog.lusis.org/blog/2011/08/22/the-configuration-management-divide/)) problems, and the community’s attention had shifted to the next level of complexity: cross-node interactions and orchestration, application deployment, and managing ephemeral cloud computing instances rather than (or alongside) long-lived physical hardware.

A new crop of CM tools and approaches “born in the cloud” began to emerge in the 2010s to address this shift. SaltStack, Ansible, and Chef-v11 built on advances in language (Erlang and Clojure vs Ruby and Python), methodology (continuous deployment and orchestration vs static policy enforcement), and the component stack (ZeroMQ and MongoDB vs MySQL).

Whatever specific configuration management tooling operations engineers encounter as an operations engineer, ultimately the technology exists to enable business goals – short time-to-restore in the face of component failure, auditable assurance of control, low ratio of operators per managed system, etc. – in a world whose IT systems are moving, in the words of CERN’s Tim Bell, “from pets to cattle”.