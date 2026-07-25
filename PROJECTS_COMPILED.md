# Sheldon De Sousa — Projects Compilation

Compiled from the README files in the [sheldondesousa/SheldonDeSousa](https://github.com/sheldondesousa/SheldonDeSousa) GitHub profile repository.

## About

Sr. Product Manager (Digital Technology, Consumer Products) at **athenahealth**, based in London. 15+ years building products across healthcare, consumer, and enterprise — from 0→1 to scale. Currently focused on applied AI in product workflows and clinical software.

**Product Strategy & Execution · Applied AI/ML · Growth & Engagement · Research & Discovery · Stakeholder Management**

---

## Table of Contents

1. [The Hush Initiative](#-the-hush-initiative)
2. [The Hydration App](#-the-hydration-app)
3. [World Cup Prediction Model](#-world-cup-prediction-model)
4. [PM Dashboard](#-pm-dashboard)
5. [Expedited Release Planning](#-expedited-release-planning)
6. [The AI Digest](#-the-ai-digest)

---

## 🏥 The Hush Initiative

A breathing app with scientifically-designed exercises, built as a social experiment using AI-assisted product development.

*A POC in Vibe Coding.* A minimal, science-backed breathing app designed to help you detach from the noise of modern life. No subscriptions, no gamification, no clutter — just sound, breath, and choice.

**Tech Stack:** React 19, Vite, Tailwind CSS, Firebase (Authentication, Firestore, Analytics)

**Features:**
- Six Breathing Exercises: Box Breathing, 4-7-8 Breathing, Coherent Breathing, Physiological Sigh, Alternate Nostril, and Humming Bee
- Customizable cycles and breath timing
- Guided information, tips, and precautions per exercise
- Activity tracking (active days, exercises completed)
- Google & Apple Authentication via Firebase
- Minimalist, distraction-free, mobile-first design

**Architecture:**
- `src/features/` — feature modules (home, meditation)
- `src/components/`, `src/hooks/`, `src/contexts/` — shared UI, hooks, and app-wide state
- `src/config/firebase.js` — Firebase app initialization (Auth, Firestore)
- `src/services/analytics.js` — Firebase Analytics event tracking
- Deploys to Firebase Hosting as a static SPA

**Philosophy:** Built because nothing like it existed — most breathing/meditation apps were too noisy, too feature-heavy, or too focused on engagement. This is a simple, effective space for stillness.

*Source code is private.*

---

## 💧 The Hydration App

A hydration app that uses personal and ambient data to mathematically calculate intake water levels, with a reminder and tracking system built in.

A personalized water-intake tracker built with Expo (React Native + TypeScript). Android is the MVP target; the Expo/React Native Web stack keeps the same codebase extendable to web and iOS. Implements the MVP scope from the Hydration Tracker PRD (Draft v2): Google sign-in, an optional onboarding profile, a bio-data goal calculator, quick-add logging, manual reminders, and a two-track gamified progress scene (Garden / Countryside / Forest).

**Stack & why:**
- **Expo (managed) + TypeScript** — one codebase for Android now, Web and iOS later
- **expo-sqlite** — local structured storage (profile, goal history, logs, reminders, streak)
- **zustand** — small state stores, one per domain
- **expo-auth-session** (Google provider) — Google Sign-In without a bare native module; session in `expo-secure-store`/`localStorage`
- **expo-notifications** — on-device scheduled reminders, no backend required for MVP

**Key mechanics:**
- Day boundaries anchored to a configurable day-start time, not calendar midnight
- Daily Scene pacing based on expected intake vs. actual at reminder checkpoints
- Persistent Scene withering: streak resets immediately on a missed day, but the scene withers one stage per missed day
- Append-only goal history, keyed by `createdAt`
- 35-day log retention for week-over-week comparisons

**Known gaps:** placeholder illustrations, no silent OAuth refresh (no backend for MVP), web needs a CORS proxy for Places Autocomplete eventually, no offline banner, hydration formula pending medical validation.

**Verified:** `tsc --noEmit` passes, `expo export --platform web` bundles successfully, manually exercised via `expo start --web` + headless Chromium. Android native build not yet verified on device/emulator.

*Source code is private.*

---

## ⚽ World Cup Prediction Model

An AI-assisted experiment testing mathematical models (Elo ratings + Poisson distributions) to predict match outcomes using a data pipeline via Kaggle.

Repo: [FIFA-Prediction-Model](https://github.com/sheldondesousa/FIFA-Prediction-Model)

Predicts the most likely World Cup winner from historical data, and shows the quantitative evidence behind the prediction — Elo gap, simulated win rate, historical base rate at that stage — not just a name.

**Approach:**
1. Convert the Elo rating gap between two teams into win/draw/loss probabilities
2. Convert those into expected goals via a Poisson distribution, calibrated on historical goals-per-match
3. Simulate matches and the bracket they feed into
4. Simulate extra time/penalties for knockout rounds using historical shootout rates
5. Roll the simulation forward 10,000+ times and count title frequency per team

Deliberately not a deep learning model — with only 22 past World Cups to learn from, a black-box model would overfit and undermine the "show your evidence" goal.

**Status:** v1 working — Elo rating engine, Poisson goal-simulation model, knockout bracket Monte Carlo simulator, historical backtest, a custom "Match Outlook" web app, and a Streamlit app.

**Data sources:** Kaggle international football results (1872–2024), eloratings.net historical Elo ratings, FIFA's official World Rankings archive.

**Roadmap:**
- **v1:** Elo + Poisson simulation, static historical bracket backtest, Streamlit display
- **v2:** Knockout-stage-experience adjustment, full backtesting/evaluation suite, published calibration numbers
- **v3:** Extend to simulate from a full pre-tournament field, not just mid-tournament

---

## 📊 PM Dashboard

A central source of truth and operation, built to remove dependence on multiple apps and constant context-switching.

**Case study:** Built a proof-of-concept Product Management Dashboard in ~3 hours (solo build using Codex) to reduce PM context switching by consolidating prioritization, execution, planning, and key system views into a single, desktop-like workspace.

**Problem:** Routinely context-switching across Jira, Confluence, Amplitude, notepads, calendars, and communication tools creates cognitive load, increases missed follow-ups, and slows execution.

**Tech Stack:** React 18 + Vite 5, Node.js + Express 4 (local backend), plain CSS, browser localStorage, dotenv for config/secrets.

**Security:** Secrets live server-side in `.env`, never in the React bundle; local server proxies outbound calls to Jira/Confluence/OpenAI; data at rest in localStorage is unencrypted; no multi-user login/roles.

**Features (POC scope):**
- **Task hub** — create/edit/delete, Eisenhower tagging, status, filters, sorting, keyboard shortcuts, local persistence
- **Prioritization & planning** — Eisenhower Matrix, Kanban (drag-and-drop), RICE scoring, Roadmap Builder (Now/Next/Later)
- **Integrations** — Jira (sprints, issues, comments), Confluence documentation
- **Analytics** — embedded Amplitude dashboard
- **Built-in AI Assistant** chat with local history and model selector
- Light/Dark theme, resource indicator, "install as app" guidance

**Learnings:** The single-pane experience resonated, but permissions-heavy systems (Teams/Outlook) are both a major value lever and a primary adoption risk since they couldn't be integrated.

**Next:** Validate Teams/Outlook integration feasibility and security review path, define pilot success metrics, expand integrations incrementally.

---

## 🚀 Expedited Release Planning

An experiment adapting the AmbientNotes idea to how releases are planned, condensing a 3-day process into 3 hours.

**Proposal:** AI-Assisted Release Planning Using Copilot, Windsurf, and MCP — captures planning discussions in real time and uses AI to generate, organize, and operationalize release artifacts, while keeping humans in control of decisions and validation.

**Problem:** Manual note-taking and story writing, delays between planning and Jira/Confluence setup, inconsistent story structure, manual sprint allocation/pointing, rework after planning.

**Workflow:**
1. **Release Planning Meeting** — Teams Copilot records/transcribes a structured agenda (goals, epics, stories, ACs, points, bandwidth)
2. **Draft Artifact Generation** — Copilot produces a structured meeting summary as draft input
3. **AI Structuring & Normalization (Windsurf)** — organizes stories under epics, standardizes format, expands ACs, flags gaps
4. **Sprint Planning & Bandwidth Constraints** — AI applies sprint parameters and team bandwidth; humans validate estimates
5. **Work-Type Tagging** — stories tagged Product/Engineering/UX with enforced ratios, imbalances flagged for review
6. **Jira & Confluence Creation via MCP** — PRD pages, sprints, stories, and epics created automatically (sprint and epic auto-creation, and labels, didn't work in practice; done manually)

**Humans still own:** scope/priorities, epic definitions, story point validation, sprint commitments, risk/dependency decisions.

**Success metrics:**
- Time to complete release planning: **3 Days → 3 Hours**
- Story creation accuracy: **85/100**
- Time from planning meeting to "Jira-ready": **80% gains**
- No manual work beyond epic creation + sprint setup; no stories required manual rewrite

**Pilot recommendation:** Start with one team (Android), one release, one planning cycle — measure, refine, then scale.

---

## 🤖 The AI Digest

Curated AI-related posts from frontier models and other credible sources.

Repo: [The-AI-Digest](https://github.com/sheldondesousa/The-AI-Digest)

---

## Connect

🌐 [sheldondesousa.com](https://www.sheldondesousa.com) · 💼 [LinkedIn](https://www.linkedin.com/in/sheldondesousa)
