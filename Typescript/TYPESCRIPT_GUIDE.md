# TypeScript Guide — Taha Jamaly
### Head-start → parallel with React · same two-pass loop as the CSS→Tailwind drills

> **Total budget: ~8–10 hours of dedicated TS time, spread across Phase 4. Not a phase. Not a course purchase.**
> Your C# background covers ~70% of TS fundamentals already. The remaining 30% is structural typing,
> unions/narrowing, and React-specific patterns. That's what this guide targets.

---

## The sequencing decision

| Option | Verdict |
|---|---|
| TS fully **before** React (1–2 week block) | ❌ Unnecessary delay. You'd learn advanced TS with no context for why. |
| Follow Jonas in JS, defer all TS | ❌ Conflicts with "never write plain JS again" and builds a JS habit you'd immediately unlearn. |
| Switch to a TS-first React course (Mosh, Maximilian) | ⚠️ Legitimate option, but trades away Jonas's React depth (behind-the-scenes, thinking-in-React) to avoid a friction that Stage 0 mostly eliminates. Only switch if TS-native code-along fails after a real attempt. |
| **Stage 0 head-start → TS-native code-along** ✅ (rev. 2) | 3 evenings of pure TS + the 6 React patterns first, then code along with Jonas **directly in TS** from lesson one. The per-lesson delta is a few annotations, not a translation task. |

**Why this works:** ~90% of React+TS friction is 6 memorizable patterns (see Stage 2 table). Learned
cold, they make live TS code-along feel like translation. Learned first in Stage 0, they make it
near-zero overhead. The rebuild loop (rev. 1 plan) is demoted to a per-section fallback.

---

## Stage 0 — Head-start (3 evenings, before/alongside first React sections)

**Cap: 6 hours total. Hard stop.**

| Task | Resource | Cap |
|---|---|---|
| 1. Handbook: "The Basics" + "Everyday Types" — read fully | typescriptlang.org/docs/handbook | 1.5 h |
| 2. Beginner's TypeScript Tutorial — all exercises, don't peek at solutions early | totaltypescript.com/tutorials (free, Matt Pocock) | 3 h |
| 3. Retrofit drill: add types to 3 functions from RecipeBox (the search/results logic is ideal — real data shapes) | your own repo | 1.5 h |

**Setup for task 3:** `npm create vite@latest ts-drills -- --template vanilla-ts` · `strict: true` is on by default — never turn it off, anywhere, ever. Loose-mode TS teaches habits you'll have to unlearn.

**C# → TS mapping (the 70% you already know):**

| C# | TypeScript | Note |
|---|---|---|
| `interface IFoo` | `interface Foo` | Near-identical. TS also has `type Foo =` — for objects they're interchangeable; use `interface` for object shapes, `type` for unions/intersections. Don't burn time on the debate. |
| `List<T>`, generic methods | `T[]` / `Array<T>`, `function f<T>(x: T)` | Same mental model |
| `int?` nullable | `prop?:` / `string \| undefined` | `?` on the property, not the type |
| `enum` | union of string literals: `'draft' \| 'sent'` | Prefer literal unions — more idiomatic, better narrowing |
| Compiler enforcement | `strict: true` in tsconfig | Non-negotiable |

**The 30% that is genuinely new — spend your attention here:**

| Concept | Why C# didn't prepare you |
|---|---|
| **Structural typing** | C# is nominal (a thing is its declared class). TS only cares about shape — any object with the right properties satisfies the interface. This is the single biggest mental-model shift. |
| **Union types + narrowing** | `string \| number` then `typeof x === 'string'` narrows it. C# pattern matching is the closest cousin but the compiler-flow behavior is new. |
| **Discriminated unions** | `{ status: 'ok', data: T } \| { status: 'error', msg: string }` — switch on `status`, compiler narrows the rest. You will use this constantly in React state. |
| **Type inference culture** | Idiomatic TS annotates function boundaries and lets inference handle locals. Don't annotate everything like C# — that's a smell. |

**Done when:** Pocock beginner tutorial 100% · 3 RecipeBox functions typed with zero `any` · you can explain structural vs nominal typing out loud in one sentence.

---

## Stage 1 — The 6 patterns (final Stage 0 evening)

These six shapes are ~90% of all React+TS friction. Memorize them BEFORE lesson one of the course —
this is what turns "converting JS to TS" from a translation task into a few keystrokes per lesson.

