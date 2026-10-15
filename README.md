# how-long

[한국어](README.ko.md) · v0.4.0 · [MIT license](LICENSE)

`how-long` asks an AI assistant to estimate task duration once before starting work. After reading the required instructions, it reports immediately when the supplied context is sufficient. It then continues with the work you authorized. If you only asked for an estimate, it stops after the report.

A skill is a set of instructions an AI can follow. This one is written in Markdown, a text format that supports headings and lists. It needs no extra program or background service.

## Try it

Download this repository using **Code → Download ZIP**, then extract it. You can rename the extracted folder to `how-long` for the examples below.

If your AI assistant can read local files, give it this request, adjusting the path to match your folder:

> Read how-long/SKILL.md. Estimate how long the following task will take, then do it: change the submit button text from “Save” to “Send” and check the result.

If the assistant cannot read files, paste the contents of [SKILL.md](SKILL.md) into the conversation before your task. It must receive those instructions to follow them.

Apps with built-in skill support can load the folder from their documented skill location. Installation paths and invocation syntax vary by app. In apps that support `$skill-name` invocation, you can use:

```text
$how-long Estimate the time first, then fix the submit button.
```

For every-task use, add this to your app's supported user or project instructions, with the correct path:

> Before starting each task, read and apply how-long/SKILL.md.

Simply downloading the folder does not enable it for every task.

## How it estimates time

The estimate covers elapsed time from the report until final delivery, including required checks, saving, and ordinary tool waits. Preliminary checks before the report are outside that duration. Unpredictable waits for a user response, approval, or an external service are identified separately. If the scope is open-ended, only the part that can be bounded is estimated.

When the available context is enough, the assistant makes no extra tool lookups. If an unknown could substantially change the estimate, it may make at most two small, independent read-only checks together in one parallel batch. If parallel calls are unavailable, the limit is one check. This cap applies only to extra investigation for the estimate, not reading required instructions or doing the task after the report. No editing, builds, tests, installations, or substantive research happen before the estimate.

The assistant estimates the most likely route through the work: reasoning, writing, sequential tool calls and waits, verification, and necessary rework. It does not have to construct three scenarios for every task. Remaining important uncertainty is expressed as a short assumption or range.

Existing runtimes are useful only when commands and conditions are similar. A run that reuses cached results can differ from an initial run; a timeout sets a waiting limit, not an expected duration. Sequential work is added together. For work that actually runs in parallel, the estimate follows the longest chain of dependent steps and includes coordination and combining the results.

Human development times, fixed time per file, invented processing speeds or retry probabilities, and blanket padding percentages are not used. AI work is not assumed to fit a universal seconds-or-minutes limit.

## What you will see

The report uses your language and normally takes one content line, or at most two when needed. It starts with one rounded estimate. A range and its main cause are added only for important uncertainty, and the estimate must lie within that range. A breakdown by step is provided only if you ask.

When Markdown headings are supported and allowed, the report can look like this. Brackets are replaced with values for your task:

> ### 🟦 Estimated duration: about [time]
>
> Expected range: [lower] to [upper]. [Main reason the time may vary]

Otherwise, it uses plain text:

```text
Estimated duration: about [time]
```

An explicitly requested output format takes priority. After reporting, the assistant proceeds only with authorized work and keeps any existing approval conditions.

## Limits

A range describes plausible outcomes. It is not a statistical confidence interval or a guaranteed maximum. A range is adjusted when the evidence changes, not to fit a deadline or hide uncertainty. This does not add periodic updates.

The skill does not run timers, save timing history, learn from past estimation errors, count down, or report measured time after completion. Response speed, tool delays, and unexpected failures can still affect the result. Faster reporting and lower prediction error have not been demonstrated through performance measurements.

## Files and license

The instructions are in [SKILL.md](SKILL.md). The `agents/` and `assets/` folders contain optional display metadata and an icon; they do not control message text formatting. They are not required to follow the instructions as text.

You may use, modify, and share this skill under the [MIT license](LICENSE). Keep the copyright and license notice when distributing copies.
