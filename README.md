# Cressida OS — Cycle & Relationship Intelligence

**Cressida** is a mobile-first OS for emotional and relationship intelligence.

The v1 MVP focuses on:
- Tracking menstrual cycles (period start, length, simple phases)
- Tracking relationship events (dates, conflicts, intimacy, appreciation, deep talks)
- Generating a simple **Daily Card**:
  - Today’s cycle phase (estimated)
  - Today’s mood (if logged)
  - Short summary text
  - “Do” / “Avoid” guidance for the day

This project is built as an **Expo + TypeScript + Supabase + Zustand** app and is designed to be extended into a full Relationship & Emotional OS over time.

---

## Core Concept

- **User:** Woman in a relationship (boyfriend/girlfriend/partner), solo user in v1.
- **Goal:** Reduce unnecessary fights and misunderstandings by syncing:
  - Cycle data (period, phase, symptoms, mood)
  - Relationship data (events, conflicts, intimacy)
- **Output:** Simple, actionable guidance instead of charts-only.

---

## Tech Stack (MVP)

- **Frontend:** Expo (React Native) + TypeScript
- **State:** Zustand
- **Backend:** Supabase (Auth + Postgres)
- **Navigation:** Expo Router or React Navigation (to be chosen in PHASE 1)
- **Styling:** Basic React Native styles (minimal dependencies)

---

## Planned Data Model (High Level)

- `profiles`
  - `id` (uuid, FK to `auth.users`)
  - `name`
  - `relationship_status`
  - `typical_cycle_length`
  - timestamps

- `cycles`
  - `id`
  - `user_id`
  - `start_date`
  - `end_date` (nullable)
  - timestamps

- `moods`
  - `id`
  - `user_id`
  - `date`
  - `score` (1–10)
  - `note` (optional)
  - timestamps

- `relationship_events`
  - `id`
  - `user_id`
  - `date`
  - `type` (`date`, `conflict`, `intimacy`, `appreciation`, `deep_talk`, ...)
  - `intensity` (1–10)
  - `description`
  - timestamps

A simple **insight engine** will infer:
- Cycle phase (menstruation / follicular / ovulation / luteal)
- Risk level (low/medium/high)
- A short summary and “Do / Avoid” suggestions.

No external AI calls are required in v1. The logic is a pure TypeScript function.

---

## Project Structure (Target)

```text
app/
  (screens and navigation)

components/
  (shared UI components)

lib/
  supabase.ts
  insight/
    generateDailyCard.ts

store/
  useAuthStore.ts
  useUserStore.ts

types/
  (shared TS types/interfaces)

assets/
  (images, icons, fonts)
