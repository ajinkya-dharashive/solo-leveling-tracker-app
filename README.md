# SYSTEM — Hunter's Dashboard

> _"Arise."_

A Solo Leveling–inspired gamified life tracker. One HTML file. No server. No dependencies. Just you and the grind.

---

## What Is This?

A personal productivity tracker built around the RPG mechanics of the Solo Leveling manhwa. You are a Hunter. Your daily habits, workouts, study sessions, and goals are your quests. Every action earns XP. Every missed commitment costs you. Level up. Rank up. Become the Shadow Monarch.

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

- Create quests with a title, description, and difficulty (1.0 Easy → 3.0 Extreme)
- Each difficulty has its own label and colour: Easy / Moderate / Challenging / Hard / Extreme
- **48-hour grace period** — 24h normal window, then 24h grace before penalty fires
- Missed quest penalty: 10–20 XP deducted, 25% chance of a Recovery Quest appearing
- **Recurring quests** — mark a quest as Daily or Weekly; it auto-recreates on completion
- **Edit quests** — update title, description, or difficulty without resetting the timer
- **Quest limit: 3 active at a time** — forces prioritisation, just like the manhwa
- Quest counter shown in the section header (`1 / 3 ACTIVE`)

### 🔁 Habit Tracker

- Create habits with name, category, XP reward, XP penalty, difficulty, frequency, and rest days
- **Grace period** — miss a daily habit and get 24h to recover before the streak resets
- Rest days — mark specific days of the week; no penalty, streak waits
- 7-day milestone: +5 bonus XP and +1 Freeze Token
- **Edit habits** — update any setting without touching streak data
- **Compact view** — collapse all habits to single rows for a cleaner overview; preference saved
- **30-day calendar** — dot grid on each card showing completions, rest days, and misses at a glance
- Daily XP cap from habits: 100 XP

### 🏋️ Quick Log — Workout & Study

Two independent log panels. Optional — no penalty for skipping — but streak-tracked.

**Workout Log**

- Activity, duration, intensity (Low / Med / High), stat boost (STR / END / AGI)
- XP = `max(10, duration × multiplier)` — Low 1×, Med 1.5×, High 2×

**Study Log**

- Subject, duration, focus level (Distracted / Focused / Deep), stat boost (INT / WIL)
- XP = `max(10, duration × multiplier)` — Distracted 1×, Focused 1.5×, Deep 2×

**Log Streak Cards** sit above the panels showing:

- Current streak, best streak, total sessions logged (every log counts, streak ticks once/day)
- Status badge: TODAY / ✓ DONE / ⏳ GRACE / 🧊 FROZEN

### 🧊 Streak Freeze Tokens

- Earned at every 7-day habit milestone (+1 token)
- **Protects Workout and Study log streaks only** — habits use grace period instead
- One freeze per day; frozen logs show 🧊 FROZEN and skip penalty on the next reset

### ⚖️ Weight Tracker

- Log your weight each day (KG or LBS)
- One entry per day — logging again updates rather than duplicating
- Stats: Current, Starting, Change (green if loss, red if gain), Lowest, Highest, Total entries
- Line chart with gradient fill; also available as a tab in Progress Analytics

### 📊 Progress Analytics

Four switchable canvas charts (no libraries):

- **XP History** — line chart of last 20 XP events
- **Stat Radar** — pentagon radar for all five stats
- **Habit Streaks** — current vs best streak bar chart per habit
- **Weight** — full weight history line chart

### 🏆 Badge System (16 badges)

Unlock badges for milestones: First Blood, Iron Will, Beast Mode, Mind Palace, Shadow Monarch, and more. Locked badges show ❓ until earned.

### ✨ Titles System (22 titles)

Titles are earned automatically based on behaviour and displayed in gold under your hunter name. Click your title to cycle through all titles you've unlocked. A cinematic overlay flashes on unlock.

| Title             | How to Earn                   |
| ----------------- | ----------------------------- |
| 🌅 Early Riser    | Log a workout before 8am      |
| 💪 Iron Body      | STR + END ≥ 50                |
| 🦾 Beast          | STR ≥ 25                      |
| 🏃 Endurance King | END ≥ 25                      |
| ⚡ Swift          | AGI ≥ 25                      |
| 🔥 On Fire        | Any streak ≥ 14 days          |
| 💀 Relentless     | Any streak ≥ 30 days          |
| 📚 Scholar        | INT ≥ 20                      |
| 🧠 Mind Forged    | INT ≥ 40                      |
| 🎯 Deep Focus     | 10 Deep Work sessions         |
| 🌑 Shadow Walker  | Complete 10 quests            |
| 👑 Veteran Hunter | Reach Level 20                |
| ⚔️ Quest Lord     | Complete 25 quests            |
| 🌟 Overachiever   | All habits done same day × 5  |
| 🧘 Disciplined    | 7-day habit streak            |
| 🏆 Champion       | Earn 10 badges                |
| 🧊 Ice Veins      | Use freeze token 3 times      |
| 💥 Comeback Kid   | Complete a recovery quest     |
| 📖 Bookworm       | 20 study sessions             |
| ⚙️ Grinder        | 20 workout sessions           |
| 🌙 Night Owl      | Log study after 10pm × 3      |
| 🗡️ Solo           | Complete 5 quests in one week |

