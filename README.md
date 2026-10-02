# pi Config

My configuration for the [pi coding agent](https://github.com/earendil-works/pi).

## Contents

- `models.json` — custom model registry. Overlay on top of pi's bundled catalog to expose local models.

## Setup

1. Install pi: `npm install -g @earendil-works/pi-coding-agent`
2. Copy `models.json` into the agent directory (replaces any existing file):

   ```sh
   cp models.json ~/.pi/agent/models.json
   ```

3. Start pi and select a model with `/model`. No credentials are needed for the models below; they speak a local OpenAI-compatible API.

## Models

### dgx-spark-sg-lang

| Field | Value |
|---|---|
| Base URL | `http://192.168.1.30:8888/v1` |
| API | `openai-completions` |
| API key | `none` (dummy; the local router ignores it) |

| Model ID | Context | Max tokens | Reasoning |
|---|---|---|---|
| `qwen3.8-27b-sglang` | 262144 | 120000 | Yes — sgl router thinking levels via `thinkingFormat: "chat-template"` (`enable_thinking` / `reasoning_effort` template kwargs, mapped from pi thinking levels) |
| `qwen3.6-35b-sglang` | 262144 | 120000 | No |

Both models serve from an sgl router on a DGX Spark at `192.168.1.30` (LAN only).

## Notes

- This file contains no secrets. Credentials for built-in providers live in `~/.pi/agent/auth.json` and are intentionally not published here.
- Pi reads the file on startup and re-reads it when you open `/model`, so edits apply without restarting the session.
