---
title: Startups Playbook
tags:
  - business
  - startups
  - infrastructure
  - learning-path
draft: false
---

# Startups Playbook Learning Path

Master the decisions that determine whether your startup controls its own destiny. This path takes you from "we need a tech stack" to a self-hosted, sovereign, scalable business — without surrendering your data or budget to SaaS incumbents.

## 📋 Overview

**Duration:** 6–10 weeks (self-paced)
**Level:** Intermediate
**Prerequisites:** Basic Linux familiarity, general comfort with technology

**Why this matters:** Most startup guides assume you'll use Stripe Atlas + AWS + Notion + Slack + whatever the current SaaS darling is. That's fine until the pricing changes, the platform sunsets, or you need to move. This path teaches you to build with open-source tools that you own, on infrastructure you control, in ways that keep your options open.

## ✅ Prerequisites

Before starting this path, you should:
- [ ] Understand basic Linux command line (files, services, SSH)
- [ ] Know what a server is and roughly how HTTP works
- [ ] Have access to a small VPS or home lab to practice on
- [ ] **Recommended:** Complete the [Linux Systems](/paths/linux) path first
- [ ] **Recommended:** Complete the [Networking Fundamentals](/paths/networking) path

## 🎯 Learning Milestones

### 🏗️ Milestone 1: Business Operating System (BOS) (Weeks 1–2)

**Goal:** Understand what a Business Operating System is, why it matters at every startup stage, and which frameworks apply to your situation.

**Core Concepts:**
- What a BOS is: the system of systems that runs your business (not just software)
- Startup stages and why your stack should match your stage (pre-revenue vs. Series A are different problems)
- Key BOS frameworks: EOS (Entrepreneurial Operating System), Holacracy, and custom hybrid approaches
- The "sovereign by default" principle: choose tools you can self-host before reaching for SaaS
- Common BOS anti-patterns: spreadsheet chaos, tribal knowledge, tool sprawl

**🛠️ Hands-on Practice:**
- [ ] Map your current (or hypothetical) business processes: what information flows where, who makes what decisions
- [ ] Identify which processes are currently handled by SaaS tools and which could be self-hosted
- [ ] Draft a one-page "business operating model" covering: how you deliver value, how you invoice, how you track work, how you communicate
- [ ] Review the TWN Systems BOS template and adapt it to a startup of your choosing

**Checkpoint:** Can you explain the difference between a BOS and a project management tool? What problem does each solve?