| Pattern | Shape |
|---|---|
| Props | `interface Props { items: Item[]; onSelect: (id: number) => void }` then `function List({ items, onSelect }: Props)` |
| useState with empty init | `useState<Item[]>([])` · `useState<Item \| null>(null)` — the two cases inference can't solve |
| Event handlers | `React.ChangeEvent<HTMLInputElement>` · `React.FormEvent<HTMLFormElement>` — copy from cheatsheet; they stick after ~5 uses |
| children | `children: React.ReactNode` |
| useRef (DOM) | `useRef<HTMLInputElement>(null)` |
| Context / useReducer | The only genuinely fiddly one — arrives mid-course, learn it there (cheatsheet has the canonical recipe) |

**Drill:** build one throwaway typed component using patterns 1–5 in a `react-ts` Vite app. 45 min cap.

---

## Stage 2 — TS-native code-along (the whole course)

**Every course project starts as:** `npm create vite@latest <name> -- --template react-ts`
**Pinned tab at all times:** react-typescript-cheatsheet.netlify.app

Code along with Jonas **directly in TS from lesson one**. He writes JS on screen; you write the same
code plus a handful of annotations. For the small apps (Steps, Travel List, Eat-N-Split) the delta
per lesson is minutes, and doing it live means typed-React is your default from day one — no habit
to unlearn later.

**Friction-easing rules (the actual answer to "how do I ease this"):**

1. **10-minute rule:** any type fight over 10 min → `// @ts-expect-error TODO(type)` → keep pace
   with Jonas → log in daily-drill misses → clear all TODOs at section end. React learning is the
   priority; types never block the video.
2. **PropTypes section: skip entirely.** TS replaces it — your approach makes part of the course
   obsolete. Net time saved, not added.
3. **AI line (same as CSS drills):** Claude may *explain* a type error you're stuck on. Claude does
   not *write* your types. Understanding the error is the curriculum.
4. **Don't over-annotate.** Type props, state, handlers, and function boundaries. Let inference do
   locals. If you're writing types Jonas's logic doesn't force, you're gold-plating.
5. **Section-end audit (5 min):** zero `any`, zero surviving `@ts-expect-error`, `strict: true` green.

**Fallback — the rebuild loop (rev. 1):** if live TS genuinely bogs you down for a *full section*
(not one lesson), demote that section: code along in JS, then rebuild it in TS after, 60–90 min cap
(Mapty rule), commit `feat: <project> ts rebuild`. This is the escape hatch, not the plan. If you're
using it for a third consecutive section, that's a Stage 0 gap — go back and re-drill the 6 patterns
rather than grinding.

---

## Stage 3 — Big projects (WorldWise / Fast React Pizza / Wild Oasis tier)

Nothing changes — same TS-native code-along — but this is where Context/useReducer typing (pattern 6)
and API-response typing arrive. Budget slightly more per section; the 10-minute rule still applies.

"Never write plain JS again" from your roadmap is now literal: course, portfolio, NFC, all five
projects — TS-native throughout.

---

## Explicitly skipped (do not study yet)

| Topic | When it becomes relevant |
|---|---|
| Conditional types, mapped types, `infer`, template literal types | Portfolio/NFC build, if ever. Recognize on sight; don't author. |
| Authoring `.d.ts` declaration files | Only if you publish a library. Skip. |
| Decorators, namespaces | Legacy/Angular-adjacent. Skip. |
| Utility types (`Partial`, `Pick`, `Omit`, `Record`) | Passive now — recognize and use when handed to you. Active authoring: NFC platform. |
| Zod + TS inference (`z.infer`) | NFC platform onward — it's all over your architecture docs, but it's a backend-boundary concern, not a React-learning concern. Pocock has a free Zod tutorial for when you get there. |

---

## Video library — beginner → advanced watch-later ladder

> ⚠️ **Your own CSS lesson applies here:** watching produces familiarity, not skill. Videos in this
> ladder are **Tier 1 (event-season passive consumption)** — they support the drills above, they don't
> replace them. Watch order is the ladder order. Everything below Tier "Now" is deliberately deferred.

### Tier: Now (Stage 0 support — first 2 weeks)

| Video / Playlist | Channel | Length | Why |
|---|---|---|---|
| TypeScript Crash Course | Traversy Media | ~90 min | Single clearest standalone intro: types, interfaces, generics, classes, compiler workflow. Watch once at 1.25–1.5× as a primer before the Pocock exercises. |
| TypeScript Crash Course with Matt Pocock (VS Code livestream) | Visual Studio Code (YouTube) / Microsoft Learn | ~60 min | Pocock's editor-first method on video — errors, testing types, unions. Pairs directly with the free tutorial you're doing. |
| TypeScript in 100 Seconds + "TS: the good parts" videos | Fireship | ~5–10 min each | Zero-cost context refreshers. Good between-drill filler, not instruction. |

