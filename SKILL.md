---
name: how-long
description: >-
  Estimate task duration once before execution. Use when the user requests
  a pre-task estimate, says 작업 전에 예상 시간을 알려줘, or enables
  estimates as a standing instruction.
---

# How Long Will It Take?

## Estimate

After required instructions, report immediately if context suffices. Only for a material unknown, allow at most two small, independent read-only checks in one parallel batch, or one check without parallel calls. This cap covers extra estimation research only. No pre-report edits, builds, tests, installs, or substantive research; skip lookups that merely refine precision.

Estimate elapsed time from report to final delivery, including reasoning, generation, sequential tool calls and waits, required verification, saving, and necessary rework. Use the likely execution path; no mandatory scenarios. For actual parallel work, use the longest dependency path plus coordination and integration.

Reuse observed runtimes only for similar commands and conditions: distinguish cached and initial runs; timeouts are not expected durations. Do not substitute human development times, impose universal AI time limits, or invent time per file, throughput, retry probabilities, or padding percentages.

## Ground the report

Separate observations from predictions. Claims about measurements, history, logs, checks, or completion require evidence; distinguish supplied reports from direct observation.

Without comparable timing evidence, label the result a rough, task-based estimate. Missing history alone does not prevent estimating clear, bounded work. If no defensible estimate or range is possible, state that and one missing condition instead of inventing a number. Identify unpredictable user, approval, or external waits separately; estimate only bounded portions and label exclusions.

## Report once

Use the user's language and requested format: one content line, at most two if needed. Lead with a rounded estimate when defensible. Add a range and main uncertainty only when material; the estimate must lie within the range. Breakdowns only on request.

Ranges describe plausible outcomes, not statistical confidence intervals or guaranteed maxima. Adjust only with changed evidence, never to fit deadlines or hide uncertainty. Use `### 🟦` only when Markdown headings are supported and allowed; otherwise plain text.

Proceed with authorized work, preserving approval conditions. Stop after reporting if only an estimate was requested. Never omit required verification or claim completion to meet the forecast.

No timers, saved timing history, countdowns, periodic ETA updates, or measured completion-time reports. Normal task communication remains unchanged.
