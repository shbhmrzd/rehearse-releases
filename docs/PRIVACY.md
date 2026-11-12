# Privacy and data storage

Rehearse v0.4 has no backend, account, payment integration, analytics, advertising, telemetry, or automatic model requests.

## Network

### Direct provider connections

Rehearse includes its own provider adapters. No community AI plugin, Rehearse backend or account is required.

Each explicit **Refresh models** action makes one GET request. Each **Create practice** action makes one POST request to a cloud or custom provider, or one model-list GET and one chat POST to local Ollama. Startup, sample practice, manual cards, saved-card review and exports make no provider requests. Retries require another user action.

- **Refresh models:** GETs the chosen provider's models endpoint with its authentication headers; no note text is sent.
- **Create practice:** sends selected source blocks, learning goal, schema and instructions directly to the configured provider. It does not send unrelated notes or index the vault.
- Cloud connections send inputs off-device. The provider's retention, billing and privacy terms apply. Local runtimes follow their own configuration.
- Keys are stored through Obsidian's built-in secret storage when available, otherwise in memory until Rehearse reloads. They are not stored in `data.json`, cards or exports. Other plugins can access Obsidian's shared secret store; no additional encryption boundary is claimed.
- Keys are scoped to provider and full base URL. Rehearse never copies another community plugin's keys or silently falls back to a different provider. Presets use fixed official base URLs; custom OpenAI-, Anthropic-, and Gemini-compatible servers require explicit configuration. No extra SDK, account system, or proxy is introduced by the added presets.
- Remote URLs require HTTPS. HTTP is allowed only for loopback. Authentication uses request headers, not query strings. Raw remote error bodies are not displayed or saved.
- Cancel and deadlines stop accepting results. Browser requests are signalled to abort; Obsidian's native request API can finish in the background. Neither cancellation nor timeout guarantees that provider billing or compute stops.

### Direct local Ollama (optional)

In direct mode, Rehearse connects only to the configured Ollama server at `localhost`, `127.0.0.1`, or `::1`. URLs with credentials, query strings, fragments, or non-root paths are rejected.

- **Find downloaded models:** GET `/api/tags`; no note text is sent.
- **Create practice:** checks `/api/tags`, then POSTs to `/api/chat` with the same bounded inputs described above.

The model is checked against the installed-model list before sending the note. Recognized cloud-backed entries are excluded. Configure and trust your local runtime, and disable its cloud features for offline use. These restrictions apply to direct Ollama mode; the other direct adapters support user-selected cloud providers.

Direct mode uses Obsidian's HTTP API. Cancel and timeout stop processing the result but may not stop an already-running request.

### No AI connection needed

Sample practice, manual cards, saved-card review, editing, and export make no model requests. Rehearse does not automatically generate questions when a note is opened.

## Files

| Data                                                                                                         | Location                                                        |
| ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- |
| Question, answer, checklist, stable ID, creation time, source path, quote, line range                        | `Rehearse/cards/<id>.md`                                        |
| Exported Markdown / Anki TSV                                                                                 | `Rehearse/exports/`                                             |
| Active and saved provider/endpoint/model details, session size, new-card limit, topic preference, FSRS schedules, rating events | Obsidian plugin data (`<configDir>/plugins/rehearse/data.json`) |
| Optional typed practice answer                                                                               | In memory only for the current question                         |
| Draft cards                                                                                                  | In memory until explicitly saved                                |

Quotations in saved cards can contain sensitive material. Your existing vault-sync provider and backups may copy them. Rehearse adds no encryption or separate sync system.

Review events contain card IDs, timestamps, self-ratings, and previous/next scheduling state. They do not include typed answers. These events support undo and counting new cards introduced on a local calendar day.

## Permissions and scope

The plugin reads the active note or selected passage when you start practice, and lists files only within its managed `Rehearse/cards/` folder for the library. It does not enumerate the vault, recursively index notes for AI, read outside the vault, install dependencies, fetch websites named in notes, execute code snippets, or interpret source instructions as commands.

Generated text is displayed as text, not inserted as executable HTML. Exact-quote validation does not eliminate model mistakes or prompt injection risks; every generated question remains a draft for your review.

## Deletion and uninstall

Use Obsidian's ordinary file management to remove card/export files. Uninstalling the plugin can remove its settings/history depending on Obsidian behavior; back up plugin data before uninstalling if you want to preserve scheduling. Card Markdown files are independent and remain in the vault unless you remove them yourself.

## Browser demo

The local browser demo uses localStorage under `rehearse-demo-v1-*`. It has no server-side storage. Clearing the site's storage removes demo cards and review history. Its downloaded exports are ordinary local files. The demo is a test/preview surface and does not provide vault synchronization. Its direct provider requests are subject to browser CORS and its API keys are kept in memory only.
