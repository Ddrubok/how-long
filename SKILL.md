---
name: how-long
description: >-
  Estimate task duration once before execution. Use when the user requests
  a pre-task estimate, says 작업 전에 예상 시간을 알려줘, or enables
  estimates as a standing instruction.
---

# How Long Will It Take?

## Before the report

After reading required instructions, report immediately without extra tool lookups if the supplied context is sufficient.

Only when an unknown could materially change the estimate, make at most two small, independent read-only checks in one parallel batch. If parallel calls are unavailable, make at most one check. This limit applies only to extra investigation for estimating, not required instruction reads or the work after the report. If tools are unavailable, use the supplied context.

Before reporting, do not edit files, run builds or tests, install anything, or begin substantive research. Express remaining important uncertainty as a short assumption or range.

## Estimate

- Estimate elapsed time from the report until final delivery, including required verification, saving, and ordinary tool waits. Identify unpredictable user-response, approval, and external waits separately. For open-ended scope, estimate only the bounded part and label any excluded waits.
- Use the most likely execution path, accounting for model reasoning and generation, sequential tool calls, command waits, and necessary verification and rework. Do not require three scenarios for every task.
- Reuse existing runtimes only for similar commands and environment conditions. Distinguish cached runs from initial runs; a timeout is not an expected runtime.
- Add sequential work. For actual parallel work, use the longest dependency path and include coordination and result integration. Do not assume unavailable concurrency.
- Do not copy human development times or cap all AI tasks at a few seconds or minutes. Do not invent fixed time per file, throughput, retry probabilities, or a blanket padding percentage.

## Report and proceed

Report once in the user's language: one content line by default, at most two when needed. Lead with one appropriately rounded, most likely estimate. Add a range and its main cause only for important uncertainty; the estimate must lie within the range. Provide a phase-by-phase breakdown only when requested.

A range describes plausible outcomes, not a statistical confidence interval or guaranteed maximum. Base any range adjustment on changed evidence; never shrink or widen it to meet a deadline or conceal uncertainty.

Respect the user's explicit output format. Use a `### 🟦` heading only when Markdown headings are supported and allowed; otherwise use plain text. For example: `Estimated duration: about [time]`, replacing the placeholder and translating as needed.

After the report, proceed with already-authorized work while preserving existing approval conditions. If only an estimate was requested, stop after reporting.

## Scope

Add no timers, saved timing history, countdowns, periodic ETA updates, or measured completion-time reports. Leave normal task communication to the host's instructions. Keep execution instructions free of product-specific commands and installation paths.
