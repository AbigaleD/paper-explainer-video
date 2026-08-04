# Paper Explainer Video (Skill for Claude Code)

Turn a research paper into a short **popular-science explainer video** — automatically.

```
paper PDF  →  Manim per-scene animation (1080p60)
           +  edge-tts voiceover (Chinese or English), lip-synced to the visuals
           +  synthesized royalty-free ambient BGM
           +  a Live2D anime host in the corner whose mouth moves with the narration
           +  auto transitions, intro title card, end-card with references
```

This repository is a [Claude Code skill](https://support.claude.com/en/articles/12512198-creating-custom-skills) that drives the whole pipeline. You only rewrite 3 small files per paper; the generic rendering scripts are included.

## Demo

The 1m53s promo below was produced **end-to-end by this skill itself** — paper-style 7-scene structure, Manim animation, edge-tts voiceover, synthesized BGM, and the Live2D host `llny` composited in the corner:

![Paper Explainer demo](demo/demo.gif)

▶ **[Watch the full 1080p60 video](demo/promo.mp4)** (7 MB, h264+aac)

## Two skills

| Skill | Language | Description |
|---|---|---|
| `skills/paper-explainer-video` | 中文 | 把一篇论文做成 3–5 分钟中文科普短视频 |
| `skills/paper-explainer-video-en` | English | Turn a paper into a 3–5 minute English explainer video |

Each is self-contained with a `SKILL.md`, the generic `assets/` scripts, and a fully worked **"model collapse"** example under `reference/`.

## Requirements

- **macOS** (uses the built-in PingFang SC / Helvetica Neue fonts)
- `ffmpeg` + `ffprobe` (`brew install ffmpeg`)
- Python 3.10+; the one-time setup (`bash ./assets/setup.sh`) creates a local venv with manim / edge-tts / live2d-py / etc. and fetches the free Live2D sample models (llny / Mao / Haru)

> This pipeline is intentionally macOS-first. It was built and measured on an Apple Silicon Mac; other platforms aren't covered yet.

## Install

**Option A — Claude Code plugin marketplace (recommended):**

```
/plugin marketplace add AbigaleD/paper-explainer-video
```

then browse / install the `paper-explainer-video` plugin.

**Option B — copy into your skills directory:**

```bash
git clone https://github.com/AbigaleD/paper-explainer-video
cp -R paper-explainer-video/skills/paper-explainer-video* ~/.claude/skills/
```

**Option C — install via [skills.sh](https://skills.sh) registry:**

```bash
npx skillsadd AbigaleD/paper-explainer-video
```

## Usage

Once installed, just say it in Claude Code:

- *"把这篇论文做成科普视频"* → `paper-explainer-video` (中文)
- *"make an English explainer video of this paper"* → `paper-explainer-video-en`

Claude reads the paper, designs 5–8 scenes (intro hook → core intuitions → conclusion → references), writes the narration + scene list, renders with Manim, mints the voiceover + BGM, composites the Live2D host, and frame-checks the result.

Typical end-to-end time for a paper of similar difficulty: **~22–28 min** (publish tier) or **~10–15 min** (fast preview tier).

## Repository layout

```
├── demo/                          # self-made demo (animated gif + full mp4)
├── skills/
│   ├── paper-explainer-video/     # Chinese pipeline skill
│   │   ├── SKILL.md               # instructions Claude follows
│   │   ├── assets/                # generic scripts (setup, TTS, BGM, render, mux, Live2D)
│   │   └── reference/             # worked "model collapse" example
│   └── paper-explainer-video-en/  # English pipeline skill
├── .claude-plugin/marketplace.json  # for /plugin install
└── LICENSE                        # MIT
```

## License

MIT © 2026 Zixin Dong. Each skill folder also carries its own `LICENSE.txt` so it stays self-contained if copied out.
