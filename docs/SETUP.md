# Setup and troubleshooting

Rehearse is independent: install only Rehearse. All AI configuration is in its own **Settings** screen. Sample practice, manual cards and saved-card review need no AI setup.

## Saved connections

**Settings → Saved connections** lists each saved provider/server address and its last selected model. **In use** identifies the active connection. Choose **Use connection** to switch immediately, or **Edit connection** to load the active connection into the form. Configure another provider below and **Save settings** to add it. Saving the same provider/address again updates that entry rather than creating a duplicate.

- **Key saved in Obsidian:** a key is stored for this connection. The password field stays blank.
- **Key available this session:** this host keeps keys in memory; they must be entered again after reload.
- **Key needed:** no key is stored for a provider that requires one.
- **No key required / No key saved (optional):** local or custom connections may not need authentication; follow your server's requirements.
- **Key entered — save settings to store it:** the field has an unsaved value.

These labels describe stored credentials, not a promise of successful authentication, model access or available API credits. **Forget saved key** clears that connection's credential; its saved details remain and show the updated status. Keys are not included in the connection list's persisted metadata or card exports. The existing configured connection is imported on upgrade.

## Cloud provider

1. Choose a preset in **Provider**: **Claude (Anthropic)**, **OpenAI**, **Google Gemini**, **OpenRouter**, **Groq**, **DeepSeek**, **Mistral**, **Grok (xAI)**, **Together AI**, **Fireworks AI**, or **Cerebras**.
2. Paste that provider's API key into **API key**. The standard API URL is shown automatically.
3. Click **Refresh models**, choose a text-generation model, and **Save settings**. Alternatively, enter the exact **Model ID** manually. The model list can include non-chat models and may be paginated by the provider; manual entry stays available.
4. Open a note → **Rehearse: Practice this note** → **Create practice**. Inspect and edit the draft questions before saving.

Provider accounts and usage charges belong to you. Model discovery checks the models endpoint without sending notes; it does not prove that a particular model can generate successfully. No automatic retries, fallback providers, indexing, or background generation are used. For Claude, choose **Claude (Anthropic)** and use an Anthropic API key scoped to your workspace; custom workspace-header configuration is not currently exposed.

## Local model

Open your existing Ollama or LM Studio server. Rehearse does not install runtimes or download models.

| Provider          | Default base URL           | Next step                                                         |
| ----------------- | -------------------------- | ----------------------------------------------------------------- |
| Ollama (local)    | `http://127.0.0.1:11434`   | Find downloaded models, select one, save                          |
| LM Studio (local) | `http://127.0.0.1:1234/v1` | Start the local server, refresh models, select a text model, save |

Ollama's direct mode accepts only loopback URLs and downloaded local models; recognized cloud models are excluded. For offline operation, configure the runtime appropriately, including disabling its cloud features. LM Studio local mode also requires a loopback address; the runtime's own upstream/cloud behavior is outside Rehearse's control.

## Custom endpoint

Choose **Custom server…** in **Provider**, then select the **API format** that your server supports. Enter its **Server URL** and its own API key, if required. Named providers such as OpenAI and Claude fill in their official URLs automatically and do not expose these advanced controls.

“Compatible” means the server accepts that request and response format. It does not mean the service is operated by OpenAI, Anthropic or Google, or that their API keys work on the custom server. The server URL is the base address supplied by that service's API documentation, including a required `/v1` or `/v1beta` prefix. There is no universal custom-server URL.

| API format                    | Generation path appended to base URL | API key header                       |
| ----------------------------- | ------------------------------------ | ------------------------------------ |
| OpenAI Chat Completions        | `/chat/completions`                  | `Authorization: Bearer …`            |
| Anthropic Messages            | `/messages`                          | `x-api-key` plus `anthropic-version` |
| Google Gemini                 | `/models/<model>:generateContent`    | `x-goog-api-key`                     |

Enter the base URL including any required prefix (`/v1`, `/v1beta`, etc.), an optional API key, and a model ID. **Refresh models** uses `/models`; manual model entry stays available when a server does not expose a catalogue. Model discovery supports both wrapped and bare-array compatible catalogues. There is no fixed model allowlist or automatic fallback between API formats.

Remote addresses require HTTPS; HTTP is accepted only on loopback. URLs must not contain credentials, query strings or fragments. API keys remain isolated by provider choice and complete base URL, including when two formats use the same server. Arbitrary custom headers, OAuth, AWS Bedrock signing, Azure-specific routes, and Responses-only APIs are not implemented. An unlisted service must match one of the supported API formats; generic does not mean every proprietary API works automatically.

