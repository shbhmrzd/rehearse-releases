# Try Rehearse and tell us what gets in the way

Rehearse 0.5 is a public beta for turning a note into a short practice session. All plugin features are free. Install from [Obsidian's Community directory](https://community.obsidian.md/plugins/rehearse) using the [installation guide](../README.md#installation), or download the ZIP from [the public release](https://github.com/shbhmrzd/rehearse-releases/releases/tag/0.5.0). You do not need a second AI plugin or a Rehearse account.

This is voluntary feedback, not an exam. Skip any step or stop at any time. Rehearse sends no usage analytics. Share only what you choose in the template below; a topic description is enough, and private notes, keys and account details are not needed.

## First session: about ten minutes

1. Install Rehearse using the [installation guide](../README.md#installation). In Obsidian, run **Rehearse: Open practice** from the command palette. No developer CLI is required.
2. Choose **Try the sample**, inspect the five prepared questions, then **Practice selected**. Answer before revealing and compare with the checklist. Note the first control or instruction that confuses you.
3. To try your own material, open Rehearse's **Settings**. Configure a provider you already use, refresh its models, select a text model and save. The [setup guide](SETUP.md) explains cloud and local choices. Cloud generation may cost money at your provider; local AI requires your own running runtime. If you do not have either, skip generation and continue with the sample or a manual card.
4. Open a short Markdown note on a subject you want to remember. Run **Rehearse: Practice this note**, or select one passage and run **Rehearse: Practice selected text**. Enter a concrete learning goal and create five questions. Record how long setup and generation took separately, if convenient.
5. Before saving, classify each draft once: **keep unchanged**, **keep after editing**, or **reject**. Check whether its quotation supports the answer. Look for repeated questions, irrelevant detail and missing qualifications. Edit or deselect drafts, then practice the ones you want.
6. Save one or two useful cards. Close and reopen Obsidian and confirm they are under **My cards**. Try a due review or **Practice all**, then export Markdown if you want a portable copy.

If you get stuck, record the step and visible error, then stop that step. There is no need to regenerate repeatedly or buy API credit for the beta. A blank password field can still mean a key is stored: check **Saved connections → Key saved in Obsidian**.

## Return when it is useful

After three to seven days, decide whether to open Rehearse again. There is no automatic reminder or tracking. If you return, try recalling the material before revealing the answers. Tell us whether it helped and what made you return. If you do not return, that is useful feedback too.

## Copy-and-fill feedback

Send this through the channel the maintainer used to invite you, or a [public repository issue](https://github.com/shbhmrzd/rehearse-releases/issues). Please use an invented or public example when reporting question content.

```text
Rehearse / Obsidian version and device:
What I wanted to learn (topic only):
How I revise this material today:

Sample: completed / needed help / stopped at step __
AI setup: already configured / configured myself / needed help / skipped
Provider and model (no key or account details):
Saved connection and key status were clear: yes / no — because:
Own-note generation: succeeded / failed / skipped
Visible error, if any:

Drafts generated: __
Keep unchanged: __  Keep after editing: __  Reject: __
Main reasons for editing/rejecting:
  irrelevant detail / duplicate idea / unsupported answer /
  missing qualification / unclear question / other:
Approximate setup time: __  Generation wait: __  Editing time: __
Was this easier than my current process? Why?
Saved cards survived reopening: yes / no / not tried

After 3–7 days: returned / did not return / not reached yet
Why I returned or did not return:
An example of something I could explain or apply later (optional):
One improvement that would make me use this again:
```
