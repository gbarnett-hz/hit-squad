# hit-squad

A collection of agent skills, installable with the [skills.sh](https://skills.sh) CLI.

## Skills

### root-cause-cabal

A root-cause investigation run as a cabal of deranged, manically obsessive engineer personas. Each persona investigates an issue from a conflicting lens (logs, git history, state invariants, integration boundaries, environment, dependencies), they argue with each other under an arbiter who kills trivial quarrels and enforces evidence, and the surviving analysis is handed to an RCA author who writes a coherent research document.

The derangement is flavor; the epistemics are strict — every claim cites an artifact, every rival hypothesis is entombed with evidence or presented honestly as a split verdict.

**Install** (from a cloned checkout or via the skills.sh CLI once published):

```bash
npx skills add <owner>/hit-squad
```

**Usage:**

```
/root-cause-cabal "checkout API 500s under load since Tuesday" --size 4
/root-cause-cabal "reconcile job corrupts ledger rows" --size 5 --contrarian
/root-cause-cabal flaky test: test_invoice_reconcile fails 1-in-20
```

- Default cabal size is 3; specify 2–6.
- Add `--contrarian` for The Deranged Skeptic: an adversarial member who contests the finer details, asks the challenging questions, and never has the answers. They sit outside the cabal size count, and unanswered objections are reported honestly in the RCA document rather than buried.
- The cabal investigates read-only and produces `RCA-<slug>.md` in your workspace.

See [skills/root-cause-cabal/SKILL.md](skills/root-cause-cabal/SKILL.md) for the full workflow and [skills/root-cause-cabal/references/](skills/root-cause-cabal/references/) for the persona roster, arbiter protocol, and RCA template.