> [!TIP] Need guidance?
> Join [TWN Commons on Discord](https://discord.gg/kgaMm6WJya) to discuss BOS approaches and share what you're building.

**💬 Share Your Progress:** Post your one-page business operating model in the `#business-ops` channel for feedback!

---

### ☁️ Milestone 2: Infrastructure Foundations (Weeks 2–3)

**Goal:** Make informed decisions about self-hosted vs. cloud infrastructure, and understand the tradeoffs of Proxmox, Docker, and Kubernetes for different startup stages.

**Core Concepts:**
- Self-hosted vs. managed cloud: total cost of ownership, data sovereignty, operational overhead
- Proxmox VE: virtualisation platform for small-to-medium self-hosted environments
- Docker and container basics: what they solve, when they're appropriate
- Kubernetes: what problem it actually solves (and when you don't need it yet)
- Decision matrix: solo → small team → Series A and what infrastructure each stage needs
- Backup and disaster recovery as first-class requirements, not afterthoughts

**🛠️ Hands-on Practice:**
- [ ] Deploy a Proxmox VE instance (VM or bare metal) and create two VMs
- [ ] Run a containerised application with Docker Compose (e.g., Gitea or Nextcloud)
- [ ] Set up automated backups for your VM or container to an external location
- [ ] Complete the [VyOS and Proxmox Network Infrastructure](/paths/vyos-proxmox) milestone 1 if you haven't already

**Checkpoint:** For a 3-person software startup, would you recommend Proxmox + Docker or a managed Kubernetes service? Justify your answer with cost, operational complexity, and sovereignty tradeoffs.

> [!TIP] Stuck on infrastructure decisions?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#infrastructure` channel has practitioners who've made these choices — ask them what they'd do differently.

**💬 Share Your Work:** Post your Proxmox setup or Docker Compose configuration for review!

---

### 🔐 Milestone 3: Security & Identity from Day One (Weeks 3–4)

**Goal:** Implement zero-trust security and identity management before you have a breach, not after.

**Core Concepts:**
- Why "we'll add security later" is always wrong: the cost of retrofitting vs. building in
- Identity providers: Keycloak as a self-hosted alternative to Auth0/Okta
- Zero-trust networking: NetBird and WireGuard for team connectivity without VPN sprawl
- Dependency security: Dependabot and automated vulnerability scanning
- Secrets management: Vault and environment variable hygiene
- Multi-factor authentication as a baseline requirement
- ISMS (Information Security Management System) basics: what you need before you have customers

**🛠️ Hands-on Practice:**
- [ ] Deploy Keycloak and configure SSO for at least two services
- [ ] Set up NetBird to create a zero-trust overlay network for your lab environment
- [ ] Enable Dependabot (or Renovate) on a code repository
- [ ] Write a one-page security policy covering: access control, secrets management, incident response
- [ ] Complete the [NetBird VPN](/paths/netbird-vpn) path for hands-on zero-trust practice

**Checkpoint:** What's the difference between authentication and authorisation? How does Keycloak handle both?

> [!TIP] Security questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) `#security` — there are practitioners who deploy Keycloak and NetBird professionally.

**💬 Share Your Progress:** Share your security policy draft for peer review in Discord!

---

### 📊 Milestone 4: Business Operations Stack (Weeks 4–6)

**Goal:** Replace SaaS subscriptions with self-hosted business operations tools — CRM, project management, and automation.

**Core Concepts:**
- CRM options: ERPNext (full ERP + CRM) vs. Twenty (lightweight, developer-friendly) vs. managed alternatives
- Project management: Plane, Taiga, or GitLab Issues as self-hosted alternatives to Jira/Linear
- Automation: n8n as a self-hosted Zapier/Make alternative for workflow automation
- Communication: Matrix/Element for team chat, if you want to move off Slack
- Finance and invoicing: ERPNext Accounts, InvoiceNinja, or Crater
- The integration problem: how to make these tools talk to each other (hint: n8n)

**🛠️ Hands-on Practice:**
- [ ] Deploy ERPNext or Twenty and set up a basic CRM with contacts, leads, and pipeline stages
- [ ] Create an n8n workflow that connects two of your business tools (e.g., new lead → Slack notification)
- [ ] Migrate a sample dataset from a SaaS tool (CSV export) into your self-hosted alternative
- [ ] Document your business stack as a simple architecture diagram (Mermaid works well — see the [PIMPyourDocs](/business/pimpyourdocs) path)

**Checkpoint:** What's the main risk of deploying ERPNext for a 2-person startup? What would you do to mitigate it?

> [!TIP] Help with the ops stack?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#business-ops` channel includes people who've deployed ERPNext and n8n in production.

**💬 Share Your Work:** Share your n8n workflow or CRM setup in Discord for feedback!

---

### ⚖️ Milestone 5: Legal & Compliance (Weeks 6–8)

**Goal:** Understand the minimum viable legal and compliance requirements for an Australian technology startup — and build them in, not on.

**Core Concepts:**
- ABN and company structure: sole trader vs. Pty Ltd and what each means for liability
- Australian Privacy Act: what it requires, who it applies to, and how to comply from day one
- Privacy policy and Terms of Service: what they must cover, what templates you can use
- ISMS (Information Security Management System): ISO 27001 basics and what a lightweight version looks like
- Data residency: where your data lives and why Australian customers care
- Contracts: MSA (Master Services Agreement), SOW (Statement of Work), and NDA templates
- GDPR relevance: if you have EU customers or data, this applies too

**🛠️ Hands-on Practice:**
- [ ] Register an ABN (or understand the process if you already have one)
- [ ] Review an open-source Privacy Policy template and identify what you'd need to customise
- [ ] Write a one-page data handling statement: what data you collect, where it lives, who can access it
- [ ] Create a lightweight ISMS: a simple spreadsheet tracking your information assets, threats, and controls
- [ ] Review your infrastructure from Milestone 2 for Australian data residency compliance

**Checkpoint:** Under the Australian Privacy Act, what are the Notifiable Data Breach (NDB) scheme requirements? What would you do if you discovered a breach?

> [!TIP] Legal questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) to connect with practitioners who've navigated AU compliance — but always verify with a qualified legal professional for your specific situation.

**💬 Share Your Progress:** Share your data handling statement in Discord for peer review!

---

### 📈 Milestone 6: Scaling Your Stack (Weeks 8–10)

**Goal:** Understand how to right-size your systems as you grow from solo to team to Series A — without unnecessary complexity or catastrophic rewrites.

**Core Concepts:**
- The "scaling trap": over-engineering for scale you don't have yet
- When to add Kubernetes (hint: later than you think)
- Database scaling basics: when a single Postgres instance stops being enough
- Observability: logging, metrics, and alerting before something breaks in production
- Team scaling: how your BOS needs to change when you go from 2 to 10 to 50 people
- Cost management: unit economics of self-hosted vs. SaaS at different growth stages
- The exit ramp: making sure your sovereign stack can be migrated if you need to sell or merge

