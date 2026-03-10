---
title: MSP Content Model
tags:
  - msp
  - knowledge-management
  - documentation
  - learning-path
draft: false
---

# MSP Content Model Learning Path

Structure your knowledge so your business survives staff turnover, scales with new clients, and stops depending on what lives in one person's head. This path takes you from scattered tribal knowledge to a governed, repeatable content model that makes your MSP professionally scalable.

## 📋 Overview

**Duration:** 4–6 weeks (self-paced)
**Level:** Intermediate
**Prerequisites:** Basic understanding of IT service delivery, familiarity with any documentation tool

**Why this matters:** Knowledge silos are the silent killer of MSPs. When the person who "knows everything about Client X" leaves, you lose months of context. When a new technician onboards, they drown in undocumented processes. A content model solves this by treating knowledge as a structured, governed asset — not a personal document collection.

## ✅ Prerequisites

Before starting this path, you should:
- [ ] Work in or understand an IT service delivery context (MSP, internal IT team, or similar)
- [ ] Have basic familiarity with Markdown or any structured documentation format
- [ ] Understand the difference between a process and a procedure
- [ ] **Recommended:** Complete the [PIMPyourDocs](/business/pimpyourdocs) path (or do them in parallel)

## 🎯 Learning Milestones

### 🧠 Milestone 1: Why Content Models Matter (Week 1)

**Goal:** Understand the knowledge management problem MSPs face and why a structured content model is the solution.

**Core Concepts:**
- The tribal knowledge problem: why "it's in [person's] head" is a business risk
- Knowledge silos vs. knowledge systems: the difference between storing information and making it findable and usable
- Information types in an MSP: what kinds of knowledge exist (client configs, runbooks, procedures, onboarding, sales content)
- The scalability ceiling: how unstructured knowledge limits growth
- Content model basics: what a content model is (a structured framework for organising information types and their relationships)
- Why existing tools (SharePoint, Confluence, random folders) fail without a model

