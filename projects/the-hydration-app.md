# 💧 The Hydration App

A hydration app that uses personal and ambient data to mathematically calculate intake water levels, with a reminder and tracking system built in.

Source code is kept private; this page mirrors the project's README.

---

# Hydration Tracker

A personalized water-intake tracker built with Expo (React Native + TypeScript). Android is the MVP target; the
Expo/React Native Web stack keeps the same codebase extendable to web and iOS. This implements the MVP scope from
the Hydration Tracker PRD (Draft v2): Google sign-in, an optional onboarding profile, a bio-data goal calculator,
quick-add logging, manual reminders, and a two-track gamified progress scene (Garden / Countryside / Forest).

## Stack & why

- **Expo (managed) + TypeScript** — one codebase for Android now, Web and iOS later, without ejecting.
- **expo-sqlite** — local structured storage (profile, goal history, logs, reminders, streak) so daily totals and
  history can be queried instead of scanning flat key-value blobs, per the PRD's storage guidance.
- **zustand** — small, dependency-light state stores, one per domain (auth/profile/settings/goal/log/reminders/streak).
- **expo-auth-session** (Google provider) — Google Sign-In without a bare native module, so the same code path can
  eventually run in a web build too. Session lives in `expo-secure-store` (native) / `localStorage` (web fallback —
  see `src/services/secureStorage.ts`), never in plain AsyncStorage.
- **expo-notifications** — on-device scheduled reminders, no backend required for MVP.

## Project layout

```
App.tsx                     Root: providers + RootNavigator
src/
  types/models.ts           Core domain types (Profile, Settings, Goal, LogEntry, Reminder, StreakState)
  config/env.ts             Reads EXPO_PUBLIC_* env vars (Google client IDs, Places API key)
  db/                       SQLite schema + one repository module per table
  services/                 Pure logic + platform integrations:
    dayWindow.ts             day-start-aware "day" boundaries
    goalCalculator.ts         bio-data hydration formula
    unitConversion.ts         ml/oz + locale default
    sceneEngine.ts            Daily Scene stage + pacing/withering math
    streakEngine.ts           Persistent Scene streak assessment + gradual withering
    googleAuth.ts             expo-auth-session wrapper
    secureStorage.ts           cross-platform secure token storage
    notifications.ts           reminder scheduling
    placesAutocomplete.ts      Google Places Autocomplete client
  state/                    zustand stores, one per domain, wired to db/ repos
  theme/                    themes.ts (Garden/Countryside/Forest stage defs), colors.ts (UI palette)
  components/               Reusable UI (ProgressRing, SceneView, QuickAddButton, modals, pickers)
  screens/                  LoginScreen, ProfileSetupScreen, HomeScreen, RemindersScreen, SettingsScreen
  navigation/                RootNavigator (auth/onboarding gate) + MainTabs
```

## How the PRD's trickier mechanics are implemented

- **Day boundaries**: every "day" (log totals, Daily Scene reset, streak assessment) is anchored to the user's
  configurable day-start time, not calendar midnight.
- **Daily Scene pacing**: reminder times are checkpoints. Expected intake at "now" =
  `goal × (elapsed checkpoints ÷ total checkpoints)`. If actual intake is behind that, the displayed stage is
  reduced proportionally to the deficit.
- **Persistent Scene withering**: missing a day resets the *live* streak counter immediately, but the scene itself
  withers only one stage per missed day.
- **Goal history**: goals are append-only rows keyed by `createdAt`; recalculating fetches "the goal active as of
  time T" rather than mutating a single row, so past days keep the goal that was actually active then.
- **35-day log retention**: covers the Dashboard's "current week vs. average of the previous 4 weeks" comparison.

## Known gaps / deliberate simplifications

- Illustrations are placeholders (emoji + color + label) pending final art.
- No silent OAuth token refresh — no backend for MVP, so users re-authenticate when the Google token expires.
- Places Autocomplete on web will need a small CORS proxy eventually; fine on Android/iOS.
- No explicit offline/connectivity banner beyond what sign-in itself surfaces.
- The hydration formula is implemented exactly as specified in the PRD but is explicitly flagged there as pending
  medical validation.

## What's been verified

- `npx tsc --noEmit` passes with no errors.
- `npx expo export --platform web` bundles successfully.
- Manually exercised via `expo start --web` + headless Chromium across onboarding, Home, Reminders, and Settings.
  Android has not yet been run on a device/emulator — verify the native build before shipping.
