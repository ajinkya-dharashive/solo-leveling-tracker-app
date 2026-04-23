# SYSTEM — Hunter OS

> _"Arise."_

A Solo Leveling–inspired gamified life tracker. One HTML file. No server. No dependencies. Just you and the grind.

---

## What Is This?

A personal productivity tracker built around the RPG mechanics of the Solo Leveling manhwa. You are a Hunter. Your daily habits, workouts, and goals are your quests. Every action earns XP. Every missed commitment costs you. Level up. Rank up. Become the Shadow Monarch.

---

## Getting Started

1. Download `index.html`
2. Open it in any modern browser (Chrome, Safari, Firefox, Edge)
3. **On mobile:** Open in Chrome/Safari → tap Share → _Add to Home Screen_ → opens fullscreen like a native app
4. Click your hunter name to set it
5. Add your first quest or habit and begin

No installation. No account. No internet required after first load (Google Fonts loads once).

All data is stored locally in your browser via `localStorage`. Nothing leaves your device.

---

## Features

### ⚔️ Quest System

- Create quests with a title, description, and difficulty: Easy / Moderate / Challenging / Hard / Extreme
- XP rewards: 50 / 100 / 150 / 200 / 250 XP by difficulty
- **48-hour system** — 24h normal window, then 24h grace before penalty fires
- Missed quest penalty: 10–20 XP deducted, 25% chance of a Recovery Quest appearing
- **Recurring quests** — mark as Daily or Weekly; auto-recreates on completion
- **Edit quests** — update title, description, or difficulty without resetting the timer
- **Quest limit: 3 active at a time** — forces prioritisation

### 🔁 Habit Tracker

- Create habits with name, category, XP reward, XP penalty, frequency, and rest days
- **Strict midnight reset** — missed daily habits lose their streak at midnight; no grace for habits
- **Rest days** — mark specific days of the week; streak is preserved, no penalty
- **7-day milestone:** +1 Freeze Token earned per 7-day streak
- **Edit habits** — update any setting without touching streak data
- Daily XP cap from habits: 100 XP
- **Stat boost on completion** — category determines which stat increases (see Stats section)

### 🏋️ Workout Log

Log-based tracker with streak mechanics. No penalty for skipping — but streak-tracked.

- Activity, duration, intensity (Low / Med / High), primary stat boost (STR / END / AGI)
- XP = `max(10, duration × multiplier)` — Low 1×, Med 1.5×, High 2×
- Streak card shows current streak, best streak, and total sessions
- Logs automatically create a calendar entry for that day

### 🧊 Streak Freeze Tokens

- Earned at every 7-day habit milestone (+1 token)
- Earned at every 7-day workout streak milestone (+1 token)
- On next morning open after missing habits: a single prompt lists all at-risk habits
- Spend **1 token** to protect **all** incomplete habits at once
- Already-completed habits are unaffected
- One freeze action per day maximum
- No tokens? Penalties apply automatically

### ⚖️ Weight Tracker

- Log your weight each day (KG or LBS)
- One entry per day — logging again updates rather than duplicating
- Stats: Current, Starting, Change (green if loss, red if gain), Lowest, Highest, Total entries
- Line chart with gradient fill

### 📊 Progress Analytics

Three switchable canvas charts (no libraries):

- **XP History** — line chart of last 20 XP events
- **Stat Radar** — pentagon radar for all five stats
- **Habit Streaks** — current vs best streak bar chart per habit

### 📅 Smart Calendar

Two-tab layout with full calendar views and a sidebar.

**Views:** Month · Week · Day · Agenda

**Auto-populated items (read-only):**
- **Habit chips** — appear at the top of every calendar day; green if done, purple if pending, blue if rest day
- **Quest deadline markers** — appear on the day a quest expires; colour-coded by urgency

**Events (+ EVENT button):**
- Title, category, date, time, XP reward, stat boost, recurrence, reminder
- **Deadline toggle** — mark any event as a deadline; optionally set work block duration and how many days before to show them

**Sidebar:** Mini navigator, today's XP and event summary, upcoming events

### 🏆 Badge System (12 badges)

Unlock badges for reaching milestones. Locked badges show a cryptic hint rather than the unlock condition — figure it out yourself.

| Badge | Hint |
|---|---|
| ⚔️ First Blood | Draw first blood in the hunt |
| 🔁 Creature of Habit | Build something that outlasts willpower |
| 🛡️ Iron Will | Seven days of unbroken quest resolve |
| 💀 Relentless | Thirty days of unbroken quest resolve |
| 🔥 Beast Mode | Push until the ordinary breaks |
| 💪 Unstoppable Force | Become an immovable legend |
| ⚖️ Balanced Hunter | No stat left behind |
| 👑 Habit Master | Rule your routines for a moon cycle |
| 🎖️ Centurion | Reach a milestone few achieve |
| 🌑 Shadow Monarch | Ascend to the highest throne |
| 📅 Consistent | Seven days of perfect repetition |
| 🔮 From the Ashes | Rise after falling |

