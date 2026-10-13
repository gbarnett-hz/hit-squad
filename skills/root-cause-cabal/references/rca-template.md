# RCA Document Template

The RCA author (a subagent) writes exactly one document, `RCA-<slug>.md` (slug: the issue in 4-6 kebab-case words), using this structure. It receives the full debate transcript, the Case Brief, and the hypothesis ledger.

## Author rules

- Plain, precise prose. The cabal's voices stay in the "Cabal Deliberations" section as quotes; findings themselves are emotionless and verifiable.
- Every claim carries a citation: `file:line`, log excerpt with timestamp, commit hash, or command + observed output.
- The author may re-verify any citation before publishing, but may **not** introduce a new hypothesis. If the debate left something unexplained, it goes in Unknowns.
- Distinguish three things explicitly and never conflate them:
  - **Root cause** — the defect or condition that made the failure possible.
  - **Trigger** — the event or change that activated the root cause.
  - **Contributing factors** — what let it persist, hide, or spread (missing observability, swallowed errors, no test).
- If the arbiter declared a **split verdict**, write the document around both survivors: present the leading hypothesis as such, the rival as such, and the discriminating test. Do not pretend consensus exists.
- If The Deranged Skeptic sat in, their ledger is part of the record: objections settled by evidence go where that evidence lives (usually the evidence chain, with a line noting the doubt they answered); unanswered questions get their own honest section — never buried, never inflated into claims.
- Mark clearly what was *executed* vs. *reasoned*. Experiments proposed but not run are labeled `[not run]`.

## Document structure

```markdown
# RCA: <issue title>

**Date:** <date> · **Cabal size:** <n> · **Verdict:** consensus | split · **Confidence:** high|medium|low

## 1. Summary
<3-5 sentences: what happened, why, and the mechanism in brief. A reader who stops here should understand the incident.>

## 2. Observed facts
<The symptom as actually observed: errors, metrics, reproduction conditions. Cited.>

## 3. Timeline
<Ordered causation timeline from cited evidence: when the cause was introduced, when the trigger occurred, when symptoms began, discovery/diagnosis events. Timestamps with sources.>

## 4. Root cause
**Cause:** <one falsifiable sentence>
**Mechanism:** <numbered causal chain, trigger → symptom, every step cited>
**Why this and not something else:** <point to the eliminated rivals below>

## 5. Evidence chain
<The load-bearing citations, each with a one-line explanation of what it proves. The shortest path from artifact to conclusion.>

## 6. Rival hypotheses eliminated
<For each: the hypothesis in one line, who championed it, the evidence that killed it (or why it survived as the rival, in a split verdict).>

## 7. Open sharp questions
<Only if The Deranged Skeptic sat in. The objections that were never settled by evidence: each stated precisely as a question (not a claim), what the Skeptic contested, why it remains open, and the cheapest observation that would close it. Never omit a parked objection; never restate one as a finding. If there were none, write "None — every objection was settled by evidence.">

## 8. Contributing factors
<Why it was possible / why it took so long to find. Includes observability gaps as first-class findings.>

## 9. Confidence and unknowns
<Confidence level and honest justification. Each unknown: what would resolve it, the cheapest test, expected result.>

## 10. Remediation
<Ordered by leverage: fix the root cause, then the contributing factors. Each item: action, why it addresses the cause, a verification step. Concrete proposals only — no "add more logging" without specifying what and where.>

## 11. Cabal deliberations (abridged)
<The argument distilled: each persona in one line, the sharpest exchange of the debate, the Skeptic's most damaging objection and how it ended, and the arbiter's final ruling. This section preserves *why to believe* the analysis — the rivalries, concessions, and the entombed hypotheses.>
```

## Length discipline

The summary, root cause, and evidence chain are the core — never bloat them. The deliberations section is flavor with a purpose: include the exchanges that justify belief, omit the ones that just entertained. A reader should finish in under ten minutes and be able to defend the conclusion without having watched the debate.
