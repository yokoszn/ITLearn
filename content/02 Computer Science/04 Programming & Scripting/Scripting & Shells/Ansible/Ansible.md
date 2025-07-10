---
title: Ansible
---
- **Purpose**: Configuration management and orchestration tool.
- **Usage**: Ideal for automating the setup, configuration, and management of infrastructure, including servers, applications, and services across multiple environments.
- **Interaction**: Ansible can be used to:
    - Automate the installation of **Docker** and deployment of services.
    - Configure services within **Kubernetes** clusters.
    - Work with **Terraform** to handle post-infrastructure setup tasks, such as installing and configuring software on provisioned VMs or cloud instances.

[Ansible](http://ansible.com) is a configuration management, deployment, and remote execution tool that uses SSH to address remote machines (though it offers other connection types, including 0mq). It requires no server software nor any remote programs, and works by shipping small modules to remote machines that provide idempotent resource management. While implemented in Python, Ansible uses a basic YAML data language to describe how to orchestrate operations on remote systems.

Ansible can be extended by writing modules in any language you want, though there is some accelerated module writing ability that makes it easier to do them in Python.

To prevent documentation drift, see [Ansible documentation site](http://docs.ansible.com).