### ✨ Titles System (16 titles)

Titles are earned automatically and displayed in gold under your hunter name. Click your title to cycle through all titles you've unlocked. A cinematic overlay flashes on unlock.

| Title | How to Earn |
|---|---|
| 🌅 Early Riser | Log a workout before 8am |
| 💪 Iron Body | STR + END ≥ 50 |
| 🦾 Beast | STR ≥ 25 |
| 🏃 Endurance King | END ≥ 25 |
| ⚡ Swift | AGI ≥ 25 |
| 🔥 On Fire | Any streak ≥ 14 days |
| 💀 Relentless | Any streak ≥ 30 days |
| 🌑 Shadow Walker | Complete 10 quests |
| 👑 Veteran Hunter | Reach Level 20 |
| ⚔️ Quest Lord | Complete 25 quests |
| 🌟 Overachiever | All habits done same day × 5 |
| 🧘 Disciplined | 7-day habit streak |
| 🏆 Champion | Earn 10 badges |
| 🧊 Ice Veins | Use freeze token × 3 |
| 💥 Comeback Kid | Complete a recovery quest |
| 🗡️ Solo | Complete 5 quests in one week |

### 🔔 Daily Briefing (Bell)

Bell icon in the header with a red badge showing pending items. Opens a dropdown with all active quests (time remaining), pending habits, and workout streak status. Dismiss individual items or clear all. Resets each new day.

### 🌙 End of Day Summary

At 9pm a modal fires once per day showing:

- XP earned today
- Habits completed vs total, with pending habits and their midnight penalties listed
- A Solo Leveling flavour line based on your performance

---

## XP & Progression

| Concept | Rule |
|---|---|
| Level | `floor(totalXP / 1000) + 1`, no cap |
| XP per level | 1,000 XP flat |
| Quest XP | 50 / 100 / 150 / 200 / 250 by difficulty |
| Habit XP | 10–100 XP (your choice), capped at 100/day total |
| Workout XP | `max(10, duration × intensity multiplier)` |

### Rank Thresholds

| Rank | Level Required |
|---|---|
| F | 1–4 |
| E | 5–9 |
| D | 10–19 |
| C | 20–29 |
| B | 30–39 |
| A | 40–49 |
| S | 50+ |

---

## Character Stats

| Stat | Full Name | Raised By |
|---|---|---|
| STR | Strength | Workout (STR selected) |
| INT | Intelligence | Learning habits |
| END | Endurance | Workout (END selected) · Health habits |
| WIL | Willpower | Workout (WIL selected) · Productivity / Finance / Relationships / Creativity / Other habits |
| AGI | Agility | Workout (AGI selected) |

Each stat increases by 1 per workout log or habit completion. No cap.

---

## Daily Reset Logic

Runs on page load if the date has changed since last visit:

1. **Habits** — uncompleted daily habits are flagged; if you have freeze tokens a prompt appears to protect all at once with 1 token; otherwise penalties apply and streaks reset
2. **Quests** — expired (48h+) quests apply penalty; 24–48h window shows grace warning
3. **Workout streak** — missed workout log resets streak to 0
4. **Midnight timer** — a precise midnight timer also fires to reset habit streaks without waiting for next page load
5. **Resets** — `completedToday`, `frozenToday`, `habitXPToday`, `freezeUsedToday` all reset

---

## Saving & Backup

Data lives in `localStorage` key `hos4` (auto-migrates from older `hos3` / `hos2` saves).

**To back up:** Activity History section → ⬇ EXPORT → saves a `.json` file

**To restore:** ⬆ IMPORT → pick your save file → all data restored

Calendar events, habits, quests, stats, XP, history, weight logs, badges, and titles all export and import together in one file.

---

## Tech Stack

- Vanilla JavaScript (no frameworks)
- CSS Grid / Flexbox
- HTML5 Canvas API (charts, weight graph)
- localStorage API (persistence)
- Google Fonts CDN (Cinzel, Rajdhani, Exo 2)
- Zero external dependencies

Single file. ~1,800 lines. Runs entirely offline after first load.

---

## Mobile Usage

1. Transfer the HTML file to your phone (Google Drive, AirDrop, email, etc.)
2. Open in Chrome (Android) or Safari (iOS)
3. Tap **Share → Add to Home Screen**
4. Opens fullscreen like a native app
5. localStorage persists between sessions

---

_The System has acknowledged your existence. Now prove you deserve to level up._
