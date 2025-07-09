---
title: Shared Responsibility Model
---
The **Shared Responsibility Model** defines **who handles what** in cloud security:

The line between responsibilities **shifts** depending on the **cloud service model** you're using: **SaaS, PaaS, IaaS**.

- **Cloud provider**: Secures the infrastructure.
- **You (the customer)**: Secures your usage — data, access, config.

#### Who's Responsible for What?

| Service Model | Provider Handles              | You Handle                                      |
| ------------- | ----------------------------- | ----------------------------------------------- |
| **SaaS**      | Infra, app, OS, runtime       | Users, data, permissions, configs               |
| **PaaS**      | Infra, OS, runtime            | App code, data, IAM, environment settings       |
| **IaaS**      | Infra, networking, hypervisor | OS patching, firewall, data, access, monitoring |
#### Further Resources:
https://learn.microsoft.com/en-us/azure/security/fundamentals/shared-responsibility
https://learn.microsoft.com/en-us/azure/security/fundamentals/shared-responsibility-ai
