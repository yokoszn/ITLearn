---
title: PIMPyourDocs
tags:
  - documentation
  - markdown
  - plain-text
  - learning-path
draft: false
---

# PIMPyourDocs Learning Path

Documentation you don't own is documentation that can disappear. This path teaches the philosophy and practice of plain-text, git-versioned, AI-ready documentation — from Markdown fundamentals to professional templates, Mermaid diagrams, and clean migration paths away from Confluence, Notion, and Google Docs.

## 📋 Overview

**Duration:** 4–6 weeks (self-paced)
**Level:** Beginner to Intermediate
**Prerequisites:** Basic text editing, familiarity with any file system

**Why this matters:** Most teams write documentation into someone else's platform: Confluence (Atlassian owns your content), Notion (proprietary export), Google Docs (requires Google account to access). When the platform changes pricing, gets acquired, or sunsets, your documentation becomes a migration crisis. Plain-text Markdown with git version control is the antidote — it's readable by humans, processable by machines, versionable with git, and exportable to anything.

## ✅ Prerequisites

Before starting this path, you should:
- [ ] Be comfortable opening and editing text files
- [ ] Understand what a file system is (folders, files, paths)
- [ ] Have git installed (or be willing to install it)
- [ ] **Recommended:** Complete the [Linux Systems](/paths/linux) path first for git familiarity

## 🎯 Learning Milestones

### 📝 Milestone 1: The Plain Text Manifesto (Week 1)

**Goal:** Understand why plain-text documentation is the sovereign choice and how it positions your team for AI readiness and platform independence.

**Core Concepts:**
- Plain text as infrastructure: why Markdown is to documentation what TCP/IP is to networking — a universal base layer
- AI readiness: why LLMs work better with structured Markdown than with WYSIWYG exports
- Platform independence: your documentation should be readable without the platform that created it
- Git as documentation infrastructure: version history, blame, branches, and merge requests for docs
- The "single source of truth" principle: one location, one format, one version
- RFC 2119 keywords: why `MUST`, `SHOULD`, `MAY` reduce ambiguity in technical documentation
- Common objections addressed: "Markdown is hard for non-technical users", "We need rich formatting", "Our team won't adopt it"

