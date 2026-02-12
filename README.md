# Claude Search — Firefox Extension

Prompt Claude directly from your Firefox address bar using **`@claude`**, just like `@youtube` or `@google`.

---

## Installation

1. Open Firefox → navigate to `about:debugging#/runtime/this-firefox`
2. Click **"Load Temporary Add-on..."**
3. Select `manifest.json` from the unzipped folder

> **Permanent install:** Use Firefox Developer Edition or Nightly with
> `xpinstall.signatures.required` set to `false` in `about:config`.

---

## Usage

Type `@claude` in the address bar, press **Tab** (or space), then type your prompt:

```
@claude   what is quantum entanglement
```

Hit **Enter** — Firefox opens `claude.ai/new` and injects your prompt into the editor.

### Model Flags

Defaults to **Opus**. Add a flag anywhere in your prompt to switch:

| Flag               | Model         |
|--------------------|---------------|
| `-opus` or `-o`    | Claude Opus   |
| `-sonnet` or `-s`  | Claude Sonnet |
| `-haiku` or `-h`   | Claude Haiku  |

```
@claude   explain dark matter in simple terms -sonnet
@claude   translate hello to japanese -h
```

### Auto-Submit (Default: ON)

Prompts are **automatically submitted** by default. To review before sending, add `-wait`:

```
@claude   capital of france -haiku -wait
```

### Combined Example

```
@claude   write a bash script to batch rename files -s
```
→ Opens Claude Sonnet and auto-submits.

```
@claude   review my approach to X -wait
```
→ Opens Claude Opus, injects prompt, waits for you to review/edit before sending.

---

## How It Works

1. The extension registers **Claude** as a Firefox search engine with the `@claude` keyword
2. When you submit, Firefox navigates to `claude.ai/new?q=your+prompt+here`
3. A content script on `claude.ai` reads the `?q=` parameter, parses any flags, cleans the URL, and injects the prompt into the chat editor
4. If `-send` was used, it clicks the send button automatically

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `@claude` not appearing | After loading the extension, type `@claude` then Tab. Firefox may need a restart. |
| Prompt not injected | claude.ai may have updated their editor DOM. Open an issue. |
| Model not switching | Best-effort — depends on claude.ai's UI structure. Change manually if needed. |

---

## Files

```
claude-search/
├── manifest.json      # Extension manifest + search engine registration
├── content.js         # Prompt injector (runs on claude.ai)
├── icons/
│   ├── claude-16.png
│   ├── claude-32.png
│   ├── claude-48.png
│   ├── claude-64.png
│   └── claude-128.png
└── README.md
```

## License

MIT
