# 🚀 Expedited Release Planning

An experiment adapting AmbientNotes to how releases are planned, condensing a 3-day process into 3 hours.

---

# Proposal: AI-Assisted Release Planning Using Copilot, Windsurf, and MCP

## Overview

Release planning is a critical but time-consuming activity that currently requires significant manual effort to translate discussions into PRDs, epics, user stories, acceptance criteria, sprint plans, and Jira tickets.

This proposal outlines an AI-assisted release planning workflow that captures planning discussions in real time and uses AI to generate, organize, and operationalize release artifacts, while keeping humans firmly in control of decisions and validation.

The goal is not to replace product or engineering judgment, but to eliminate mechanical work and reduce planning friction.

## Problem Statement

Today's release planning challenges include:

- Manual note-taking and story writing after meetings
- Time delays between planning discussions and Jira/Confluence setup
- Inconsistent story structure and acceptance criteria — create testable ACs aligned with frameworks like Spec-Kit
- Manual sprint allocation and story pointing
- Rework required post–release planning to fix gaps or misalignment

## Proposed Solution (High-Level)

A structured, AI-assisted release planning flow that integrates:

- **Microsoft Teams Copilot** for live meeting capture
- **AI structuring** to convert notes into clean product artifacts
- **Windsurf + MCP** to automatically create and organize Jira and Confluence content

This builds directly on patterns already proven in prior AI-assisted delivery experiments.

## End-to-End Workflow

### Step 1: Release Planning Meeting (Human-Led, AI-Captured)

- Team meets together (in-person, or on a Teams call)
- Copilot records and transcribes the session
- Meeting follows a structured agenda: release goals and constraints, epic definition, story and acceptance criteria discussion, story point estimates, team bandwidth/sprint assumptions, and allocations by product:engineering ratio
- The objective is clear intent, not perfect documentation

### Step 2: Draft Artifact Generation (AI-Assisted)

- Copilot produces a structured meeting summary (downloadable in Word or PDF), including release goals, epics, story candidates with AC-like statements, initial story points, and open questions/risks
- This output is treated as a draft input, not a final outcome

### Step 3: AI Structuring & Normalization (Windsurf)

The Copilot output is fed into Windsurf, where GenAI + a structured prompt:

- Organizes stories under their respective epics
- Cleans and standardizes story format
- Expands incomplete acceptance criteria
- Identifies gaps or ambiguities
- Applies consistent language and patterns
- Allocates based on set parameters

### Step 4: Sprint Planning & Bandwidth Constraints (AI + Rules)

Explicit inputs provided to the AI:

- **Sprint parameters:** number of sprints, sprint start/end dates, target velocity per sprint
- **Team bandwidth:** available capacity, known PTO/holidays/constraints, max story points per sprint
- **Story pointing:** points from planning are preserved; AI flags oversized stories and suggests splits; humans validate final estimates

### Step 5: Work-Type Tagging and Ratios

Each story is tagged as **Product**, **Engineering**, or **UX/Design**. The AI enforces predefined ratios for the release (e.g., 75% Product / 20% Engineering / 5% UX). If ratios are exceeded, AI flags the imbalance for review rather than forcing changes.

### Step 6: Jira & Confluence Creation via MCP

Using MCP integration:

- Confluence PRD pages are created
- Sprints created in Jira *(sprint creation didn't work)*
- User stories + ACs are created
- Epics created automatically *(epic creation didn't work — done manually)*
- Jira stories are created automatically, assigned to the correct epic, tagged by work type *(labels didn't work)*, placed into the appropriate sprint, and linked to capacity assumptions

Human review occurs before final commit if desired.

## What Humans Still Own (By Design)

This process is human-led at all decision points:

- Release scope and priorities
- Epic definitions
- Story point validation
- Final sprint commitments
- Risk and dependency decisions

AI accelerates execution; humans provide judgment.

## Success Metrics

**Primary metrics**

- Reduced time to complete release planning — **3 Days → 3 Hours**
- Reduced manual post–release planning work — no manual work other than epic creation + sprint setup
- Accuracy of story creation — Good, **85/100**
- Accuracy of story organization by epic and sprint — N/A
- Accuracy of adherence to defined parameters (points, ratios, bandwidth) — Very Good; split stories above threshold

**Additional metrics**

- Reduction in Jira rework after planning — manual copy/paste from Description to AC
- Number of stories requiring manual rewrite — None
- Sprint carryover rate
- Team satisfaction with planning process — Happy, informed
- Consistency of story structure across releases — Very Good
- Time from planning meeting to "Jira-ready" state — **80% gains**

## Expected Benefits

- Faster release planning cycles
- Higher consistency and quality of stories
- Reduced cognitive load on PMs and engineers
- Better alignment across Product, Engineering, and UX
- A repeatable, scalable planning system

## Pilot Recommendation

Start with one team (Android), one release, one planning cycle. Measure outcomes, refine prompts and rules, then scale.

## Summary

This proposal shifts release planning from a manual documentation exercise to a structured, AI-assisted orchestration process. The result is not just speed — but better quality, better alignment, and more time spent on strategic thinking instead of mechanical work.