**🛠️ Hands-on Practice:**
- [ ] Audit your current documentation: list every place information is stored in your organisation
- [ ] Identify 5 examples of tribal knowledge that would be lost if a key person left
- [ ] Interview a colleague about a recent incident where missing documentation caused a problem
- [ ] Read the [MSP Content Model README](https://gitlab.tas.twn.network/twn/marketing/msp-content-model) for the framework overview

**Checkpoint:** What's the difference between a document and an information type? Why does that distinction matter when building a content model?

> [!TIP] Need guidance?
> Join [TWN Commons on Discord](https://discord.gg/kgaMm6WJya) to discuss knowledge management challenges with other IT professionals.

**💬 Share Your Progress:** Post your documentation audit findings in `#knowledge-mgmt` — others will recognise the patterns!

---

### 📋 Milestone 2: Information Inventory (Week 1–2)

**Goal:** Identify and categorise all the information types your MSP creates, uses, and maintains.

**Core Concepts:**
- Information type vs. document: a "Client Overview" is an information type; a specific client's overview is an instance
- MSP-specific information types: CLIENT_OVERVIEW, CLIENT_ONBOARDING, RUNBOOK, SERVICE_CATALOGUE, INCIDENT_REPORT, CHANGE_REQUEST, CONTRACT
- Template anatomy: what every template needs (metadata, required fields, optional fields, lifecycle state)
- Frontmatter as structured metadata: using YAML frontmatter to make documents machine-readable
- Information lifecycle: draft → active → archived → deprecated
- The completeness trap: not every document needs every field — design for the minimum viable structure

**🛠️ Hands-on Practice:**
- [ ] List every type of document your team creates or uses (not instances — types)
- [ ] For each type, define: what triggers its creation, who creates it, who uses it, when it's updated, when it's retired
- [ ] Download and review the MSP Content Model templates (CLIENT_ONBOARDING.md, CLIENT_OVERVIEW.md)
- [ ] Create an information inventory spreadsheet with columns: Type, Trigger, Creator, Consumer, Update Frequency, Lifecycle
- [ ] Write a template for one information type that doesn't yet exist in your organisation

**Checkpoint:** What's the purpose of a lifecycle state field in a document template? Give an example of why it matters in an MSP context.

> [!TIP] Stuck on categorisation?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#knowledge-mgmt` channel has practitioners who've done this inventory exercise — share your list and get feedback.

**💬 Share Your Work:** Post your information inventory for peer review in Discord!

---

### 🔗 Milestone 3: Relationship Mapping (Weeks 2–3)

**Goal:** Understand how information types connect to each other and visualise those relationships using Mermaid diagrams.

**Core Concepts:**
- Information relationships: how a CLIENT_OVERVIEW links to RUNBOOKS, which link to INCIDENTS, which link to CHANGE_REQUESTS
- Entity-relationship thinking: treating information types like database tables with defined relationships
- Mermaid diagrams: using `graph` and `erDiagram` syntax to visualise content models
- Hub documents vs. leaf documents: some information types are entry points (CLIENT_OVERVIEW); others are referenced by many (RUNBOOK)
- Navigability: a content model only works if users can find information by traversing relationships
- The orphan problem: documents with no relationships are documents no one will find

**🛠️ Hands-on Practice:**
- [ ] Draw a relationship diagram (on paper or in Mermaid) showing how your information types connect
- [ ] Identify which types are "hubs" (many connections) and which are "leaves" (few connections)
- [ ] Write a Mermaid `erDiagram` for your MSP's core information types
- [ ] Add relationship fields to three of your templates (e.g., CLIENT_OVERVIEW → related RUNBOOKS)
- [ ] Find and document 3 orphan documents in your current system and decide what to do with them

**Checkpoint:** Draw the relationship between CLIENT_OVERVIEW, RUNBOOK, and INCIDENT_REPORT. What information flows in each direction?

> [!TIP] Mermaid help?
> See the [PIMPyourDocs path](/business/pimpyourdocs) Milestone 3 for a full Mermaid tutorial. Join [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` for hands-on help.

**💬 Share Your Work:** Post your Mermaid relationship diagram in Discord for feedback!

---

### 👥 Milestone 4: Governance & Ownership (Weeks 3–4)

**Goal:** Establish who is responsible for each information type, how it gets reviewed, and what happens when it goes stale.

**Core Concepts:**
- Governance roles: Creator (writes it), Owner (accountable for accuracy), Reviewer (validates on schedule), Consumer (uses it)
- Review cycles: different information types need different review frequencies (runbooks quarterly, client overviews monthly, contracts at renewal)
- The stale document problem: undated, unowned documents are worse than no documents
- Escalation paths: what happens when an owner leaves, or a review is missed
- Governance without bureaucracy: lightweight processes that actually get followed vs. heavy processes that get ignored
- Metrics for governance: how do you know your content model is working?

**🛠️ Hands-on Practice:**
- [ ] Assign a Creator, Owner, and Reviewer role to each information type in your inventory
- [ ] Define a review cycle for each type (weekly / monthly / quarterly / at-event)
- [ ] Set up a simple review calendar or recurring reminders for your most critical information types
- [ ] Write a one-page "Content Governance Policy" covering: roles, review cycles, escalation, and what "stale" means
- [ ] Audit 10 existing documents and assign owners — note how many have no obvious owner

**Checkpoint:** What's the difference between an Owner and a Reviewer? Why do you need both?

> [!TIP] Governance questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) to discuss what governance looks like in practice — theory is easy, implementation is hard.

**💬 Share Your Progress:** Share your Content Governance Policy draft for peer review!

---

### 🚀 Milestone 5: Implementation (Weeks 4–5)

**Goal:** Roll out your content model in phases — from pilot to full adoption — and measure whether it's working.

**Core Concepts:**
- Phased rollout: pilot (one team or one client) → expand (broader adoption) → institutionalise (policy and process)
- Pilot selection: choose a team or client where success is achievable and visible
- Change management: why people resist new documentation practices and how to address it
- Quick wins: find documents that are actively painful right now and migrate them first
- Migration strategy: don't try to migrate everything at once — prioritise by pain and frequency of use
- Success metrics: document freshness %, orphan rate, time-to-find, onboarding time for new staff
- Failure modes: the "we'll do it later" trap, the "perfect template" trap, the "no one updates it" trap

**🛠️ Hands-on Practice:**
- [ ] Select a pilot scope: one client, one service line, or one team
- [ ] Migrate 10 existing documents into your new templates
- [ ] Run a "documentation sprint" with your team: block 2 hours to migrate the highest-priority documents
- [ ] Measure baseline metrics before rollout: how long does it take to find a specific piece of information?
- [ ] After 2 weeks of pilot, measure again and document what improved

**Checkpoint:** Your pilot is running. Two people say the new templates "take too long to fill in." How do you respond?

> [!TIP] Rollout challenges?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#knowledge-mgmt` channel has people who've done this — share what's working and what isn't.

**💬 Share Your Progress:** Post your pilot results and metrics in Discord!

---

### 🛠️ Milestone 6: Tooling Selection (Weeks 5–6)

**Goal:** Choose the right platform for your content model based on your team's workflow, technical capability, and long-term ownership requirements.

**Core Concepts:**
- Git-based documentation: Markdown in GitLab/GitHub as the most sovereign and durable option
- PSA-native documentation: using your existing PSA (ConnectWise, Autotask, HaloPSA) for client-facing docs
- Wiki platforms: Confluence, Notion, BookStack, Wiki.js — tradeoffs for MSP use
- The migration risk: getting locked into a platform that makes export painful
- Tooling criteria: searchability, versioning, access control, export options, cost at scale
- Hybrid approaches: git for internal docs, PSA for client-facing, and how to keep them in sync
- When to migrate: signs your current tool is hurting you more than helping

**🛠️ Hands-on Practice:**
- [ ] Evaluate your current documentation platform against 5 criteria: versioning, export, search, access control, cost
- [ ] Deploy a self-hosted wiki (BookStack or Wiki.js) and migrate 5 documents into it
- [ ] Set up a GitLab repository as a documentation store and commit 3 templates as Markdown files
- [ ] Write a "platform selection" document for your organisation covering: current state, requirements, options evaluated, recommendation

**Checkpoint:** Your MSP is growing and your current wiki is becoming a bottleneck. What criteria would you use to decide whether to migrate vs. fix your current approach?

> [!TIP] Platform questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) to compare notes on documentation platforms — there's experience with all of them.

**💬 Share Your Work:** Share your platform evaluation document for peer feedback!

---

## 📚 Essential Resources

### Documentation
- [MSP Content Model (TWN)](https://gitlab.tas.twn.network/twn/marketing/msp-content-model) - The source framework this path is based on
- [BookStack Documentation](https://www.bookstackapp.com/docs/) - Self-hosted wiki platform
- [Wiki.js Documentation](https://js.wiki) - Modern self-hosted wiki
- [HaloPSA Knowledge Base](https://halopsa.com) - PSA with built-in documentation features

### Tools and Software
- **BookStack** - Self-hosted wiki with book/chapter/page structure that maps well to content models
- **Wiki.js** - Modern, self-hosted wiki with Markdown and Git sync
- **GitLab** - Git-based documentation with merge request review workflows
- **Obsidian** - Local Markdown editor with excellent relationship visualisation (good for building the model before committing to a platform)
- **Mermaid** - Diagram-as-code for relationship maps (see [PIMPyourDocs](/business/pimpyourdocs))

### Practice Labs
- **Home Lab** - Deploy BookStack or Wiki.js on a small VPS or local VM
- **GitLab.com** - Free tier sufficient for documentation repositories during learning

## 🤝 Community and Support

**[Join TWN Commons](https://discord.gg/kgaMm6WJya)** for help with:
- **#knowledge-mgmt** - Content model design, governance, and implementation
- **#documentation** - Platform selection and migration questions
- **#msp-ops** - MSP-specific operational challenges
- **#lab-help** - Assistance with tool deployments

**Share your progress:**
- Post your information inventory and relationship diagrams
- Share governance policies for peer review
- Help others who are earlier in the path

## 🌉 Bridge to TWN Systems

The knowledge management practices in this path are how TWN operates internally:

> [!NOTE] Bridge to TWN
> TWN's MSP operations use the same content model framework taught here. Explore [TWN Systems](https://twn.systems) to find:
> - **MSP portal tools** (twnpanel.com and OpenSelfService) that integrate with structured documentation
> - **Self-hosted wiki providers** who support TWN-aligned hosting
> - **Community-vetted templates** refined through real MSP use

**🛠️ Connected Paths:**
- **[PIMPyourDocs](/business/pimpyourdocs)** - The documentation layer and tooling philosophy that underpins this content model
- **[Startups Playbook](/business/startups-playbook)** - The broader business operations context where this knowledge model lives

## 🚀 What's Next?

After completing this path, you'll be ready for:
- **[PIMPyourDocs](/business/pimpyourdocs)** - Deepen the documentation layer with plain-text-first practices
- **[Startups Playbook](/business/startups-playbook)** - Apply knowledge management to a broader business operating system
- **[Linux Systems](/paths/linux)** - Self-host the wiki platform your content model runs on
- **Advanced MSP Operations** - Deeper dives into PSA configuration, client lifecycle management, and service catalogue design

## 🏆 Certification Alignment

This learning path provides practical grounding for:
- **ITIL Foundation** - Service management and knowledge management align directly with ITIL v4 practices
- **CompTIA Project+** - Project and change management concepts from the governance milestone
- **Microsoft 365 Certified: Fundamentals** - If your MSP is Microsoft-stack heavy, the information typing skills transfer

> [!TIP] Focus on Understanding, Not Certs
> A content model that actually gets used is worth more than any certification. Build the practice first.

---

**Ready to start?** Begin with Milestone 1 and join the [TWN Commons #knowledge-mgmt channel](https://discord.gg/kgaMm6WJya) for support and community.
