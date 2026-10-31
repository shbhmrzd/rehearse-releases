# Rehearse

**Make your notes second nature.**

Turn a Markdown note or selected passage into a short practice session inside Obsidian. Review the source evidence, edit questions, and keep only the cards worth revisiting.

All Rehearse features are free. Connect your own cloud provider or local model directly in Rehearse. No companion AI plugin, Rehearse account, backend, or subscription is required. Cloud providers may charge you for API usage. Samples, manual cards and saved-card review need no AI connection.

This repository contains built plugin files and user documentation. The development repository and its history remain private; the bundled JavaScript is publicly readable. Rehearse is an independent community plugin, not an official Obsidian product.

## Install the beta

The Obsidian Community directory listing is pending. Use either method below for the beta.

### BRAT

1. Install and enable [BRAT](https://github.com/TfTHacker/obsidian42-brat) from Obsidian's Community plugins.
2. In BRAT, choose **Add a beta plugin** and enter `https://github.com/shbhmrzd/rehearse-releases`.
3. Enable Rehearse, then run **Rehearse: Open practice** from the command palette.

BRAT is an optional beta installer. Rehearse itself works independently.

### Manual installation

1. Download [rehearse-0.5.0.zip](https://github.com/shbhmrzd/rehearse-releases/releases/download/0.5.0/rehearse-0.5.0.zip) from the [release page](https://github.com/shbhmrzd/rehearse-releases/releases/tag/0.5.0).
2. Put the extracted `rehearse` folder under `<your vault>/.obsidian/plugins/`. It must contain `main.js`, `manifest.json` and `styles.css`.
3. Reload Obsidian, enable Rehearse under **Settings → Community plugins**, and run **Rehearse: Open practice**.

Use your custom configuration folder instead of `.obsidian` if you have one. On updates, replace only the plugin assets; keep `data.json` and your cards.

Minimum Obsidian version: **1.9.14**. Persistent API-key storage requires **1.11.4 or later**; older hosts retain keys only for the current session. Native mobile behavior has not been verified.

## Try a session

Choose **Try the sample** to inspect five hand-written questions without configuring AI. Edit or deselect questions, choose **Practice selected**, answer before revealing, then compare with the checklist. Save cards only when you want to revisit them.

For your own note:

1. Open Rehearse's **Settings**, choose a provider and enter its API key or local server address.
2. Refresh models, select a text model or enter its ID, then **Save settings**.
3. Open a note and run **Rehearse: Practice this note**, or select a passage and run **Rehearse: Practice selected text**.
4. Describe what you want to understand, create questions, then review, edit and practice or save them.

**Saved connections** shows the provider, model, key-storage status and active connection. Switch without re-entering a stored key. A stored key does not guarantee model access or available API credit.

Named provider choices fill in the API URL. **Custom server…** supports OpenAI Chat Completions, Anthropic Messages and Gemini formats; use the server's own base URL and credentials. Compatibility describes the API format, not shared accounts or universal model support. Ollama and LM Studio are optional local choices; Rehearse does not install runtimes or download models.

## What you can do

- Generate recall, explanation and application questions from one note or passage.
- Exclude setup, build and dependency sections by default.
- Inspect source quotations, edit answers and checklists, and save selected drafts.
- Keep cards as ordinary Markdown files with stable identities.
- Use FSRS spaced review, four ratings and undo; free practice is always available.
- Export Markdown or an Anki-compatible TSV import file.
- Use multiple saved provider/server connections without another AI plugin.

AI suggestions need human review. Quote matching confirms that quoted words occur in the source; it does not prove the answer is accurate or useful. Sessions accept up to 24,000 characters and generate at most ten drafts. Repository exploration, automatic source-change repair, AI grading and two-way Anki sync are not implemented.

## Privacy and costs

Rehearse has no telemetry, advertising, payment service or hosted inference. Generation sends only selected source blocks and the learning goal directly to the provider you choose. Model discovery sends no note content. Cloud handling follows that provider's policies, and cloud generation may incur charges. Local generation requires a running local server; reviewing saved cards requires no model.

Source notes are not rewritten. Cards are stored in `Rehearse/cards/`, exports in `Rehearse/exports/`, and preferences/review history in Obsidian's plugin data. Keys use Obsidian secret storage where available and are excluded from ordinary settings, cards and exports. Your own vault sync/backup configuration can copy vault data. There is no conflict-aware merge for concurrent reviews across devices.

The directory's **Optional payment** classification applies because third-party AI services can charge, even though Rehearse itself has no paid features.

## Documentation and feedback

- [Connection setup and troubleshooting](docs/SETUP.md)
- [Practice, review, editing and exports](docs/USER_GUIDE.md)
- [Privacy and storage](docs/PRIVACY.md)
- [Beta walkthrough and feedback template](docs/BETA_FEEDBACK.md)
- [Report a problem](https://github.com/shbhmrzd/rehearse-releases/issues)

For a report, include Rehearse/Obsidian versions, your OS, provider/model and reproduction steps. Use a public or invented example; do not attach API keys, private notes or raw plugin data.

The [standalone demo](https://github.com/shbhmrzd/rehearse-releases/releases/download/0.5.0/Rehearse-demo.html) can be downloaded and opened in a browser to try the sample. Browser provider calls are subject to cross-origin restrictions; the Obsidian plugin uses its native request API.

## Verification and license

Version 0.5.0 passed 225 automated tests, build/lint/coverage checks and native Obsidian 1.14.5 workflow checks. Native testing covered Ollama generation, connection switching, key persistence, saved cards, reload, review/undo and exports. OpenAI discovery succeeded; generation was blocked by account quota. Other paid providers, native mobile and Anki import remain unverified. Checksums accompany each release.

MIT licensed. FSRS is provided by `ts-fsrs`; see [third-party notices](THIRD_PARTY_NOTICES.md).
