# 📊 PM Dashboard

A central source of truth and operation, built to remove dependence on multiple apps and constant context-switching.

---

# Case Study: Building a Product Management Dashboard (POC)

**Date/timeframe:** May 1, 2026 (3 hours)
**Role/team:** Sr. Product Manager (solo build using Codex)
**Intent/channel:** Proof of concept to share on Confluence
**Audience:** Cross-functional stakeholders (PMs, Devs, UX, etc.)

## Summary

Built a proof-of-concept Product Management Dashboard in ~3 hours using Codex to reduce PM context switching by consolidating prioritization, execution, planning, and key system views into a single, desktop-like workspace.

## Situation / Problem

As a PM, routinely context-switching across Jira, Confluence, Amplitude, notepads, calendars, and communication tools creates cognitive load, increases the chance of missed follow-ups, and slows prioritization and day-to-day execution.

## Goal

Deliver a "single-pane-of-glass" workspace where the most common PM workflows are reachable in one click, without requiring a new account system or complex setup, so stakeholders can see what an integrated PM cockpit could look like.

## Approach / Solution

Designed the experience as a desktop-like web app that keeps execution (tasks), prioritization (Eisenhower Matrix + RICE), and planning (Roadmap Builder + Kanban) tightly coupled, with optional integrations surfaced alongside the core workflow.

## Tech Stack

- **Frontend:** React 18 (`react`, `react-dom`) with JavaScript/JSX
- **Build/dev tooling:** Vite 5 (`vite`, `@vitejs/plugin-react`)
- **Backend (local):** Node.js + Express 4 (`server/index.js`)
- **Styling:** plain CSS (`src/styles.css`)
- **Storage:** browser localStorage (client-side persistence)
- **Config/secrets:** dotenv via `.env`

## Security Measures

- **Secrets:** API keys/tokens live in `.env` and are read by the Node/Express server; they are not embedded in the React bundle.
- **Browser vs server:** The web UI talks to the local server; the server makes outbound calls (Jira/Confluence/OpenAI) so credentials stay server-side.
- **Transport/auth:** Requests are over local host; external services use their own auth (API token/Bearer/Basic as configured).
- **Data at rest:** Tasks/roadmap/RICE are stored in browser localStorage (not encrypted); anyone with access to the browser profile can read it.
- **Access control:** There's no multi-user login/roles; security is essentially "who can access your machine + your `.env` file."

## How It Works

- **UI → Local state:** React components collect input (tasks, roadmap, filters) and keep it in component state.
- **UI → Browser storage:** When you save/update, the app persists data to localStorage so it survives refreshes.
- **UI → Local server:** For integrations (Jira/Confluence/OpenAI/Amplitude), the UI calls local Node/Express endpoints on `XXX.X.X.X`.
- **Local server → External services:** The server reads credentials from `.env`, calls Jira/Confluence/OpenAI over HTTPS, then returns JSON back to the UI.
- **External links/iframes:** Clicking "Open in …" or viewing an embedded dashboard loads that remote URL directly (separate from the server API flow).

## Features Included (POC scope)

### Task hub

- Create/edit/delete tasks in a modal editor
- Task fields: subject, description, tag (Eisenhower quadrant), status (To Do / In Process / Done)
- Mark done/undo; All/Active/Done filters with counts
- Sort by date or by tag (quadrant)
- Keyboard shortcut: `Ctrl`/`⌘`+`K` to create; `Esc` closes overlays/modals
- Local persistence in Chrome `localStorage` (no account required)

### Prioritization & planning

- **Eisenhower Matrix** overlay with quadrant drill-in
- **Kanban** overlay with drag-and-drop between To Do / In Process / Done
- **RICE Prioritization** widget with scoring, ranking, editing, and reset (saved locally)
- **Roadmap Builder** overlay with Now/Next/Later (or 6-month horizon), draggable features, epics, and color tagging (saved locally)

### Information & integrations (optional; via local APIs)

- **Jira**: sprint/release navigation, issue lists, issue detail modal, view/post comments
- **Confluence Documentation**: pages created by a configured creator, grouped by date, with refresh

### Analytics

- **Amplitude** overlay with embedded dashboard iframe and editable links

### Built-in assistant

- **AI Assistant** chat overlay with history saved locally and a model selector

### Operational UX

- Light/Dark theme toggle
- Resource indicator (storage/heap/localStorage/app size)
- Chrome "install as app" guidance for desktop-like usage

## Execution Highlights (3-hour build)

- Prioritized a cohesive workflow (tasks → prioritization → planning) over breadth of integrations.
- Kept the POC lightweight by using local persistence and optional server-backed integrations.

## Results (qualitative; not yet measured)

- **Expected outcomes:** time saved, reduced cognitive load, fewer workflow errors, and better prioritization by consolidating work into one workspace.
- **Early feedback:** Nicer to have all applications in one place with more integrations between apps. However, apps like Teams and Outlook have not been integrated due to permissions.
- They account for a lot of communication and content storage. Hence, not having them is a gap.

## Learnings / Gaps

- The single-pane experience resonated, but **permissions-heavy systems (Teams/Outlook)** represent a major value lever and a primary risk for adoption if they can't be integrated.

## What's Next

- Validate integration feasibility (Teams/Outlook permissions, security review path, and acceptable scopes).
- Define success metrics for a pilot (e.g., reduction in tool switching, time-to-status-check, missed follow-ups).
- Expand integrations incrementally while preserving the "one-click" workflow.
