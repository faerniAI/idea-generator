---
name: real-work-model-evaluation
description: Design evidence-led evaluations for model specialization, fine-tuning, and task-level model replacement using real work, held-out benchmarks, and output checks.
---

# Real-work model evaluation

Use this skill when deciding whether to assign a model a bounded role, compare hosted and local models, generate training examples, fine-tune, or gate model outputs before delivery.

## Method

1. **Bound the job.** Name the input, expected output, user or downstream decision, and the failure that matters. Keep different jobs separate; do not judge a broad model by one aggregate score.
2. **Set data boundaries.** Use examples only when their source, permission, sensitivity, retention, and intended use are understood. Minimize or anonymize data where practical. Record provenance and transformations.
3. **Build a case set from actual work.** Include ordinary work, edge cases, ambiguity, and prior costly mistakes. For each case, define a marking guide and severity for errors. Have a domain reviewer validate expected outcomes.
4. **Separate development from evaluation.** Keep training and prompt-development examples distinct from a stable held-out benchmark and answer keys. Generate variations only from approved, reviewed seeds. Do not let model-generated cases silently define correctness.
5. **Establish fair baselines.** Compare the current workflow, a capable hosted model, and relevant prompt/retrieval or base-model options. Compare specialist models on the same inputs, rubric, tools, and context; record model, provider, prompt, tool, and dataset versions.
6. **Measure the whole job.** Report per-category quality and critical failures alongside latency, inference/training cost, human review time, fallback rate, and operational burden. Do not let a strong average hide a severe failure class.
7. **Use output checks when useful.** Prefer deterministic checks for facts that exist in tool results or system state. Use a constrained model evaluator only for interpretation that code cannot reasonably check. Validate it on known passing, failing, and deceptive-but-valid cases; track false accepts and false rejects. An evaluator should inspect evidence already produced, not invent or fetch authoritative state.
8. **Decide whether specialization helps.** Start with instructions and retrieval where they can solve the problem. Fine-tune only when a repeatable gap remains, suitable permissioned examples exist, and a candidate improves the pre-agreed held-out criteria enough to justify data and operating costs.
9. **Roll out proportionally.** Keep outputs advisory and human-reviewed when the job affects money, customers, inventory, legal decisions, physical systems, or other consequential outcomes. Expand only after a bounded shadow or pilot meets its gates. Keep a fallback and a way to stop or revert.

## Decision record

For each comparison, record: task and owner; data permission and provenance; benchmark split; rubric and critical-failure rules; candidate versions; results by category; cost and latency; evaluator error rates if used; human-review findings; decision and remaining unknowns.

## Boundaries

- Benchmark pass rates are evidence for the tested cases, not proof of general capability.
- A model grader is not an independent source of truth. Validate it against reviewed labels.
- Synthetic data can expand variation but cannot validate its own labels.
- A model benchmark never substitutes for physical safety tests, access control, regulatory review, or product approval.
- Do not trigger training, deploy a model, change a live routing policy, or write to a customer system solely because an evaluation passes; follow the owning project’s authorization and release process.
