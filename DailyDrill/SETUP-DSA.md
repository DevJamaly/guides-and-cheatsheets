# DSA Drill — Setup & Operating Guide

Same architecture as the quiz drill: a Claude Project generates the sessions,
the **private `daily-drill` repo** is the permanent record. One repo, one
commit habit; the DSA drill lives in its own subtree and its own Claude
Project so the two drills never bleed into each other.

---

## 1. One-time setup (~15 min)

### A. The repo (5 min)

You already have `daily-drill`. Add the subtree:

```bash
cd daily-drill
git pull
mkdir -p dsa/sessions dsa/solutions
```

Drop in the four files from this bundle:

```
daily-drill/
├── ...                     (existing quiz drill, untouched)
└── dsa/
    ├── SETUP-DSA.md        this file
    ├── PROMPT-DSA.md       the Claude Project instructions (canonical copy)
    ├── syllabus-dsa.md     patterns, tags, selection rules — edit as you clear
    ├── misses-dsa.md       weakness log — grows from graded sessions
    ├── sessions/           one file per D-day: problem + solution + verdict
    └── solutions/          your runnable solution files
```

Commit:

```bash
git add dsa/ && git commit -m "chore: bootstrap dsa drill" && git push
```

### B. The Claude Project (5 min)

1. claude.ai → **Projects** → **New project** → name it **DSA Drill**
   (do NOT reuse the Daily Drill project — instructions would collide)
2. Project instructions → paste the full contents of `dsa/PROMPT-DSA.md`
3. Project knowledge → upload `dsa/syllabus-dsa.md`

### C. The tracker (2 min)

Nothing to change — D days already exist. A DSA session = tick the D cell;
the solved counter increments itself. That's the whole integration.

---

## 2. The D-day loop (~30–45 min)

| Step | What | Where |
|---|---|---|
| 1 | `git pull` (skip if single machine) | terminal |
| 2 | DSA Drill project → new chat → type **`dsa`**. If it's been a while or you're being precise, paste current `dsa/misses-dsa.md` with it | Claude |
| 3 | Read the problem. **State your approach + expected complexity in chat** — Claude locks it and waits | Claude |
| 4 | Solve in `dsa/solutions/YYYY-MM-DD.<ext>` (any language), **run the provided tests**, note your time | editor |
| 5 | Paste solution + time → graded → answer the one follow-up | Claude |
| 6 | Save block 1 → `dsa/sessions/YYYY-MM-DD.md`; append block 2 → `dsa/misses-dsa.md`; commit; tick the D cell in the tracker | terminal + tracker |

```bash
git add dsa/
git commit -m "dsa: $(date +%F)"
git push
```

Stuck? Ask for a hint — tier 1 is a probing question, tier 3 is the key
insight. Every hint is logged, and a hinted solve is a miss, not a pass.
That's not punishment; it's what makes the log honest.

**On mobile:** say "mobile session" — you get approach-only mode (no editor):
full plan, complexity, and edge-case list in prose, graded like a design
round.

---

## 3. Calibration week

The first **3 sessions are diagnostic**: easy baselines across different
buckets instead of the normal selection rules. PROMPT-DSA.md handles this
automatically once real misses exist. As a senior you'll likely clear them
fast — good; that's measurement, not wasted time.

---

## 4. Phases & pacing (the honest math)

- Alternating D days ≈ 15 problems/month → **~110 by Soft Apps, ~165 by
  Full Push** — on target *only* with the phase flip below.
- **Acquisition** (now → ~3 months): one pattern at a time, easy→medium,
  in syllabus order.
- **Mixed** (after the last bucket clears): every session a random cleared
  pattern or a due redo. Recognition training.
- **Mock** (final ~6–8 weeks before applications, ≈ Feb 2027): flip the
  alternation — DSA daily, the JS/TS quiz to ~2×/week. Timed two-problem
  rounds, 70 minutes, approach spoken first. Freshest reps land closest to
  interviews.

---

## 5. Maintenance

| When | Do |
|---|---|
| A pattern clears (3 clean mediums) | Retag it `core`, next bucket `active` in `syllabus-dsa.md` → commit → **re-upload to project knowledge** (the one manual sync) |
| Entering mixed / mock phase | Update the phase note in `syllabus-dsa.md`, same sync |
| Monthly | Prune `misses-dsa.md`: delete anything cleared 3+ times |
| Problems feel recognizable / stale | Fix `PROMPT-DSA.md` in the repo first, then re-paste into project instructions. Repo copy stays canonical |

---

## Anti-goals (same as ever)

- ❌ No public repo — grind logs are study infrastructure, not portfolio
- ❌ No LeetCode-premium dependence — the drill writes disguised variants;
  the archive is the question bank
- ❌ No volume worship — one problem done properly beats three skimmed
- ❌ No automation before the manual loop has run two weeks
