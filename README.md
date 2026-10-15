# how-long

[한국어](README.ko.md) · v0.5.0 · [MIT license](LICENSE)

`how-long` asks an AI assistant to give one time estimate before starting your task. It uses the available context, identifies important uncertainty, and then continues with authorized work. If you only asked for an estimate, it stops after reporting.

The skill is a Markdown instruction file. It needs no extra program or background service.

## Use it

Download this repository with **Code → Download ZIP**, extract it, and rename the folder to `how-long` if you want to use the example path below.

For an assistant that can read local files, adjust the path and ask:

> Read how-long/SKILL.md. Estimate the time first, then change the button text from “Save” to “Send” and check the result.

If it cannot read files, paste [SKILL.md](SKILL.md) into the conversation before your request. Apps with native skill support can load the folder from their documented skill location. Where `$skill-name` invocation is supported:

```text
$how-long Estimate the time first, then fix the submit button.
```

For every-task use, add this to your app's supported user or project instructions, using the correct path:

> Before starting each task, read and apply how-long/SKILL.md.

Downloading the folder alone does not activate it. Installation and invocation vary by app.

## How it estimates

After reading required instructions, the assistant reports immediately if the context is sufficient. Only a material unknown can justify extra investigation: at most two small, independent read-only checks in one parallel batch, or one if parallel calls are unavailable. This cap applies to estimation research, not required instruction reads or the work afterward. It skips lookups that merely refine precision and does no editing, building, testing, installation, or substantive research before reporting.

The estimate covers elapsed time from the report to final delivery. It includes reasoning, writing, tool calls and waits, required verification, saving, and necessary rework. Preliminary checks are outside that duration. Unpredictable user, approval, and external waits are identified separately; only bounded portions are estimated, with exclusions stated.

The assistant uses the likely execution path without mandatory scenarios. Sequential work adds up. Actual parallel work follows the longest chain of dependent steps, including coordination and combining results. Observed runtimes apply only to similar commands and conditions: cached and initial runs can differ, and a timeout is not an expected runtime. It does not invent processing rates, retry probabilities, time per file, or blanket padding, copy human development times, or cap all AI work at a few seconds or minutes.

## Evidence and uncertainty

Version 0.5.0 makes three distinctions explicit:

- Without comparable timing evidence, label the result a rough estimate based on the task. Clear, bounded work can still be estimated without timing history.
- Claims about measurements, logs, history, checks, or completion need evidence. A duration reported by the user must not be presented as the assistant's own measurement.
- If no defensible estimate or range is possible, say so and name one missing condition. Do not make up a number just to fill the output format.

For example, changing supplied button text gives the assistant a clear scope for a rough estimate. A claim that “this project's tests average one minute” needs actual evidence. Knowing the task does not establish that average.

## Output

Use one content line, or at most two when needed, in the user's language. Start with a rounded estimate when one is defensible. Add a range and its main cause only for important uncertainty; the estimate must lie within the range. Give a breakdown only if requested.

An example when comparable timing evidence is unavailable follows. Brackets are replaced with task-specific values; the second line is optional.

> ### 🟦 Estimated duration: about [time] (rough, task-based estimate)
>
> Expected range: [lower] to [upper]. [Main uncertainty]

Use this heading only when Markdown headings are supported and allowed. Otherwise use plain text, respecting any format the user requested. When no useful estimate is possible, a report can instead say:

> I cannot estimate the duration from the current information. The scope of the migration is unspecified.

Ranges describe plausible outcomes, not statistical confidence intervals or guaranteed maxima. Change them only with changed evidence, never to fit a deadline or hide uncertainty. This does not introduce periodic updates.

## Limits and files

The estimate does not justify skipping required verification or claiming completion. Existing approval conditions still apply. Normal task communication continues.

There are no timers, saved timing histories, automatic learning from past errors, countdowns, periodic ETA updates, or measured completion-time reports. The instructions have not been shown through behavioral or performance testing to reduce latency, prediction error, or fabricated claims.

[SKILL.md](SKILL.md) contains the instructions. `agents/` and `assets/` hold optional skill-display metadata and an icon, not message formatting controls. They are unnecessary when supplying the instructions as text.

Use, modify, and share under the [MIT license](LICENSE), retaining its copyright and license notice.
