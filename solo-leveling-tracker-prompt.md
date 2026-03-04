# Solo Leveling Life Tracker — System Prompt

Build a single-file HTML gamified life tracker inspired by the Solo Leveling manhwa. No frameworks, no external libraries except Google Fonts. All state stored in `localStorage` key `slv2`. Dark fantasy RPG aesthetic with light mode toggle.

---

## FONTS & THEME

- Google Fonts: Cinzel (headings/ranks), Rajdhani (UI labels/numbers), Exo 2 (body)
- Dark default: `#0a0a0f` background, electric blue `#00d4ff`, purple `#7b2fff`, gold `#ffd700`, green `#00ff9d`, red `#ff3366`
- Light mode toggle (`body.light`): slate-blue palette with high-contrast accessible colors
- Override ALL neon colors explicitly in light mode — diff badges, habit tags, stat values, stat bars, toasts, log streak badges must all have deep readable colors

### Light mode color overrides (explicit)
```css
body.light .diff-easy     { color: #006633; }
body.light .diff-moderate { color: #0068cc; }
body.light .diff-chall    { color: #996600; }
body.light .diff-hard     { color: #b45000; }
body.light .diff-extreme  { color: #bb0033; }
body.light .stat-STR .stat-val { color: #cc3300; }
body.light .stat-INT .stat-val { color: #0068cc; }
body.light .stat-END .stat-val { color: #006633; }
body.light .stat-WIL .stat-val { color: #5500cc; }
body.light .stat-AGI .stat-val { color: #996600; }
/* match bar colors to val colors, box-shadow: none in light mode */
```

---

## HEADER (sticky)

- Left: Rank badge (color matches rank) + Hunter name (click to edit via modal)
- Center: Level label, XP progress bar, XP count `(xpInLevel/1000)`
- Right: 🧊 Freeze token counter + USE button | 🔔 Bell notification button | ☀/🌙 Light/Dark toggle
- **No quest streak display anywhere in the header**

---

## CHARACTER STATS

Five stat cards in a grid: STR, INT, END, WIL, AGI

Each card layout (top to bottom):
1. Abbreviation (Cinzel, dim, letter-spaced)
2. Current value (large Rajdhani number, colored per stat)
3. Progress bar (colored per stat)
4. **Full name in small dim text** — Strength / Intelligence / Endurance / Willpower / Agility

Dark mode stat colors: STR `#ff6644` | INT `#44aaff` | END `#44ff88` | WIL `#cc44ff` | AGI `#ffcc44`
Light mode stat colors override all of the above (see Light mode section).

Stats increase by 1 each time a Workout or Study session is logged (per the stat chosen at log time).

---

## XP & LEVELS

- Level = `floor(totalXP / 1000) + 1`, no cap
- Rank tiers: F(1–4) → E(5–9) → D(10–19) → C(20–29) → B(30–39) → A(40–49) → S(50+)
- **No XP bonus from any streak** — flat XP only
- Level-up overlay: 3s particle burst animation
- Rank-up overlay: 4s shockwave animation

---

## QUEST SYSTEM

- Manual creation: Title, Description, Difficulty slider 1.0–3.0 (step 0.5)
- XP reward = `100 + (50 × difficulty)`
- **Difficulty — each value gets its own distinct label and color:**

| Value | Label | Dark color | Light color |
|-------|-------|------------|-------------|
| 1.0 | EASY | `#44ff88` green | `#006633` |
| 1.5 | MODERATE | `#00d4ff` teal | `#0068cc` |
| 2.0 | CHALLENGING | `#ffd700` gold | `#996600` |
| 2.5 | HARD | `#ff8c00` orange | `#b45000` |
| 3.0 | EXTREME | `#ff3366` red | `#bb0033` |

