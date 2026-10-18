# Chrome Prompt API Demo (Gemini Nano)

A single-page demo of Chrome's built-in Prompt API: text and image prompts answered by Gemini Nano running locally in the browser, with streaming output.

![UI view](screenshots/ui.png)

## What it does

- Sends a text prompt, optionally with an image, to Chrome's on-device `LanguageModel` (Gemini Nano).
- Streams the model's answer into the page as it is generated.
- Runs entirely on your machine: after the model is downloaded there are no network calls and no API costs.

## Tech stack

- Plain HTML, CSS and JavaScript in one file (`index.html`), no build step and no dependencies
- [Chrome Prompt API](https://developer.chrome.com/docs/ai/prompt-api) (`LanguageModel.create`, `promptStreaming`) with multimodal (image) input

## Requirements

Hardware (from Chrome's requirements for Gemini Nano):

- Storage: 22 GB free disk space (the model itself is about 4 GB)
- GPU with 4 GB+ VRAM, or a CPU with 16 GB+ RAM and 4+ cores

Software:

- Chrome 138 or later
- Windows 10/11, macOS 13+, Linux, or ChromeOS

The Prompt API is still evolving and its surface has changed between Chrome versions. This demo targets the Chrome 138+ API shape (`LanguageModel` global, `expectedInputs`, message objects with `content` arrays).

## Getting started

### 1. Enable Chrome flags

1. Open `chrome://flags` in Chrome.
2. Enable both flags:
   - `chrome://flags#optimization-guide-on-device-model`
   - `chrome://flags#prompt-api-for-gemini-nano-multimodal-input`
3. Click **Relaunch**.

### 2. Open the page

Clone the repo and open `index.html` in Chrome:

```bash
git clone https://github.com/maksimkunaev/gemini-nano-local.git
cd gemini-nano-local
```

You can open the file directly, or serve the folder locally if you prefer, for example:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

### 3. Download the model

The model downloads automatically on first use:

1. Enter any prompt and click **Generate**.
2. Wait for the download to finish (about 4 GB; it can take 10 to 20 minutes).

To track progress, open `chrome://on-device-internals` and check the "Foundational Model" section. Once the model shows as ready, prompts run offline.

## Project structure

```
.
├── index.html        # The whole app: UI, styles and Prompt API calls
└── screenshots/
    └── ui.png        # Screenshot used in this README
```

## Known issues

- A new model session is created on every click of **Generate**, so there is no conversation memory between prompts.
- If the API is unavailable (flags off, unsupported Chrome, model not downloaded) the page shows the browser's error message.

## Further reading

- Chrome Prompt API documentation: https://developer.chrome.com/docs/ai/prompt-api

## License

MIT, see [LICENSE](LICENSE).
