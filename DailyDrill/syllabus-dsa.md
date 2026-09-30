# DSA Syllabus — what's in scope and how to pick the problem

> This file only says WHAT to drill. Current weaknesses live in
> dsa/misses-dsa.md. What was already asked lives in dsa/sessions/.
> Never trust this file for either of those.

## Tags

- `active` — the pattern being acquired now. Exactly one at a time.
- `core` — cleared. In the retention rotation.
- `excluded` — not reached yet. Never drill.

## Buckets — in learning order

| # | Bucket | Covers | Tag |
|---|---|---|---|
| D1 | Arrays & hashing | frequency maps, prefix sums, in-place tricks | active |
| D2 | Two pointers | converging, fast/slow, partition | excluded |
| D3 | Sliding window | fixed, variable, with hashmap state | excluded |
| D4 | Stack | monotonic stacks, matching, spans | excluded |
| D5 | Binary search | on arrays, on answer space, boundaries | excluded |
| D6 | Linked lists | reversal, merge, cycle, dummy-head hygiene | excluded |
| D7 | Trees | DFS/BFS, recursion contracts, BST invariants | excluded |
| D8 | Heaps | top-k, k-way merge, two-heap median | excluded |
| D9 | Backtracking | subsets, permutations, pruning | excluded |
| D10 | Graphs | BFS/DFS on grids & adjacency, topo sort, union-find | excluded |
| D11 | Intervals | sort-then-sweep, merging, meeting rooms | excluded |
| D12 | Greedy | exchange arguments, when greedy is provably right | excluded |
| D13 | 1-D DP | memo → tabulation, house-robber / climb family | excluded |
| D14 | 2-D DP basics | grids, two-sequence (LCS/edit distance) | excluded |

When D1 clears, retag it `core` and retag D2 `active` — and so on down
the list.

## Choosing the session's problem — first match wins

1. **Redo due** — a `timebox` or `hint-assisted` miss from 1–2 weeks ago,
   in a new disguise. Same mechanism, new skin, never the same story.
2. **Retention ambush** — every 4th session, a `core` bucket: never-tested
   first, then longest-untested (compute from the archives). Medium.
3. **Active pattern** — the default. Difficulty ladder below.

Rules that always apply:
- (TEACH FIRST) items are taught, not asked; retest them the *following*
  session (this outranks everything above that day).
- Never repeat a problem or near-variant from the archives.
- Constraints imply the intended complexity; the problem never names it.

## Difficulty ladder & clearing a pattern

- First exposure to a bucket: one easy as the baseline. Then mediums only.
- A bucket clears (→ `core`) after **3 clean mediums**: unaided, in the
  timebox, complexity stated correctly. Hinted or overtime solves don't
  count toward the three.
- Cleared buckets come back via the retention ambush. Fail one → the bucket
  goes back to sharing `active` duty until one clean medium restores it.

## Teach before retesting

A mechanism that has failed **twice or more** gets marked (TEACH FIRST) in
misses-dsa.md. Explain it at the start of the next session — smallest
possible example — and retest the session after, in a new disguise.
Never fail someone twice on something that was never explained.

## Phases

- **Acquisition (now → ~3 months in):** the ladder above, buckets in order.
- **Mixed (after D14 clears → mock phase):** no `active` bucket; every
  session is a random `core` medium or a due redo. Recognition is the skill.
- **Mock (final ~6–8 weeks before applications):** DSA goes daily (flip the
  tracker's rep alternation; the JS/TS quiz drops to ~2×/week maintenance).
  Sessions become timed rounds: two problems, 70 minutes total, approach
  spoken first, one follow-up each. Occasionally company-flavored.

## When things change

- Pattern cleared → retag here → commit → **re-upload this file to project
  knowledge** (the one manual sync).
- Entering a new phase → update the phase note above the same way.
