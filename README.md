# VoxPrompt

macOS app that turns messy voice input into clean, structured AI agent prompts — pasted directly into whatever field is focused.

Speak naturally in any language. Get a prompt optimized for Cursor, Claude Code, Copilot, OpenCode, or any AI agent.

## How it works

1. Press a global hotkey to start recording
2. Speak your thoughts — in French, English, Spanish, whatever — including false starts, "wait no", "forget that part"
3. VoxPrompt transcribes, strips verbal noise, understands what you *meant* vs what you said, translates to your target language (default: English), and restructures it as a clear, actionable prompt
4. The cleaned prompt is pasted directly into whatever input field is active — browser, IDE, native app, anywhere

## What makes it different from Wispr Flow

Wispr Flow is a general-purpose voice dictation tool — it polishes speech for writing. VoxPrompt is purpose-built for **prompting AI agents**:

- **Prompt-aware restructuring** — output is formatted as clear instructions (context, task, constraints), not just clean prose
- **Smart delimitation** — understands vocal corrections ("no wait, not that", "forget the first part", "actually what I mean is") and acts on them instead of just transcribing them
- **Translation + prompt optimization in one pass** — speak in French, get an English prompt that reads like you wrote it for an agent
- **BYOK — OpenAI Responses API compatible** — works with OpenAI, Anthropic, OpenRouter, Ollama, LM Studio, or any provider that implements the Responses API. Fully local possible

## Features (planned)

- [ ] Global hotkey recording on macOS
- [ ] Whisper-based transcription (local or cloud)
- [ ] OpenAI Responses API client (compatible with OpenAI, Anthropic, OpenRouter, Ollama, LM Studio, etc.)
- [ ] Configurable target language (default: English)
- [ ] Custom system prompt for output style
- [ ] Paste into any active input field (AXUIElement / CGEvent)
- [ ] Menu bar app with quick settings
- [ ] Provider presets: OpenAI, Anthropic, Google Gemini, OpenRouter, Ollama, LM Studio, Mistral (+ custom)

## Recommended models

### Cloud

| Provider | Model | Why |
|----------|-------|-----|
| OpenAI | `gpt-4o-mini` | Fast, cheap, great at instruction following |
| Anthropic | `claude-sonnet-4-20250514` | Excellent reasoning and restructuring |
| Google | `gemini-2.5-flash` | Fast, strong multilingual |
| Mistral | `mistral-small-latest` | Good multilingual, European focus |
| OpenRouter | Any of the above, or local models via proxy |

### Local (Ollama / LM Studio)

| Model | Size | Why |
|-------|------|-----|
| `qwen3:8b` | ~5 GB | Best multilingual small model — handles French → English well |
| `llama3.1:8b` | ~5 GB | Strong general-purpose, good instruction following |
| `mistral:7b` | ~4 GB | Lightweight, fast inference on any Mac |
| `deepseek-r1:8b` | ~5 GB | Good reasoning for complex prompt restructuring |
| `phi4:14b` | ~9 GB | Excellent quality/size ratio if you have 16 GB+ RAM |

> 💡 For local transcription, pair with Whisper (`ollama run whisper` or LM Studio). For prompt refactoring, a 7–8B model is plenty — latency matters more than raw capability here.

## Stack

- **SwiftUI** + AppKit
- **AVAudioEngine** for mic capture
- **SFSpeechRecognizer** or **Whisper** for transcription
- **OpenAI Responses API client** for prompt refactor + translation (works with any compatible provider)
- **Accessibility / CGEvent APIs** for global hotkey and paste injection

## Setup (dev, eventually)

```bash
git clone https://github.com/Rook-ai-bot/voxprompt.git
cd voxprompt
open VoxPrompt.xcodeproj
```

Requires macOS 14+ and Xcode 16+.

## License

MIT
