# 🏥 The Hush Initiative

A breathing app with scientifically-designed exercises, built as a social experiment using AI-assisted product development.

Source code is kept private; this page mirrors the project's README.

---

# The Hush Initiative
*A POC in Vibe Coding*

A minimal, science-backed breathing app designed to help you detach from the noise of modern life. No subscriptions, no gamification, no clutter — just sound, breath, and choice.

## Tech Stack

- React 19
- Vite
- Tailwind CSS
- Firebase (Authentication, Firestore, Analytics)

## Features

- **Six Breathing Exercises**: Box Breathing, 4-7-8 Breathing, Coherent Breathing, Physiological Sigh, Alternate Nostril, and Humming Bee
- **Customizable**: Adjust cycles and breath timing to suit your preferences
- **Guided Information**: Tips, preparation advice, and precautions for each exercise
- **Activity Tracking**: Monitor your progress with metrics like active days and exercises completed
- **Google & Apple Authentication**: Secure sign-in powered by Firebase
- **Minimalist Design**: Clean, distraction-free interface focused on your practice
- **Mobile-First**: Responsive design that works beautifully on all devices

## Architecture

- `src/features/` — feature modules (home, meditation)
- `src/components/`, `src/hooks/`, `src/contexts/` — shared UI, hooks, and app-wide state
- `src/config/firebase.js` — Firebase app initialization (Auth, Firestore)
- `src/services/analytics.js` — Firebase Analytics event tracking
- Deploys to Firebase Hosting as a static SPA (`firebase.json` rewrites all routes to `index.html`)

## Philosophy

Built because nothing like it existed — most breathing/meditation apps were too noisy, too feature-heavy, or too focused on engagement. This is a simple, effective space for stillness: no voiceovers, no upsells, no pressure. Just space to breathe.
