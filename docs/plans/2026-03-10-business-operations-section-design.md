# Business & Operations Section — Design Document

**Date:** 2026-03-10
**Status:** Implemented
**Author:** Claude Code

---

## Overview

Adds a new `content/business/` section to ITLearn, covering the operational and business side of running an IT organisation. Complements existing technical paths (networking, Linux, VyOS, VPN) with three structured learning paths derived from TWN internal repositories.

## Motivation

IT learners who understand both the technical and operational sides of an organisation are significantly more valuable. The three source repos teach skills that most technical courses ignore: choosing a startup tech stack, managing client knowledge at scale, and owning documentation as code.

## Target Audience

Same as existing ITLearn paths — IT learners and students who want to build complete professional capability, not just technical skills.

## Source Repositories

| Repo | Description |
|------|-------------|
| `twn/marketing/startups-playbook` | Opinionated guide to startup tech stacks (infra, security, compliance, CRM, BOS) — AU-focused |
| `twn/marketing/msp-content-model` | Knowledge management framework for MSPs (templates, governance, lifecycle) |
| `twn/documentation/PIMPyourDocs` | Plain-text-first documentation philosophy (Markdown, Mermaid, git-versioned) |

## Files Created

### New

- `content/business/index.md` — Hub page linking to all three paths
- `content/business/startups-playbook.md` — Startup tech stack learning path (6 milestones)
- `content/business/msp-content-model.md` — MSP knowledge management path (6 milestones)
- `content/business/pimpyourdocs.md` — Plain-text documentation path (6 milestones)

### Modified

- `content/index.md` — Added "Business & Operations" section to Featured Learning Paths

## Architecture Decisions

### Separate `content/business/` directory (not `content/paths/`)

The existing `content/paths/` directory contains purely technical learning paths. Business and operations content is a distinct domain. Separating them:
- Makes the taxonomy clear to learners
- Allows independent growth of each section
- Keeps technical paths uncluttered

### Same depth as technical paths

Each business path follows the `content/paths/template.md` structure exactly — same milestone format, same TWN integration callouts, same community Discord references. Consistency matters more than brevity.

### Draft: false on all new files

All files are published immediately. The content is complete and reviewed.

## Path Structures

### 1. Startups Playbook (6 milestones)
1. Business Operating System (BOS)
2. Infrastructure Foundations
3. Security & Identity from Day One
4. Business Operations Stack
5. Legal & Compliance (AU-focused)
6. Scaling Your Stack

**TWN Bridge:** Self-hosted infra providers; connects to NetBird VPN and VyOS paths.

### 2. MSP Content Model (6 milestones)
1. Why Content Models Matter
2. Information Inventory
3. Relationship Mapping
4. Governance & Ownership
5. Implementation
6. Tooling Selection

**TWN Bridge:** PIMPyourDocs for documentation layer; MSP portal.

### 3. PIMPyourDocs (6 milestones)
1. The Plain Text Manifesto
2. Document Structure & Spec
3. Diagrams as Code
4. Templates in Practice
5. Escaping Your Current Platform
6. Spec-Driven Development

**TWN Bridge:** Self-hosted GitLab; PIMPyourDocs used within TWN itself.

## Verification Checklist

- [ ] `npm run quartz build` — no errors
- [ ] `/business/` index renders with links to all three paths
- [ ] All three path pages render correctly
- [ ] `draft: false` on all new files
- [ ] TWN Commons Discord links present in each path
- [ ] TWN Systems links present in each path
- [ ] Cross-path wikilinks resolve