**🛠️ Hands-on Practice:**
- [ ] Add monitoring to your self-hosted stack (Prometheus + Grafana or Netdata)
- [ ] Set up alerting for at least one critical service (disk space, service down, response time)
- [ ] Review your current architecture and write a "what breaks first" analysis for 10x usage
- [ ] Draft a 12-month roadmap for your tech stack: what stays, what gets replaced, what gets added
- [ ] Complete the [Site Reliability Engineering](/paths/sre) path for deeper reliability engineering skills

**Checkpoint:** Your startup just closed a seed round and is hiring 5 engineers. What changes to your infrastructure, security, and BOS would you make in the first 90 days?

> [!TIP] Scaling questions?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#infrastructure` and `#business-ops` channels are full of people who've scaled self-hosted systems.

**💬 Share Your Work:** Post your 12-month roadmap for community feedback!

---

## 📚 Essential Resources

### Documentation
- [ERPNext Documentation](https://docs.erpnext.com) - Full ERP and CRM platform
- [Twenty CRM](https://twenty.com) - Lightweight, developer-friendly open-source CRM
- [n8n Documentation](https://docs.n8n.io) - Workflow automation platform
- [Keycloak Documentation](https://www.keycloak.org/documentation) - Open-source identity and access management
- [Proxmox VE Documentation](https://pve.proxmox.com/wiki/Main_Page) - Virtualisation platform
- [Australian Privacy Act](https://www.oaic.gov.au/privacy/the-privacy-act) - Official guidance from OAIC

### Tools and Software
- **ERPNext / Frappe** - Full business ERP with CRM, accounting, HR modules
- **Twenty CRM** - Lightweight alternative for smaller teams
- **n8n** - Self-hosted workflow automation (Zapier alternative)
- **Keycloak** - Identity provider and SSO platform
- **NetBird** - Zero-trust overlay network
- **Proxmox VE** - Open-source virtualisation
- **Plane / Taiga** - Project management (Jira alternatives)
- **Prometheus + Grafana** - Monitoring and observability

### Practice Labs
- **Home Lab Setup** - A $5–15/month VPS is sufficient for most milestones; a Proxmox node on a used mini-PC covers the rest
- **TWN Lab Environment** - Ask in [TWN Commons](https://discord.gg/kgaMm6WJya) about shared lab access

## 🤝 Community and Support

**[Join TWN Commons](https://discord.gg/kgaMm6WJya)** for help with:
- **#business-ops** - BOS frameworks, CRM, automation questions
- **#infrastructure** - Proxmox, Docker, Kubernetes decisions
- **#security** - Keycloak, NetBird, ISMS questions
- **#legal-au** - Australian compliance and regulatory questions (peer discussion, not legal advice)
- **#lab-help** - Assistance with hands-on exercises

**Share your progress:**
- Post architecture diagrams and configuration snippets
- Share your data handling statements and policies for peer review
- Help others who are earlier in the path

## 🌉 Bridge to TWN Systems

As you build your sovereign startup stack, you'll find TWN Systems directly useful:

> [!NOTE] Bridge to TWN
> The tools in this path are how TWN-aligned businesses operate. Find providers and tools at [TWN Systems](https://twn.systems) that support:
> - **Self-hosted infrastructure providers** who won't lock you into proprietary APIs
> - **Australian data residency options** for Privacy Act compliance
> - **Community-vetted open-source stacks** that have been tested in production

**🛠️ Connected TWN Paths:**
- **[VyOS and Proxmox Network Infrastructure](/paths/vyos-proxmox)** - The network layer under your startup stack
- **[NetBird VPN](/paths/netbird-vpn)** - Zero-trust networking for distributed teams
- **[PIMPyourDocs](/business/pimpyourdocs)** - Document your stack as you build it

## 🚀 What's Next?

After completing this path, you'll be ready for:
- **[MSP Content Model](/business/msp-content-model)** - Structure knowledge management for client-facing operations
- **[PIMPyourDocs](/business/pimpyourdocs)** - Document your stack with plain-text, git-versioned practices
- **[Site Reliability Engineering](/paths/sre)** - Deepen your reliability and scaling skills
- **[VyOS and Proxmox Network Infrastructure](/paths/vyos-proxmox)** - Go deeper on the network and virtualisation layer

## 🏆 Certification Alignment

This learning path provides practical grounding for:
- **AWS Solutions Architect** - Infrastructure and scaling concepts transfer, even though we're not using AWS
- **ISO 27001 Lead Implementer** - The ISMS milestone directly prepares for this
- **CompTIA Security+** - Security and identity concepts from Milestone 3
- **ITIL Foundation** - BOS and service management concepts

> [!TIP] Focus on Understanding, Not Certs
> The concepts in this path will outlast any specific certification. Build the understanding first; the certifications follow naturally.

---

**Ready to start?** Begin with Milestone 1 and join the [TWN Commons #business-ops channel](https://discord.gg/kgaMm6WJya) for support and community.