- **Grace period**: 48-hour window total. After 24h a grace banner appears on the card. Penalty only fires at 48h.
- Missed quest penalty: 10–20 XP random. 25% chance of Recovery Quest (1.3× difficulty, 1.2× XP, 24h window).
- **Edit Quest**: EDIT button on each active quest card. Editable: Title, Description, Difficulty (XP recalculates). Timer, status, generatedAt, isRecovery — all untouched.
- Quest card actions: COMPLETE | EDIT | ABANDON

---

## HABIT TRACKER

- Create habit: Name, Category (Health/Productivity/Learning/Finance/Relationships/Creativity/Other), XP Reward (10–100), XP Penalty (5–50), Difficulty (1.0–5.0), Frequency (Daily/Weekly), Rest Days (day-of-week picker, green = rest day)
- Daily XP cap from habits: 100 XP total
- Per-habit streak with best streak memory
- 7-day streak milestone: +5 XP bonus + 🧊 +1 Freeze Token awarded
- **Grace period only — no freeze for habits:**
  - Miss a daily habit → grace activates for 24h (amber ⏳ GRACE tag on card)
  - Complete during grace → streak saved, grace cleared
  - Grace expires → penalty fires + streak resets
  - Rest days → no penalty, no grace, streak waits
- **Edit Habit** — ✏ icon top-left of card (✕ delete top-right):
  - Editable: Name, Category, XP Reward, XP Penalty, Difficulty, Frequency, Rest Days
  - **All streak data strictly preserved**: currentStreak, bestStreak, totalCompletions, lastCompleted, graceActive — never touched by edit
  - Modal shows warning: "⚠ STREAK DATA IS PRESERVED — only settings are updated"

### Habit card layout
Name + category icon | current streak (🔥 N) | DAY STREAK label | XP/penalty/difficulty tags + grace/frozen tags if active | MARK COMPLETE button (or status mark) | best streak + rest day labels

---

## QUICK LOG (Workout & Study)

Two panels side-by-side. One-off log entries — not compulsory, streak-tracked separately.

### Workout Log
- Fields: Activity (text), Duration (minutes), Intensity (Low/Med/High radio), Stat to increase (STR/END/AGI radio)
- XP = `max(10, floor(duration × mult))` — Low=1×, Med=1.5×, High=2×
- High intensity → increments `highIntensityCount`

### Study Log
- Fields: Subject (text), Duration (minutes), Focus Level (Distracted/Focused/Deep radio), Stat to increase (INT/WIL radio)
- XP = `max(10, floor(duration × mult))` — Distracted=1×, Focused=1.5×, Deep=2×
- Deep focus → increments `deepWorkCount`

### Log Streak Cards (above the two log panels)
Two cards (⚔️ Workout / 📖 Study) each showing:
- Current streak (days), Best streak, Total logs count
- **`totalLogs` increments on every single log submission** (not just first per day)
- Streak only ticks up once per day regardless of how many times logged
- Status badge: `TODAY` purple (not yet logged) | `✓ DONE` green | `⏳ GRACE` amber | `🧊 FROZEN` blue

### Log Streak Rules
- Miss a day → grace activates (one extra day to log before streak resets to 0)
- Grace expired → streak resets
- Freeze token protects log streaks (see Streak Freeze)

---

## STREAK FREEZE TOKENS

- Earned: +1 token per 7-day habit streak milestone
- Displayed in header
- **Applies ONLY to Workout and Study log streaks — NOT to habits** (habits use grace period only)
- On USE: marks both log streaks `frozenToday = true` if not already logged today
- Frozen cards show `🧊 FROZEN` badge
- Next day reset: frozen log streaks skip penalty and grace — streak holds intact
- One freeze per day max (`freezeUsedToday` flag resets each new day)
- Toast describes exactly what was protected

---

## DAILY RESET (runs on page load when date has changed)

1. **Habits** — for each daily habit not completed:
   - Yesterday was a rest day → no action
   - `graceActive` was true → grace expired, apply XP penalty, reset streak, clear grace
   - Otherwise → activate grace, show toast warning
   - Reset `completedToday = false`, `frozenToday = false`