### 📅 Weekly Summary

Collapsible panel showing the current week at a glance:

- XP earned, habits done vs expected, quests completed
- Workout and study sessions logged
- Weight change for the week
- Mon–Sun day strip showing per-day habit completion

### 🔔 Daily Briefing (Bell)

Bell icon in the header with a red badge showing pending items. Opens a dropdown with all active quests (time remaining), pending habits, and log streak statuses. Dismiss individual items or clear all. Resets each new day.

### 🌙 End of Day Summary

At 9pm a modal popup fires once per day showing:

- XP earned today
- Habits completed vs total, with pending habits and their penalties listed
- Workout and study logged (yes/no)
- Active quests still open
- A Solo Leveling flavour line based on your performance

### 🎨 Light / Dark Mode

Toggle in the header. Dark mode is the default (deep black, neon accents). Light mode uses a slate-blue palette with high-contrast accessible colours throughout. Preference saved.

---

## XP & Progression

| Concept      | Rule                                             |
| ------------ | ------------------------------------------------ |
| Level        | `floor(totalXP / 1000) + 1`, no cap              |
| XP per level | 1,000 XP flat                                    |
| Quest XP     | `100 + (50 × difficulty)` — 150 to 250 XP        |
| Habit XP     | 10–100 XP (your choice), capped at 100/day total |
| Workout XP   | `max(10, duration × intensity multiplier)`       |
| Study XP     | `max(10, duration × focus multiplier)`           |

### Rank Thresholds

| Rank | Level Required |
| ---- | -------------- |
| F    | 1–4            |
| E    | 5–9            |
| D    | 10–19          |
| C    | 20–29          |
| B    | 30–39          |
| A    | 40–49          |
| S    | 50+            |

---

## Character Stats

| Stat | Full Name    | Raised By     |
| ---- | ------------ | ------------- |
| STR  | Strength     | Workout → STR |
| INT  | Intelligence | Study → INT   |
| END  | Endurance    | Workout → END |
| WIL  | Willpower    | Study → WIL   |
| AGI  | Agility      | Workout → AGI |

Each stat increases by 1 per session. No cap.

---

## Daily Reset Logic

Runs on page load if the date has changed since last visit:

1. **Habits** — missed daily habits activate grace; grace expired = penalty + streak reset
2. **Quests** — expired (48h+) quests apply penalty; 24–48h window shows grace warning
3. **Log streaks** — missed workout/study logs activate grace or reset if grace already expired; frozen logs are protected
4. **Resets** — `completedToday`, `frozenToday`, `habitXPToday`, `freezeUsedToday` all reset

---

## Saving & Backup

Data lives in `localStorage` key `slv2`. It persists automatically across sessions in the same browser.

**To back up:** Activity History section → ⬇ EXPORT JSON → saves `hunter-save-YYYY-MM-DD.json`

**To restore:** ⬆ IMPORT JSON → pick your save file → all data restored

**Migrating from older saves:** The import is fully backwards compatible. Any missing fields (titles, completionLog, recurring quests, etc.) are filled with safe defaults automatically. Your XP, streaks, badges, and history all carry over.

---

## Tech Stack

- Vanilla JavaScript (no frameworks)
- CSS Grid / Flexbox
- HTML5 Canvas API (charts, weight graph)
- localStorage API (persistence)
- Google Fonts CDN (Cinzel, Rajdhani, Exo 2)
- Zero external dependencies

Single file. ~3,100 lines. Runs entirely offline after first load.

---

## Mobile Usage

1. Transfer the HTML file to your phone (Google Drive, AirDrop, email, etc.)
2. Open in Chrome (Android) or Safari (iOS)
3. Tap **Share → Add to Home Screen**
4. Opens fullscreen like a native app
5. localStorage persists between sessions

---

## File Structure

```
index.html   — the entire app (HTML + CSS + JS in one file)
solo-leveling-tracker-prompt.md  — full system prompt to rebuild the app from scratch
```

---

_The System has acknowledged your existence. Now prove you deserve to level up._
