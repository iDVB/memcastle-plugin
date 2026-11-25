# Shared buckets: policies, pending items, proposals, findings

The team's shared space is written by several people and their agents, so its buckets have rules the Personal space
mostly doesn't. The receipt always says what happened; this page explains why.

## Write policies

Each bucket has a write policy (`memory_buckets` with `detail: true` shows it as `writePolicy`):

| writePolicy | What a save does | Receipt |
|---|---|---|
| `immediate` | Live at once | `status: "live"` |
| `undo` | Held for an undo window, then live (`undoSeconds`) | `status: "pending"`, `liveAt` |
| `approval` | Waits for someone who can approve | `status: "proposed"`, `proposalId` |

A person can also set **"always ask me"** for their own agents in the console. Then all of that person's agent
saves become proposals for them, in every bucket.

Some writes need approval whatever the bucket says:
- An `instruction` or a pinned item in the shared space: a space admin approves (it steers everyone's agents).
- An `instruction` or pinned item written by an agent, even in Personal: the person approves.
- Content from Personal written into the shared space: the person approves (`reason: "cross_space"`).

## Pending items and the undo window

- `pending` means nobody else sees it yet. "Undo that" within the window → `memory_undo`: discarded unseen.
- After `liveAt` it's live; undo then deletes it (recoverable for 7 days).
- Your own pending items in Personal behave the same way.

## Proposals

- `proposed` means it waits for a decision. Tell the person in the receipt line; don't save it again elsewhere to
  get around the wait.
- `memory_undo` on a proposed item withdraws it.
- `memory_propose` asks for something to be added to a bucket even where you could write directly, or moves one of
  your memories there via approval. Use it when the person says "suggest this for the team handbook" or wants a
  teammate to check it first.
- Approving happens in the Memcastle console, by someone with write access to the bucket (or a space admin for
  instructions). Agents don't approve proposals.

## Findings

`memory_findings` lists things a person should decide: conflicting values, duplicates, out-of-date facts, misfiled
items. Show the ones the person asks about, in plain words, with the options. After they choose, apply it with
`memory_resolve`:

| choice | Means |
|---|---|
| `changed` | The newer value is current; the old one becomes history (`changedAt` if they said when) |
| `wrong` | One value was a mistake; `keep` is the id of the right one |
| `keep_both` | Both are true (different contexts) |
| `cancel` | Drop the new value |
| `merge` | Duplicates: keep one |
| `ended` | An open fact is over (a membership, a subscription) |
| `dismiss` | Not a problem |

Never resolve a finding the person hasn't decided. Mention open findings only when they're relevant, or when the
session digest shows some and the person seems to want a tidy-up.

## Rules

`memory_rules_get` shows the never-save rules (the baseline, the space's own, the person's), the person's save and
skip phrases, and the caps on own-initiative saves. A refused save returns `filed: false` with a `line` that says
which rule; repeat it and move on.