2. **Quests** — for each active quest:
   - Age > 172800000ms (48h) → missed, penalty, 25% recovery offer
   - Age > 86400000ms (24h) and `graceShown` false → show grace toast, set `graceShown = true`
3. **Log streaks** (workout + study) — for each:
   - Not logged today + `frozenToday` true → streak holds, clear flag
   - Not logged today + `graceActive` → grace expired, reset streak to 0
   - Not logged today + missed yesterday → activate grace, show toast
   - Reset `loggedToday = false`, `frozenToday = false`
4. Reset `freezeUsedToday = false`, `habitXPToday = 0`

---

## WEIGHT TRACKER

Section placed between Quick Log and Progress Analytics.

- Layout: left panel (log input) + right side (chart + stats row)
- Input: number field (step 0.1) + KG/LBS toggle button
- LOG button: saves entry for today. If today already has an entry, **updates it** (no duplicates per day)
- No streaks, no penalties, no daily pressure — completely optional

### Stats row (below chart)
Current | Starting (first ever entry) | Change (current − start, **green if negative/loss, red if positive/gain**) | Lowest | Highest | Total Entries

### Weight chart (pure canvas)
- Line chart with gradient fill under line
- X-axis: M/D date labels, spaced to avoid crowding
- Y-axis: weight values with 15% padding above and below data range
- Minimum 2 entries to render; otherwise shows placeholder text
- Unit toggle converts all historical values for display (original unit stored per entry)
- Respects dark/light mode colors (line, dots, grid, text all switch)

---

## BELL NOTIFICATION PANEL

- 🔔 Bell icon in header, red badge with count of pending (non-dismissed) items
- Bell animates with CSS ring shake when items are pending
- Click → opens DAILY BRIEFING dropdown panel (closes on outside click)
- Shows all trackable items: active quests, daily habits, workout log, study log
- Sorted: urgent/grace first → pending → completed/done
- Each item: icon | title | subtitle | ✕ dismiss button
- Dismissed items hidden for the rest of the day
- Dismissals stored in `sl_dismissed` (localStorage), reset daily via `sl_dismissed_date`
- CLEAR ALL button dismisses everything at once
- Bell updates automatically when quests/habits/logs are completed

### Item types
| Icon | Type | Subtitle |
|------|------|----------|
| ⚔️ | Active quest | `Xh Ym remaining` |
| ⏳ | Grace quest | `Grace period — Xh left before penalty` |
| ⚠️ | Urgent quest <3h | red styling |
| 🔁 | Pending habit | `+XP · 🔥 N day streak · Penalty: -XP` |
| ✅ | Done habit | `+XP earned · 🔥 N day streak` |
| 😴 | Rest day habit | `Rest day — streak protected` |
| 🧊 | Frozen log streak | `Frozen — streak safe` |
| ⏳ | Grace log streak | `Grace period — log today to save streak` |
| ⚔️/📖 | Workout/Study log | streak status |

---

## PROGRESS ANALYTICS

Three switchable canvas charts (pure canvas, no chart libraries):
- **XP History** — line chart with gradient fill, last 20 history entries
- **Stat Radar** — pentagon radar for STR/INT/END/WIL/AGI
- **Habit Streaks** — grouped bar chart: current streak vs best streak per habit

Charts redraw on data change, tab switch, and window resize.

---

## BADGE SYSTEM (16 badges)

