# Practice, review, and keep your work

Connect your model once using the [setup guide](SETUP.md), or start with the sample and manual cards without AI. The normal workflow is **open note → Practice this note → review questions → practice or save**.

## Choose a useful scope

A single concept or a small group of connected concepts usually makes a better session than an entire manual. Start with a selected passage and a concrete learning goal, such as “Explain when caching can return stale data.”

Rehearse supports general Markdown subjects. It does not need a software repository. Source headings and line numbers remain associated with the selected material. YAML frontmatter is excluded. Operational headings and their subsections are excluded by default; turn them on when they are your subject.

## Preview before committing

Generated cards are drafts. The quote check confirms only that the quoted words occur in the selected source. You still need to verify whether those words support the answer, whether your notes are accurate, and whether the question is worth remembering.

You can edit the question, suggested answer, and checklist. Untick a card to omit it. **Practice selected** starts a temporary session; **Save selected cards** creates Markdown files. The plugin never rewrites the source note.

The sample deck is hand-written. It demonstrates the same preview and practice workflow without pretending to be live generation.

## Practice versus spaced review

**Free practice** is available from a preview or **My cards → Practice all**. It does not change the saved-card schedule. You can think aloud or type an optional response, reveal the answer, and judge yourself. At the end, retry missed questions or save useful cards.

**Spaced review** uses FSRS through `ts-fsrs` to choose the next due date. Each session contains at most ten cards; start another when you want to continue. New introductions are limited to five per local calendar day by default; you can set 0–50 in Settings. Zero pauses new cards without hiding existing due cards.

- **Again:** you could not retrieve the answer.
- **Hard:** you retrieved it with substantial effort or gaps.
- **Good:** you retrieved the important points.
- **Easy:** you retrieved them easily.

Rate your understanding against the checklist. There is no AI grading and no requirement to match the wording. A failed disk write leaves the current question in place for retry. Undo restores the previous schedule; it will not undo a newer rating from another open session.

Keyboard shortcuts apply while focus is outside a text field or button: Space reveals the answer; 1–4 select Again/Hard/Good/Easy for spaced review. In free practice, 1 means Need practice and 2 means Got it. Tab navigation remains available.

## Edit saved cards

Each card is a file under `Rehearse/cards/`. Use **Edit Markdown card** from the library. Keep the metadata comment and these section headings intact:

```markdown
## Question

## Answer

## Answer checklist

## Source evidence
```

Edit the question, answer, and one checklist item per line. Avoid reusing the reserved section headings inside those sections; use third-level headings for additional structure. Choose **Refresh** in My cards after editing. The stable ID in the metadata comment preserves review history even when the wording changes. Renaming the file inside the card folder also keeps the ID; refresh before opening it from the library.

The source metadata and quotation describe the material at creation time. Editing the visible evidence block does not rewrite the source metadata. Automatic repair and source-change regeneration are future work.

To remove a card, move its file to Obsidian's trash, then refresh the library. Rehearse intentionally has no permanent-delete button. Removing the plugin does not delete the Markdown cards.

## Export

**Export Markdown** writes a readable deck with questions, answers, checklists, quotations, and source paths.

**Export for Anki** writes a UTF-8 tab-separated file with Front, Back, Source, and Rehearse ID columns. During Anki import, map Front and Back to your note type's fields; map or ignore the optional fields. HTML is escaped, and newlines use line-break markup. This is a portable import, not two-way sync; repeated imports and edited questions follow Anki's own duplicate-handling settings. FSRS review history is not exported to Anki.

Exports go under `Rehearse/exports/`. If the filename exists, a new numbered filename is used; earlier exports remain untouched.
