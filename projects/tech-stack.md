# 🧰 Tech Stack Overview

A consolidated reference of the tech stack behind each app/project in this repo.

---

## 🍷 Uncork (The Winery App)

*Repo: [The_Winery_App](https://github.com/sheldondesousa/The_Winery_App)*

| Tech | Description |
|---|---|
| Kotlin | Native Android language — no cross-platform/hybrid framework used |
| Jetpack Compose | Declarative UI toolkit for the native Android interface |
| KSP (Kotlin Symbol Processing) | Annotation processing for build-time code generation |
| Google LiteRT-LM | On-device runtime that executes the LLM locally for offline inference |
| Gemma 4 E2B (Hugging Face) | ~2.58GB on-device LLM, downloaded + SHA-256 verified on first launch, powers conversational wine recommendations |
| Kaggle wine-review dataset | Static dataset used for optional AI-vs-real-data comparison |
| Brave Search API | Cloud fallback for winery verification when on-device knowledge + Kaggle miss |
| Local on-device storage | Persists favorites, ratings, notes, and conversation history (no cloud sync) |

---

## 🧠 eBrain

*Repo: [eBrain](https://github.com/sheldondesousa/eBrain)*

| Tech | Description |
|---|---|
| Python | Backend language |
| FastAPI | Local backend server framework serving the app at `127.0.0.1` |
| Uvicorn | ASGI server that runs the FastAPI app |
| SQLite | Local catalogue database for documents and conversation history |
| Google Drive (planned) | Will store original source documents |
| LM Studio (planned) | Local runtime for on-device AI chat answers |
| EmbeddingGemma 2 (planned) | Local embeddings model for semantic search |
| React / TypeScript (reserved) | Planned frontend for the desktop research canvas |

---

## 🤳🏾 The Hush Initiative

*Repo: [The-Hush-Initiative](https://github.com/sheldondesousa/The-Hush-Initiative) (private; mirrored at [projects/the-hush-initiative.md](the-hush-initiative.md))*

| Tech | Description |
|---|---|
| React 19 | Frontend UI library powering the app's components and views |
| Vite | Build tool/dev server for fast bundling and hot reload |
| Tailwind CSS | Utility-first CSS framework for the minimalist styling |
| Firebase Auth | Google & Apple sign-in for secure user login |
| Firestore | Firebase's NoSQL DB for storing activity/progress data |
| Firebase Analytics | Tracks usage events (e.g., exercises completed) |
| Firebase Hosting | Deploys the app as a static SPA |

## 🤳🏾 The Hush Initiative — Android

*Repo: [The-Hush-Initiative-Android](https://github.com/sheldondesousa/The-Hush-Initiative-Android)*

| Tech | Description |
|---|---|
| Expo + React Native | Android-first cross-platform mobile framework |
| TypeScript | Type-safe language used across the app |
| react-native-reanimated / react-native-worklets | Native timed breathing & mindfulness animations |
| react-native-svg | Vector graphics for exercise/theme visuals |
| @react-native-async-storage/async-storage | Local persistence for session and mindful-minute metrics |
| expo-font / expo-haptics | Custom typography and haptic feedback |

---

## 💧 The Hydration App

*Repo: [The-Personal-Hydration-App](https://github.com/sheldondesousa/The-Personal-Hydration-App) (private; mirrored at [projects/the-hydration-app.md](the-hydration-app.md))*

| Tech | Description |
|---|---|
| Expo (managed) + React Native | Cross-platform framework; single codebase targeting Android now, Web/iOS later |
| TypeScript | Type-safe language used across the app |
| expo-sqlite | Local structured storage for profile, logs, goals, and streaks |
| zustand | Lightweight state management, one store per domain |
| expo-auth-session | Handles Google Sign-In without a native module |
| expo-secure-store | Secure token storage on native platforms (localStorage fallback on web) |
| expo-notifications | Schedules on-device hydration reminders |

---

## ⚽ World Cup Prediction Model

*Repo: [FIFA-Prediction-Model](https://github.com/sheldondesousa/FIFA-Prediction-Model) (private; mirrored at [projects/world-cup-prediction-model.md](world-cup-prediction-model.md))*

| Tech | Description |
|---|---|
| Elo rating system | Converts team strength differences into win/draw/loss probabilities |
| Poisson distribution modeling | Simulates expected goals for each match |
| Monte Carlo simulation | Runs the bracket 10,000+ times to compute title probabilities |
| Streamlit | Web app for displaying live tournament predictions |
| Kaggle dataset | Historical match results data pipeline (1872–2024) |

---

## 📊 PM Dashboard

*Mirrored at [projects/pm-dashboard.md](pm-dashboard.md)*

| Tech | Description |
|---|---|
| React 18 (JSX) | Frontend framework for the dashboard UI |
| Vite 5 | Build/dev tooling for the React app |
| Node.js + Express 4 | Local backend server proxying integrations (Jira/Confluence/OpenAI) |
| Plain CSS | Styling, no framework |
| Browser localStorage | Client-side persistence for tasks, RICE scores, roadmap |
| dotenv | Loads API keys/secrets server-side from `.env` |

---

## 🚀 Expedited Release Planning

*Mirrored at [projects/expedited-release-planning.md](expedited-release-planning.md)*

| Tech | Description |
|---|---|
| Microsoft Teams Copilot | Captures and transcribes release planning meetings live |
| Windsurf (AI/GenAI) | Structures and normalizes meeting notes into epics/stories/ACs |
| MCP (Model Context Protocol) | Connects AI output to Jira/Confluence to auto-create tickets/pages |

*(This one's a process/workflow experiment, not a coded app — no traditional software stack.)*

---

## 🤖 The AI Digest

*Repo: [The-AI-Digest](https://github.com/sheldondesousa/The-AI-Digest)*

No tech stack documented in the repo yet.

---

## Not included

- `sheldondesousa.github.io` — personal site, not a listed project
- `Laptop-Setup-for-Coding` — dev environment setup scripts, not an app