| ID | Name | Condition |
|----|------|-----------|
| first_quest | First Blood | Complete 1 quest |
| first_habit | Creature of Habit | Create 1 habit |
| scholar | Scholar Awakened | Log 1 study session |
| iron_will | Iron Will | Quest streak ≥ 7 |
| relentless | Relentless | Quest streak ≥ 30 |
| grind | Grind Never Stops | 50 total completions |
| deep_thinker | Deep Thinker | 10 Deep Work sessions |
| beast_mode | Beast Mode | 10 High Intensity workouts |
| mind_palace | Mind Palace | INT ≥ 50 |
| unstoppable | Unstoppable Force | STR ≥ 50 |
| balanced | Balanced Hunter | All stats ≥ 20 |
| comeback | From the Ashes | Complete a recovery quest |
| habit_master | Habit Master | Any habit streak ≥ 30 days |
| centurion | Centurion | Reach Level 10 |
| shadow_monarch | Shadow Monarch | Reach S Rank (Level 50+) |
| consistent | Consistent | Any habit streak ≥ 7 days |

Unlocked badges: icon + name + earned date. Locked: ❓ + ???

---

## ACTIVITY HISTORY

- Last 50 entries, newest first
- Each entry: green/red left border, label, XP delta, relative timestamp
- Data toolbar at bottom: ⬇ EXPORT JSON (`hunter-save-YYYY-MM-DD.json`) | ⬆ IMPORT JSON (full state restore)

---

## MODALS

Six modals sharing one overlay with blur backdrop. Close on overlay click or ✕ button.

1. **New Quest** — Title, Description, Difficulty slider, XP preview
2. **Edit Quest** — same fields pre-populated; timer/status/generatedAt untouched
3. **New Habit** — Name, Category, XP Reward slider, XP Penalty slider, Difficulty slider, Frequency, Rest Days picker
4. **Edit Habit** — same fields pre-populated; all streak data untouched; warning shown in modal
5. **Hunter Name** — single text field

---

## STATE OBJECT

```js
G = {
  hunter: {
    name, totalXP, level, rank,
    questStreak, lastQuestDate, lastActiveDate,
    freezeTokens, freezeUsedToday
  },
  stats: { STR, INT, END, WIL, AGI },
  quests: [{
    id, title, description, difficulty, xpReward,
    status,        // 'active' | 'completed' | 'missed'
    generatedAt,   // Date.now()
    completedAt, isRecovery, graceShown
  }],
  habits: [{
    id, name, category, frequency,
    xpReward, xpPenalty, difficulty,
    restDays,      // int[] of DOW [0=Sun..6=Sat]
    currentStreak, bestStreak, totalCompletions, failureCount,
    lastCompleted, completedToday, graceActive, frozenToday
  }],
  habitXPToday,
  badges: [{ id, earned, earnedDate }],
  history: [{ delta, label, xp, ts }],
  deepWorkCount, highIntensityCount,
  logStreaks: {
    workout: { currentStreak, bestStreak, lastLogged, loggedToday, graceActive, totalLogs, frozenToday },
    study:   { currentStreak, bestStreak, lastLogged, loggedToday, graceActive, totalLogs, frozenToday }
  },
  weightLog: [{ date, value, unit, ts }],  // date = todayStr() e.g. 'Mon Jan 01 2025'
  weightUnit: 'kg'                          // 'kg' | 'lbs'
}
```

---

## ANIMATIONS & UX

- Staggered section entrance on load: 0.06s delay per section, opacity 0→1 + translateY(16px)→0
- Flavor text after workout/study log: random quote, fade in, auto-fade after 3s
- Toasts — bottom-right, 3.1s auto-dismiss: `badge` gold | `pos` green | `neg` red | `info` blue
- Bell animates with CSS keyframe ring shake when pending items exist
- Quest timers refresh every 30s via `setInterval`
- Single `window.addEventListener('resize', ...)` redraws all active canvases
- Level-up overlay: 32 particles burst with random angles, 3s duration
- Rank-up overlay: expanding shockwave ring, 4s duration

---

## RESPONSIVE

`@media (max-width: 700px)`:
- Stats grid → 3 columns
- Quick log grid → single column
- Weight section → single column
- Header → single column stack
- Overlay text → 36px
