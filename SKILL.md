---
name: how-long
description: Report a best estimate of the total task duration once, before starting the user's requested work. Use when the user requests a pre-task time estimate, asks how long an upcoming task will take, says 작업 전에 예상 시간을 알려줘, or has enabled this skill as a standing instruction for tasks. Works as plain instructions in CLI agents or any AI that can read Markdown; no scripts, runtime, hooks, or service integration required.
---

# How Long Will It Take?

Do one thing: tell the user the estimated duration before doing the requested work.

## Estimate before execution

1. **Define completion.** Identify the requested deliverable, acceptance checks, saving, and final delivery. Estimate wall-clock time from this report until delivery, not human developer effort or compute time alone. Include ordinary tool waits and required verification. Identify unpredictable user, approval, or external-service waits separately; a numeric estimate that excludes them is only for the bounded work, not the total.
2. **Resolve the dominant uncertainty cheaply.** If essential, make only a few targeted read-only checks, such as reading the relevant file, existing failure output, or test configuration. Check the unknown most likely to change the estimate: whether the feature already exists, whether a test command is available, or whether a dependency is missing. Do not edit files, start implementation, run builds or benchmarks, or perform substantive research before reporting. Stop inspecting when further detail is unlikely to change the rounded estimate. If tools are unavailable or forbidden, use supplied context.
3. **Estimate concrete operations.** Break the actual route to completion into a few units: remaining inspection, editing or creation, tool execution and waiting, verification, and delivery. Estimate generation and reasoning effort as well as tool time. Use available evidence as described below; file count or a label such as "simple" is not a duration. Count only necessary work, and include setup or downloads only when this task needs them. Sum sequential work; for actually available parallel work, use the longest dependency path plus coordination and integration. Do not assume workers, concurrency, or overlap that the task will not use.
4. **Build plausible scenarios.** Estimate a clean run, the most plausible route, and a slower route involving a concrete risk found in the context. Possible risks include an unresolved cause, an unavailable dependency, or a failing check requiring repair and rerun. Repeated work belongs only in the scenario where it occurs; do not count it again as a generic buffer. Use the most plausible route as the point estimate, not an automatic midpoint or the clean run. Material uncertainty calls for a range spanning plausible faster and slower routes; the upper end is not a guaranteed maximum. If no particular complication is supported, do not invent one. For genuinely undefined scope or an unbounded external queue, state what cannot be estimated and, if useful, estimate only the bounded portion.
5. **Sanity-check and report.** Check for missing verification, double-counted tool waits, fictional parallelism, and a total inconsistent with the required operations. Round to the precision the evidence supports; a short task may take seconds and must not be inflated to a fixed minimum number of minutes. Avoid second-level precision for longer or poorly understood work. Send one short report in the user's language **before substantive execution**, then proceed with already-authorized work. If the user requested an estimate only, stop after it. Do not create an extra permission step; preserve approval boundaries that independently apply to the underlying task.

### Evidence and uncertainty

- Prefer relevant facts already visible in this task or conversation: actual tool durations in supplied output, existing code, test commands, environment readiness, and known dependency steps. Use a runtime only when the command and conditions are comparable; a timeout setting is not a typical runtime, and a cached run does not establish a cold-start duration. Do not create or retrieve a separate timing history.
- Where direct evidence is missing, make an explicitly rough estimate of the concrete work. Do not invent measured throughput, model speed, historical averages, retry probabilities, or a fixed minutes-per-file conversion. This skill does not know provider load or future reasoning time.
- A range describes plausible scenarios, not a calibrated confidence interval. Do not label it "80% confidence", "accurate within 10%", or measured error without supporting measurements. Do not apply a universal percentage margin, automatic multiplier, or weighted three-point formula with invented probabilities.
- Narrow the range only when task evidence removes uncertainty. Do not merely widen every range to make predictions harder to disprove, or shrink it to satisfy a requested deadline. If evidence remains limited, say so briefly and name the main uncertainty. No history is retained, so accuracy improvements cannot be claimed from these rules alone.

## Output

Lead with a single approximate duration. Keep the default report to one content line, at most two; a blank line between Markdown blocks does not count. For material uncertainty, put the plausible range and its main cause on the second line; identify excluded waits when applicable. The point estimate must lie within its range. A routine task with little uncertainty can stay on one line. Show a phase breakdown only if the user asks for one. Treat all numbers as predictions, not measured facts or guarantees.

### Portable emphasis

- For Markdown output, use a level-three heading with one blue square: `### 🟦 예상 소요 시간: 약 [예상값과 단위]`. Keep the text in the host's theme color so it adapts to light and dark backgrounds. The square is a decorative accent; the words convey the full meaning. Use this format when the renderer is unknown; do not run tools or ask a question just to discover formatting support.
- If headings are unavailable or disallowed but bold is supported, use `🟦 **예상 소요 시간: 약 [예상값과 단위]**`. For a known plain-text-only host, use `예상 소요 시간: 약 [예상값과 단위]` without Markdown syntax. Omit the square if emoji are unsupported or unwanted. Respect an explicitly requested output format.
- Where native rich-text styling is explicitly supported, prefer bold text about 1.25 times the body size with accent blue `#2F78C4`. Its calculated contrast is about 4.56:1 against pure white and 4.60:1 against pure black. For other backgrounds, use the host's accessible theme color if contrast is uncertain. Do not force a background color.
- A skill cannot guarantee font sizes or arbitrary text colors across hosts. Markdown heading size and emoji appearance depend on the renderer. Do not emit raw HTML, CSS, ANSI escapes, images, or shell output to simulate chat styling. Optional UI metadata and the icon affect supporting skill interfaces, not the estimate's message text.

Templates below deliberately contain no sample durations. Replace every bracketed field with a task-specific estimate or supported condition; do not print placeholders:

```markdown
### 🟦 예상 소요 시간: 약 [예상값과 단위]

예상 범위 [하한]~[상한과 단위]. [범위를 좌우하는 주요 조건]
```

```markdown
### 🟦 Estimated duration: about [estimate and unit]

Plausible range: [lower] to [upper and unit]. [Main source of uncertainty]
```

Use the selected formatting directly in the report, without a code fence or a separate explanation of the formatting. Do not add a numeric total when the estimation rules above say it cannot be bounded.

## Keep the scope narrow

Add only the pre-task report. Do not start timers, collect history, save timing data, track progress, revise a countdown, send periodic ETA updates, or report measured completion time as part of this skill. Leave normal task execution and any host-required communication to the host's instructions.

Use no product-specific commands, paths, model identifiers, shell syntax, or tools. The host must load these instructions before the task; do not claim that installing a file automatically activates it in every CLI. A host without native skill support can follow this same Markdown when explicitly supplied as instructions.
