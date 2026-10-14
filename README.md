# how-long

[한국어](README.ko.md) · v0.3.0 · [MIT license](LICENSE)

`how-long` asks an AI assistant to estimate how long a task will take before it starts. The estimate includes the work, the necessary checks, and delivery of the result. After reporting it, the assistant continues with the work you requested. If you only asked for an estimate, it stops there.

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

## What you will see

The assistant gives a short estimate in your language. This template shows the format; the brackets are replaced with values for your task:

> ### 🟦 Estimated duration: about [time]
>
> Expected range: [lower] to [upper]. [Main reason the time may vary]

For a straightforward task, the first line may be enough. A task with an unknown cause or an uncertain setup may also need a range and a short explanation.

## How it estimates time

1. **Define the finish.** Include any checks, saving, and delivery needed to complete your request. The estimate covers the time from the report onward.
2. **Check what could change the plan.** Read relevant files or existing error messages when needed. For example, an existing feature may need a small adjustment instead of a new implementation.
3. **Estimate the actual steps.** Account for investigation, editing, tool execution, waiting, and verification. A required build takes time even when the code change is small.
4. **Consider likely complications.** Compare a clean run with the most likely route and a slower route supported by the available evidence. Include repair and another test run when there is a reason to expect them.
5. **Report a rounded estimate.** Give the most likely duration, plus a range when the uncertainty matters. Avoid precise-looking numbers when there is little evidence.

Changing button text and fixing a button that sometimes fails might both involve one file. The second task also needs investigation. Estimating those steps separately helps account for the difference. Work done in sequence is added together; work that really can run at the same time is counted by the path that finishes last, including any final integration.

## How much to trust the estimate

The assistant predicts a duration from the information available. It does not run a timer, save timing history, or learn from previous estimation errors. Model response speed, tool delays, and unexpected failures can change the outcome.

The range describes plausible ways the task could unfold. It is not a measured error margin or a promise that the task will finish within it. No measured reduction in prediction error has been established for this version.

If an external wait has no known end, such as waiting for approval, the assistant identifies that wait separately. Any estimate for the remaining work excludes it. Time spent on preliminary checks before the estimate is also outside the reported duration.

## Appearance

The default uses a heading and one blue square to make the estimate easy to find. The text follows the app's light or dark theme. Apps with fewer formatting options can show bold or plain text instead.

Actual font size and color depend on the app. Where direct text styling is available, the skill suggests bold text at about 1.25 times the body size in blue `#2F78C4`. The optional icon and UI settings describe the skill in supporting apps; they do not control chat-message colors. [SKILL.md](SKILL.md) contains the full display rules.

## Files and license

The instructions are in [SKILL.md](SKILL.md). The `agents/` and `assets/` folders contain optional display metadata and an icon. They are not required to follow the instructions as text.

You may use, modify, and share this skill under the [MIT license](LICENSE). Keep the copyright and license notice when distributing copies.
