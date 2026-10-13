# hit-squad

That bunch of nerds locked in the special room that nobody dares disrupt. Give them a problem, then get out of their way!

<img src="logo.jpg" alt="The root cause cabal arguing over a bug" width="800">

A collection of agent skills, installable with the [skills.sh](https://skills.sh) CLI — works with opencode, Claude Code, and any other skills-compatible agent.

## Install

```bash
npx skills add gbarnett-hz/hit-squad          # hit-squad, all agents
npx skills add gbarnett-hz/hit-squad -g       # global install
npx skills add gbarnett-hz/hit-squad -s root-cause-cabal -y   # one skill, no prompts
```

## Skill: root-cause-cabal

Point it at an issue — a bug, regression, incident, flaky test, outage — and it runs a root-cause investigation as a cabal of deranged, manically obsessive engineer personas. Each member investigates from a conflicting lens (logs, git history, state invariants, integration boundaries, environment, dependencies), they argue with each other about whose reasoning is better, and an arbiter keeps the quarrel productive: evidence above rhetoric, trivial fights killed, every rival hypothesis either entombed with evidence or honestly reported. Every cabal also seats The Deranged Skeptic — the adversary who contests the finer details and never has the answers. The cabal hands its winning analysis to an RCA author who writes the final document.

The derangement is flavor; the epistemics are strict — every claim cites an artifact.

**Use it:**

```
> find the root cause of the checkout API 500s under load since Tuesday
> why does test_invoice_reconcile fail 1-in-20? assemble the cabal
> root-cause-cabal: reconcile job corrupts ledger rows
```

### Example

```
> root-cause-cabal: checkout API returns 500s under load since Tuesday

Log Whisperer:      First 500 at 14:03:07.219 — 219ms after pool_wait starts.
State-Machine:      Pool exhaustion. The retry path waits twice on the same slot.
Git Historian:      Tuesday: 9c1f2ab touches the retry path. Reading it. Hold on.
Deranged Skeptic:   You assume pool_wait implies starvation. Where's the pool
                    pressure evidence?
Arbiter:            Evidence gavel. Cite the metric or the objection is struck.
Log Whisperer:      pool_pending=64 on every failing host — matches the cap.
Deranged Skeptic:   Fine. But "since Tuesday" — is the window itself even true?
Arbiter:            Log Whisperer, census: failing vs passing shifts. If the
                    window is wrong, every lens is chasing the wrong Tuesday.
Log Whisperer:      Failures start 14:03 — 9 minutes AFTER the resolver
                    migration deployed at 13:54, not at it.
Deranged Skeptic:   Then your migration story needs the migration. Connection?
Git Historian:      9c1f2ab, the resolver migration: adds retry-on-timeout to
                    pool_wait. Each retry re-enters without releasing the slot.
                    Two waits, one slot.
Log Whisperer:      And 14:03 is when p99 latency crossed the timeout.
Deranged Skeptic:   But the deploy was 13:54 — a 9-minute gap. Is the deploy
                    even the trigger, or just load ramping? Unexplained.
Arbiter:            Parked as unknown; needs the request-rate census 13:54–14:03.
                    Verdict: consensus. Retry-on-timeout after the resolver
                    migration double-waits, exhausting the pool under load.

RCA: checkout-api-500s.md — high confidence, 1 parked skeptic question
```

The transcript above is condensed — the real run posts the full debate, then writes `checkout-api-500s.md` with the timeline, cited causal chain, eliminated rivals, and the parked question.

**Options:**

| Option | Default | What it does |
|---|---|---|
| issue (required) | — | What to investigate. Point it at repos, logs, failing tests, incident windows. |
| no-skeptic | off | Every cabal is fixed at six investigators — logs, git history, state invariants, integration edges, environment, dependencies — plus The Deranged Skeptic, an adversarial member who contests the finer details, asks the challenging questions, and never has the answers. Pass `--no-skeptic` to omit them for trivial issues. |

**What you get:**

- The root cause in 2–3 sentences, the mechanism in 3–5 steps, and a confidence level
- The rival hypotheses the cabal killed and the evidence that killed them
- The Skeptic's unsettled objections — as questions, never buried
- `RCA-<slug>.md` in your workspace: timeline, causal chain with citations, eliminated rivals, open questions, unknown list, and remediation proposals

The cabal investigates read-only and never edits your code unless you explicitly ask for a fix.

**Going deeper:** [SKILL.md](skills/root-cause-cabal/SKILL.md) has the full workflow; [references/](skills/root-cause-cabal/references/) has the persona roster, the arbiter protocol, and the RCA document template.