### Tier: During React (Stage 2–3 support — as patterns come up)

| Video / Playlist | Channel | Length | Why |
|---|---|---|---|
| **No BS TS** (playlist, ~20 episodes) | Jack Herrington | ~10–15 min/ep | The core of this ladder. Progressive difficulty, code-dense, no fluff — episodes 1–10 cover fundamentals fast, later episodes hit React+TS patterns exactly when your rebuild loop needs them. Watch episodes on demand as a pattern appears in a rebuild, not front-to-back. |
| Practical TypeScript – Course for Beginners (John Smilga) | freeCodeCamp | ~6 h | Long-form fallback if a concept from the Handbook isn't sticking. Also covers **Zod + data fetching** — bookmark those chapters for NFC-platform time. Do NOT watch end-to-end now; it's an index, not a syllabus. |
| React + TypeScript videos (search his channel per-topic: props, generics in components, useReducer typing) | Jack Herrington | ~10 min each | Per-pattern lookups during rebuilds. |

### Tier: Later (Stage 3+ / portfolio & NFC build / event-season Tier 1 queue)

| Video / Playlist | Channel | Why |
|---|---|---|
| Matt Pocock's channel — tips shorts + "advanced patterns" videos (generics deep-dives, `infer`, branded types) | Matt Pocock | The advanced end of the ladder. Queue for event season Aug–Nov as passive consumption; author these patterns only when a real project demands them. |
| No BS TS — advanced episodes (utility types, conditional types, fp-ts adjacent) | Jack Herrington | Back half of the playlist. Post-fundamentals only. |
| Advanced state management + performance TS/React videos | Jack Herrington / Theo | Relevant at StockSense/Commerce Engine time, not before. |

**Rule for the whole ladder:** max 1 video per drill session, watched *after* attempting the exercise, not before. Front-loading video hours is the exact failure mode Phase 3 already taught you to avoid.

---

## Links & cheatsheets — bookmark folder

### Reference (daily use)
| Link | What |
|---|---|
| typescriptlang.org/docs/handbook | The Handbook — canonical reference. "Everyday Types" + "Narrowing" are the two pages you'll reopen most. |
| typescriptlang.org/play | **TS Playground** — paste any snippet, see inferred types + emitted JS live. Your scratchpad for every "why is this erroring" moment. Shareable URLs for daily-drill misses. |
| react-typescript-cheatsheet.netlify.app | THE React+TS reference. Props patterns, hooks typing, event types. Open during every Stage 2 rebuild. |
| totaltypescript.com/tsconfig-cheat-sheet | Pocock's tsconfig cheat sheet — which flags matter, sane defaults. Use when setting up any new repo. |

### Interactive practice
| Link | What |
|---|---|
| totaltypescript.com/tutorials | Pocock's free exercise tutorials — Beginner's TS (Stage 0) and **Zod tutorial** (NFC time). |
| github.com/type-challenges/type-challenges | Type-level puzzle repo, easy→extreme. **Warning:** easy tier only, and only as daily-drill variety. Medium+ is type-golf — interview-irrelevant for your targets and a classic time sink. |

### Deferred reading (post-course, pre-interview)
| Link | What |
|---|---|
| *Effective TypeScript* (Dan Vanderkam, book) | The "idiomatic TS judgment" book — 83 items, senior-flavored. Queue for ~Week 40 alongside Alex Xu, not now. |
| *Total TypeScript* (Pocock, No Starch Press, 2026 book) | His workshops in print. Only if a real gap survives the free material — same anti-goal as before: no paid TS spend pre-portfolio. |
| typescriptlang.org/docs/handbook/utility-types.html | Utility types reference page — skim once at Stage 3, internalize during NFC build. |

---

## Anti-goals

- No paid TS course. Free Pocock tutorial + Handbook + rebuilds cover the pre-portfolio bar. (Pocock's paid workshops / new book are good — *later*, if a gap shows up in real project work.)
- No "TS phase" on the timeline. It's absorbed into Phase 4 evenings.
- No annotating every local variable. Boundaries yes, locals no.
- No `any`. Ever. `unknown` + narrowing is the escape hatch.
- If a type fight exceeds 15 min during a rebuild: `// TODO type` comment, move on, log it in daily-drill misses.

---

## Syllabus update for daily-drill

Once Stage 0 is done, append to `data/syllabus.md`:
TS basics · structural typing · unions & narrowing · discriminated unions · generics · typing React props/state/events.