## Keys and upgrades

On Obsidian 1.11.4+, Rehearse uses built-in secret storage. It does not require another plugin. Older Obsidian versions and the browser demo keep keys for the current Rehearse session only; the setup screen explains which mode is active. Leave the key blank to keep the saved key for that connection, enter a new value to replace it, or choose **Forget saved key** to clear it. Changing provider/address does not reuse another connection's key. Obsidian secret storage is host-managed and accessible to other plugins; it is not a private Rehearse encryption service.

Existing Claude/Anthropic and local settings keep their provider IDs, model/address and scoped key references. Version 0.2 shared-provider users must choose a direct provider and enter their own key; Rehearse neither reads nor changes AI Providers settings. It can be disabled or absent without affecting Rehearse.

## Connection problems

- **HTTP 401/403:** check the key and account/model permissions.
- **HTTP 429:** check provider usage limits or try later. Rehearse does not retry automatically.
- **API credits or quota exhausted:** the provider reported exhausted credit/quota rather than an invalid key. Check that provider's API billing and limits; refreshing the model catalogue can succeed even when generation is unavailable.
- **Secret ID is invalid:** upgrade to Rehearse 0.4.1 or later. Earlier versions could exceed Obsidian's secret-ID length limit. This error concerns the plugin's storage identifier, not the API key's validity.
- **Could not reach / timed out:** check the server, URL, network, or model size. Generation has a two-minute deadline; model discovery has a ten-second deadline.
- **Model list unavailable:** enter the model ID manually. For local Ollama, the model must still be downloaded.
- **No text answer / response cut short:** select a supported text model or request fewer questions.
- **Browser-only failure:** browser CORS may block a provider. Try the real Obsidian plugin, which uses the native request API. Do not disable browser security.

## Other common problems

| Message / symptom                            | What to do                                                                                                                                                      |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Could not connect                            | Open Ollama or run `ollama serve`. Check the endpoint. The plugin supports Ollama's API, not an arbitrary local chat server.                                    |
| No local models found                        | Download a local model in Ollama, then refresh. Cloud models are excluded.                                                                                      |
| Selected model no longer installed           | Refresh the downloaded-model list, choose an installed model, and save settings.                                                                                |
| HTTP 500                                     | Check the Ollama app/logs for a model-load or memory error. Try a smaller model or passage. The plugin does not alter your machine's runtime settings.          |
| Model took too long                          | Use a shorter passage or smaller model. The generation deadline is two minutes.                                                                                 |
| Invalid card data / no valid source evidence | Try a clearer passage or a model that follows structured-output instructions better. Rehearse does not save unsupported suggestions.                            |
| No learning material found                   | Select more prose, or enable operational sections if the subject you want to learn is setup/build/dependencies.                                                 |
| Note too long                                | Select the section you want to study. Rehearse rejects oversized input rather than silently omitting the end.                                                   |
| Card file needs attention                    | Open the named Markdown file. Restore its metadata comment and required headings, or restore the file from your backup. The file is not deleted or overwritten. |
| Review data could not be read                | Preserve the plugin data file, then restore a known-good backup. Do not delete it merely to dismiss the warning; it contains your review history.               |
| Some cards saved before an error             | Check disk space or vault permissions, then retry. Exact duplicates are skipped.                                                                                |
| Source moved or changed                      | Use the saved quotation as a reference and locate the current source manually. Automatic source migration is not implemented.                                   |

## Desktop, mobile, and sync

Direct Ollama mode needs Ollama on the same device. Running it on a laptop does not make it available at `localhost` on a phone. Cloud and compatible endpoints connect directly from the device. Native mobile generation has not been validated; saved-card review needs no model.

Rehearse uses Web and Obsidian APIs, without Node/Electron runtime imports. Native mobile validation remains a separate release check. The browser demo's narrow layout is not a substitute for testing the real mobile app.

Cards are in the vault. Review history is in Obsidian's plugin data file, so syncing only Markdown does not necessarily sync scheduling. Configure your existing sync provider accordingly. Review on one device at a time, let it finish syncing, and keep backups. Rehearse does not merge concurrent changes from multiple devices.

## Report a problem

Open a GitHub issue in this repository with the plugin and Obsidian versions, OS, model name, steps, and exact error text. Use a short non-sensitive reproduction note. Do not include your full vault, private notes, credentials, or the raw plugin data file.