**🛠️ Hands-on Practice:**
- [ ] Export one document from your current tool (Confluence, Notion, or Google Docs) and compare the export quality
- [ ] Write the same document in plain Markdown — measure the difference in readability and portability
- [ ] Install a Markdown editor (VSCode, Obsidian, or Typora) and get comfortable with the basics
- [ ] Read the [PIMPyourDocs PRINCIPLES.md](https://gitlab.tas.twn.network/twn/documentation/PIMPyourDocs) for the full philosophy
- [ ] Write a one-page "documentation manifesto" for your team explaining why you're moving to plain text

**Checkpoint:** Name three situations where Markdown-in-git gives you an advantage over a WYSIWYG wiki. Be specific.

> [!TIP] Need guidance?
> Join [TWN Commons on Discord](https://discord.gg/kgaMm6WJya) to discuss documentation philosophy and get feedback on your approach.

**💬 Share Your Progress:** Post your documentation manifesto draft in `#documentation` for feedback!

---

### 🏗️ Milestone 2: Document Structure & Spec (Weeks 1–2)

**Goal:** Learn the PIMPyourDocs specification for consistent file naming, directory layout, YAML frontmatter, and document structure.

**Core Concepts:**
- File naming conventions: `kebab-case`, date prefixes for time-sensitive docs, type prefixes for templates
- Directory layout: how to organise a documentation repository (by type, by team, by domain — tradeoffs)
- YAML frontmatter: `title`, `status`, `owner`, `reviewed_at`, `tags` — what each field does and why it matters
- Document status lifecycle: `draft` → `active` → `deprecated` → `archived`
- RFC 2119 keyword usage: `MUST`, `MUST NOT`, `SHOULD`, `SHOULD NOT`, `MAY` in procedures and specs
- Heading hierarchy: when to use H1 vs H2 vs H3, and why violating heading order breaks accessibility
- The "minimum viable document" principle: what every document MUST have before it's published

**🛠️ Hands-on Practice:**
- [ ] Create a documentation repository structure following the PIMPyourDocs spec
- [ ] Write three documents with correct frontmatter (title, status, owner, reviewed_at)
- [ ] Convert an existing document into the correct structure (fix headings, add frontmatter, set lifecycle state)
- [ ] Write a one-paragraph procedure using RFC 2119 keywords correctly
- [ ] Review the [PIMPyourDocs SPEC.md](https://gitlab.tas.twn.network/twn/documentation/PIMPyourDocs) and note any differences from your current practice

**Checkpoint:** What does `reviewed_at` in frontmatter actually enable? What breaks if you leave it out?

> [!TIP] Spec questions?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` channel has people who've implemented this spec — ask for their experience.

**💬 Share Your Work:** Post your repository structure for peer feedback!

---

### 📊 Milestone 3: Diagrams as Code (Weeks 2–3)

**Goal:** Master Mermaid diagram syntax for the four most common diagram types: flowchart, sequence, ER, and state — and understand why diagrams-as-code are superior to screenshot-based diagrams.

**Core Concepts:**
- Diagrams as code: why a Mermaid diagram in a Markdown file is better than a PNG (versionable, searchable, editable without special tools)
- Mermaid flowchart: `graph TD`, nodes, edges, decision diamonds, subgraphs
- Mermaid sequence diagram: actors, messages, activation boxes, loops, alt/opt blocks
- Mermaid ER diagram: entities, attributes, relationships (one-to-many, many-to-many)
- Mermaid state diagram: states, transitions, initial and final states — excellent for lifecycle documentation
- When NOT to use Mermaid: complex architectural diagrams where draw.io or Excalidraw is clearer
- The `diagrams/` directory convention: where diagrams live in a PIMPyourDocs repository

**🛠️ Hands-on Practice:**
- [ ] Write a Mermaid flowchart for a process you know well (onboarding, incident response, deployment)
- [ ] Write a Mermaid sequence diagram for an API interaction or multi-party workflow
- [ ] Write a Mermaid ER diagram for 3–5 information types from the [MSP Content Model](/business/msp-content-model) path
- [ ] Write a Mermaid state diagram for a document's lifecycle (draft → active → deprecated → archived)
- [ ] Add all four diagrams to a single Markdown file and render them in your editor

**Checkpoint:** What are two situations where a Mermaid flowchart is the wrong choice? What would you use instead?

> [!TIP] Mermaid help?
> The [Mermaid Live Editor](https://mermaid.live) is excellent for learning. Share your diagrams in [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` for feedback.

**💬 Share Your Work:** Post your four Mermaid diagrams in Discord for review!

---

### 📑 Milestone 4: Templates in Practice (Weeks 3–4)

**Goal:** Learn the five core PIMPyourDocs templates and practise using each one on real or realistic content.

**Core Concepts:**
- ADR (Architecture Decision Record): capturing the context, decision, and consequences of technical choices — so future-you understands why
- RUNBOOK: step-by-step operational procedures with prerequisites, steps, verification, and rollback
- SERVICE: documenting a service's purpose, owners, dependencies, SLOs, and runbook references
- API: endpoint documentation with request/response examples, error codes, and authentication requirements
- INCIDENT: post-incident records with timeline, impact, root cause, and action items
- Template conventions: what every template shares (frontmatter, status, owner, reviewed_at)
- The "fill in later" trap: why a template with empty required fields is worse than no template

**🛠️ Hands-on Practice:**
- [ ] Write an ADR for a technology decision you've made or observed (e.g., "We chose Markdown over Confluence")
- [ ] Write a RUNBOOK for a procedure you perform regularly (e.g., deploying a service, onboarding a new user)
- [ ] Write a SERVICE document for a service you operate or use (even a simple one like "our email server")
- [ ] Write an INCIDENT document for a real or fictitious incident with full timeline and root cause
- [ ] Review all four documents against the PIMPyourDocs template spec and correct any missing required fields

**Checkpoint:** What's the most important field in an ADR? Why does context matter more than the decision itself?

> [!TIP] Template questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` to share your templates and get feedback from practitioners who use them daily.

**💬 Share Your Work:** Post your ADR and RUNBOOK in Discord for peer review!

---

### 🚪 Milestone 5: Escaping Your Current Platform (Weeks 4–5)

**Goal:** Plan and execute a migration from Confluence, Notion, or Google Docs to plain-text Markdown without losing content or context.

**Core Concepts:**
- Migration strategy: why "migrate everything at once" always fails and what to do instead
- Confluence migration: using the `confluence-to-markdown` exporter, cleaning up macro artifacts, restructuring hierarchy
- Notion migration: Notion's Markdown export quality, what you lose (database properties, linked pages), and how to handle it
- Google Docs migration: Docs-to-Markdown plugin, table handling, image extraction
- Content triage: not everything in your current wiki is worth migrating — how to decide what to keep
- The 80/20 rule for migrations: 20% of your documents are referenced 80% of the time — migrate those first
- Post-migration verification: how to confirm nothing important was lost

**🛠️ Hands-on Practice:**
- [ ] Export 20 pages from your current documentation platform (or a sample set if you're learning)
- [ ] Run an automated migration tool and assess the output quality
- [ ] Manually clean up 5 migrated documents to meet PIMPyourDocs spec (add frontmatter, fix headings)
- [ ] Identify 5 documents that aren't worth migrating (outdated, duplicated, or superseded) and archive them
- [ ] Write a "migration plan" document for your organisation covering: scope, priority order, timeline, verification

**Checkpoint:** You're migrating 500 Confluence pages. You have 40 hours of migration time available. How do you decide what to migrate first?

> [!TIP] Migration challenges?
> The [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` channel has people who've migrated from every major platform — share your specific challenges.

**💬 Share Your Progress:** Post your migration plan for peer feedback!

---

### ⚙️ Milestone 6: Spec-Driven Development (Weeks 5–6)

**Goal:** Understand how to use documentation as a development input — specs that drive implementation, planning structures that keep work visible, and testable documentation that can be verified.

**Core Concepts:**
- Spec-driven development: writing the spec before the code — what it enables and how PIMPyourDocs supports it
- The `.planning/` directory: where specs, decisions, and work-in-progress planning documents live
- GSD (Getting Stuff Done) framework: how to structure work items, acceptance criteria, and done definitions in Markdown
- OpenSpec: open specification format for APIs and services that teams can write before implementation begins
- Testable documentation: writing procedures that can be verified — steps with expected outputs, not just instructions
- Documentation as CI artifact: how to include documentation linting and link checking in your build pipeline
- The "living document" principle: documentation that ages out is worse than no documentation

**🛠️ Hands-on Practice:**
- [ ] Create a `.planning/` directory in a project and write a spec for a feature you're working on
- [ ] Write a SERVICE document before implementing the service (spec-first)
- [ ] Add a documentation linter (markdownlint) to a CI pipeline or pre-commit hook
- [ ] Write a RUNBOOK where every step has a verification command — test that every step actually works
- [ ] Set up a link checker to catch broken references in your documentation repository

**Checkpoint:** What's the difference between a procedure and a spec? Write one sentence that captures the distinction.

> [!TIP] Spec-driven questions?
> Join [TWN Commons](https://discord.gg/kgaMm6WJya) `#documentation` and `#engineering` to discuss how teams integrate documentation into their development workflow.

**💬 Share Your Work:** Post your spec-first SERVICE document in Discord for feedback!

---

## 📚 Essential Resources

### Documentation
- [PIMPyourDocs Repository](https://gitlab.tas.twn.network/twn/documentation/PIMPyourDocs) - The source framework this path is based on
- [Mermaid Documentation](https://mermaid.js.org/intro/) - Official Mermaid syntax reference
- [Mermaid Live Editor](https://mermaid.live) - Browser-based Mermaid playground
- [markdownlint](https://github.com/DavidAnson/markdownlint) - Markdown linting rules and CLI
- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) - Key words for use in RFCs (MUST, SHOULD, MAY)

### Tools and Software
- **VSCode + Markdown extensions** - Free, excellent Markdown editor with Mermaid preview
- **Obsidian** - Local-first Markdown editor with graph view and excellent plugin ecosystem
- **Typora** - Clean WYSIWYG Markdown editor (paid, worth it for non-technical users)
- **GitLab / Gitea** - Self-hosted git platforms with built-in Mermaid rendering in Markdown
- **markdownlint** - CLI and editor plugin for consistent Markdown formatting
- **Pandoc** - Universal document converter (Markdown → PDF, DOCX, HTML)
- **confluence-to-markdown** - Automated Confluence export converter

### Practice Labs
- **Home Lab** - A GitLab or Gitea instance is ideal; GitHub.com free tier works for learning
- **Local setup** - VSCode + Markdown Preview Enhanced plugin renders Mermaid locally

## 🤝 Community and Support

**[Join TWN Commons](https://discord.gg/kgaMm6WJya)** for help with:
- **#documentation** - Markdown, Mermaid, templates, and migration questions
- **#engineering** - Spec-driven development and CI integration
- **#lab-help** - Assistance with git and tooling setup
- **#study-groups** - Find study partners working through the same path

**Share your progress:**
- Post your Mermaid diagrams and templates for review
- Share migration challenges and solutions
- Help others who are earlier in the path

## 🌉 Bridge to TWN Systems

PIMPyourDocs is how TWN itself documents its systems and services:

> [!NOTE] Bridge to TWN
> TWN uses PIMPyourDocs internally. This means:
> - The templates you learn here are the same ones used in TWN repos
> - Your documentation contributions to TWN projects will fit naturally
> - Self-hosted GitLab (via [TWN Systems providers](https://twn.systems)) is the recommended platform for git-versioned docs

**🛠️ Connected Paths:**
- **[MSP Content Model](/business/msp-content-model)** - The framework that organises the documents you learn to write here
- **[Startups Playbook](/business/startups-playbook)** - Milestone 4 uses these documentation practices to document your business stack
- **[Linux Systems](/paths/linux)** - Git fundamentals underpin everything in this path

## 🚀 What's Next?

After completing this path, you'll be ready for:
- **[MSP Content Model](/business/msp-content-model)** - Apply documentation discipline to a full knowledge management framework
- **[Startups Playbook](/business/startups-playbook)** - Document your startup stack as you build it
- **[Site Reliability Engineering](/paths/sre)** - Apply spec-driven development and runbook practices to reliability engineering
- **Advanced Documentation Engineering** - Documentation CI pipelines, automated link checking, spec testing

## 🏆 Certification Alignment

This learning path provides practical grounding for:
- **Technical Writing certifications** (CPTC from STC) - Template discipline and structure align with professional technical writing standards
- **ITIL Foundation** - Runbook and knowledge management practices align with ITIL knowledge management
- **Any software development role** - ADRs, specs, and git-based documentation are expected in professional engineering teams

> [!TIP] Focus on Understanding, Not Certs
> Plain-text documentation skills are permanently useful. Every platform comes and goes; Markdown and git will be here.

---

**Ready to start?** Begin with Milestone 1 and join the [TWN Commons #documentation channel](https://discord.gg/kgaMm6WJya) for support and community.
