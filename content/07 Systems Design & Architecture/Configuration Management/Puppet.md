---
title: Puppet
---
As system administrators acquire more and more systems to manage, automation of mundane tasks is increasingly important. Rather than develop in-house scripts, it is desirable to share a system that everyone can use, and invest in tools that can be used regardless of one’s employer. Certainly doing things manually doesn’t scale.

This is where Puppet comes to rescue. Puppet is a Configuration Management Tool. It is a framework for Systems Automation. An OpenSource software written in Ruby that uses Declarative Domain Specific Language (DSL).

Puppet usually uses an agent/master (client/server) architecture for configuring systems, using the Puppet agent and Puppet master applications. It can also run in a self-contained architecture, where each managed server has its own complete copy of your configuration information and compiles its own catalog with the Puppet apply application.

### [[Puppet Agent & Master Communication]]

### Manifests[](https://www.opsschool.org/config_management.html#manifests "Link to this heading")

Puppet programs are called “manifests”, and they use the .pp file extension. These programs comprise of resource declarations, described below.

### Resources[](https://www.opsschool.org/config_management.html#resources "Link to this heading")

System’s configuration can be imagined as a collection of many independent atomic units, called “resources”.

Example of puppet resouces can be a specific file, a directory, a service.

### Anatomy of a Resource[](https://www.opsschool.org/config_management.html#anatomy-of-a-resource "Link to this heading")

In Puppet, every resource is an instance of a resource type and is identified by a title, it has a number of attributes (which are defined by the type), and each attribute has a value.

Puppet uses its own language to dsecribe and manage resources:

type { 'title':
   argument  => value,
   other_arg => value,
}

This syntax is called a resource declaration.

Example of file resource type.

file{ '/tmp/example':
  ensure   => present,
  mode     => '600',
  owner    => 'root',
  group    => 'hosts',
}

### Resource Type[](https://www.opsschool.org/config_management.html#resource-type "Link to this heading")

As mentioned above, every resource has a type.

Puppet has many built-in resource types, and you can install even more as plugins. Each type can behave a bit differently and has a different set of attributes available.

The full list of different puppet resource types can be found at the [Puppet Type Reference](http://docs.puppetlabs.com/references/latest/type.html).

### Puppet Apply[](https://www.opsschool.org/config_management.html#puppet-apply "Link to this heading")

It is used below to test small manifests, but it can be used for larger jobs too. In fact, it can do nearly everything an agent/master Puppet environment can do.

‘apply’ is a Puppet subcommand. It takes the name of a manifest file as its argument, and enforces the desired state described in the manifest.

Try applying the short manifest above:

puppet apply /root/examples/file-1.pp
notice: /Stage[main]//File[testfile]/ensure: created
notice: Finished catalog run in 0.05 seconds

### Package/File/Service[](https://www.opsschool.org/config_management.html#package-file-service "Link to this heading")

The package/file/service pattern is one of the most useful idioms in Puppet. This is a pattern constantly seen in the production Puppet code.

Below is an example of a manifest that uses this pattern to install and configure ssh for Enterprise Linux - based Linux systems.

package { 'openssh-server':
  ensure => present,
  before => File['/etc/ssh/sshd_config'],
}
file { '/etc/ssh/sshd_config':
  ensure => file,
  mode => 600,
  source => '/root/examples/sshd_config',
}
service { 'sshd':
  ensure => running,
  enable => true,
  subscribe => File['/etc/ssh/sshd_config'],
}

The package resource makes sure the software and its config file are installed, the config file depends on the package package resource, and the service subscribes to the changes in the config file.
