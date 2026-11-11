# Model specialization and evaluation proposal

**Status:** Proposed evaluation work; no model, provider, training run, threshold, or product behavior is selected.

## Why this fits

Idea Generator already assigns providers per role and calibrates its jury against reference ideas. That is a practical starting point for the video’s method: assess each bounded job on reviewed examples, keep a difficult holdout for comparison, and specialize only when results show a meaningful advantage. This proposal extends evaluation discipline; it does not prescribe fine-tuning.

## Evaluate roles separately

Use the same reviewed cases and role-specific rubric to compare the current configuration with relevant hosted, base open-weight, and local candidates. Include the current workflow as a baseline. Record exact model/provider, prompt, tools, and case-set version.

| Role | Useful evaluation signals |
|---|---|
| Judge | Agreement with independent human ratings; gold precision and false-gold rate; consistency across paraphrases; quality of reasons and keywords |
| Branch / cross | Goal fit, distinctness from existing ideas, feasibility, useful recombination, duplicate rate |
| Distill / summary | Fidelity to source ideas, preservation of caveats, useful synthesis, unsupported additions |
| Research / X scouts | Citation support, source relevance to the board goal, freshness, and whether the lead says what the cited source supports |
| Project brief | Correct lineage and constraints, actionable MVP, explicit unknowns, no invented implementation or approval |
| Autopilot | Quality of the resulting idea set per step and dollar; diversity and goal fit over a fixed number of steps; error/backoff behavior |

The existing npm run calibrate reference ideas can remain a quick judge-calibration check. Keep a separate, stable holdout that is not used to adjust prompts, thresholds, or training examples. Preserve difficult cases and examples where attractive scores hid weak ideas. Avoid treating judge-to-judge agreement as truth; the scoring guide and labels should be reviewed independently.

## Proposed experiment

1. Choose one role and a small reviewed set of real or permissioned board examples, including ordinary, ambiguous, and previous failure cases.
2. Write the rubric and critical failures before comparing models. For judging, include false golds, over-penalized good ideas, and inconsistent paraphrase cases.
3. Freeze a holdout; keep it out of prompt iteration, synthetic-data generation, and fine-tuning.
4. Compare the current role model, a capable hosted baseline, and one or more relevant local/base models on identical context.
5. Report per-category rubric results, goal relevance, diversity/duplication where applicable, cost per useful result, latency, and human review time.
6. Add a narrow output evaluator only where it can verify a concrete requirement, such as valid schema, preserved source attribution, or no unsupported project-brief claims. Calibrate it on known pass/fail cases.
7. If fine-tuning is later justified, use reviewed training examples and compare the tuned candidate against the same untouched holdout. Keep model choice per role.
8. Change production defaults only through a separately reviewed implementation and release decision.

## Boundaries and open questions

- Model scores are decision support; board owners remain responsible for choosing ideas and project scope.
- Scouts must retain source support. A citation’s presence does not establish that it supports every generated claim.
- Existing per-role provider choices, budget limits, and server binding remain unchanged by this proposal.
- There is no agreed evaluation set size or pass threshold yet. Set these with the role owner before the experiment.
