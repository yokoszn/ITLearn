---
title: Puppet Agent & Master Communication
---
Before being applied, manifests get compiled into a document called a “catalog”, which only contains resources and hints about the order to sync them in. With puppet apply, the distinction doesn’t mean much.

In a master/agent Puppet environment, though, it matters more, because agents only see the catalog.

Running Puppet in agent/master mode works much the same way, the main difference is that it moves the manifests and compilation to the puppet master server. Agents don’t have to see any manifest files at all, and have no access to configuration information that isn’t in their own catalog.

How Do Agents Get Configurations ?

Puppet’s agent/master mode is pull-based. Usually, agents are configured to periodically fetch a catalog and apply it, and the master controls what goes into that catalog.

By using this logic, manifests can be flexible and describe many systems at once. A catalog describes desired states for one system. By default, agent nodes can only retrieve their own catalog and they can’t see information meant for any other node. This separation improves security.

This way, one can have many machines being configured by Puppet, while only maintaining our manifests on one (or a few) servers.