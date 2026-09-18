# CapCut Desktop MCP Server 🎬

[![CI](https://github.com/capcut-mcp/capcut-mcp/actions/workflows/ci.yml/badge.svg)](https://github.com/capcut-mcp/capcut-mcp/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)](https://nodejs.org/)
[![Model Context Protocol](https://img.shields.io/badge/MCP-1.6.1-blue)](https://modelcontextprotocol.io/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-blue)](https://www.typescriptlang.org/)

An enterprise-grade **Model Context Protocol (MCP)** server that enables AI agents (Claude Desktop, Cursor, Google Antigravity, Cline, Windsurf) to programmatically edit videos in **CapCut Desktop** and **JianYing Pro (剪映)**.

CapCut MCP bypasses brittle GUI macros and mouse automation by directly constructing CapCut's native `draft_content.json` Abstract Syntax Tree (AST). Edits apply instantaneously, deterministically, and with zero window focus or keyboard hijacking.

---

## ✨ Features

- **24 Atomic Video Editing Tools**: Complete control over projects, multi-track timelines, transformations, speed scaling, audio fades, subtitles, and keyframes.
- **Native Desktop Integration**: Automatically detects and edits projects in **CapCut Global** and **JianYing Pro** across Windows and macOS.
- **Multi-Track Orchestration**: Base A-roll, overlay B-roll layers, audio ducking, sound effects, and text caption tracks.
- **Viral Typography Engine**: Built-in support for high-retention short-form styles (Style 6 Glow Pop, Style 7 Hero Typography, -1.0 tracking, drop shadows, and scale pop animations).
- **Mathematical Keyframing & Easing**: Quad Ease Out, smooth scale zooms, opacity transitions, and position pans.
- **Headless Proxy Previews**: Generate fast proxy preview MP4s using FFmpeg without opening the CapCut GUI.
- **Agent Skills Included**: Production-tested agent skills and prompt playbooks in `skills/capcut/`.

---

## 🚀 Quick Start

### 1. Global Installation (Recommended)

```bash
# Run directly with npx
npx capcut-mcp-server

# Or install globally
npm install -g capcut-mcp-server
```

### 2. Run from Source

```bash
git clone https://github.com/capcut-mcp/capcut-mcp.git
cd capcut-mcp
npm install
npm run build
npm test
npm start
```

---

## 🔌 Client Configuration

### Claude Desktop

Add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "capcut": {
      "command": "npx",
      "args": ["-y", "capcut-mcp-server"]
    }
  }
}
```

*File location:*
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`

---

### Google Antigravity

Add to your `mcp_config.json`:

```json
{
  "mcpServers": {
    "capcut": {
      "command": "node",
      "args": ["<PATH_TO_CAPCUT_MCP>/dist/src/index.js"]
    }
  }
}
```

---

### Cursor / Windsurf

Add to your `.cursor/mcp.json` or global MCP settings:

```json
{
  "mcpServers": {
    "capcut": {
      "command": "npx",
      "args": ["-y", "capcut-mcp-server"]
    }
  }
}
```

---

## 🛠️ MCP Tools Reference (24 Tools)

| Tool Name | Category | Description | Key Parameters |
|:---|:---|:---|:---|
| `capcut_list_projects` | Projects | List all local CapCut projects with metadata | *None* |
| `capcut_get_project` | Projects | Fetch timeline tracks, materials, and duration | `project_name_or_id` |
| `capcut_create_project` | Projects | Create a new project draft | `project_name`, `width`, `height` |
| `capcut_duplicate_project` | Projects | Clone an existing draft | `source_project_name_or_id`, `new_project_name` |
| `capcut_delete_project` | Projects | Delete a project folder | `project_name_or_id` |
| `capcut_open_app` | Projects | Launch CapCut Desktop with a specific draft | `project_name_or_id` |
| `capcut_add_video_clip` | Timeline | Append or insert a video clip on any track | `project_name_or_id`, `file_path`, `track_index`, `start_time` |
| `capcut_add_audio_clip` | Audio | Add music or voiceover with volume control | `project_name_or_id`, `file_path`, `track_index`, `volume` |
| `capcut_add_sound_effect` | Audio | Insert SFX (whoosh, pop, riser) at timestamp | `project_name_or_id`, `file_path`, `start_time` |
| `capcut_add_audio_fade` | Audio | Apply fade-in and fade-out curves | `project_name_or_id`, `track_index`, `clip_index`, `fade_in`, `fade_out` |
| `capcut_trim_clip` | Editing | Adjust in/out source points and target duration | `project_name_or_id`, `track_index`, `clip_index`, `source_start`, `source_duration` |
| `capcut_split_clip` | Editing | Split a clip at a specific timeline timestamp | `project_name_or_id`, `track_index`, `clip_index`, `split_timestamp` |
| `capcut_remove_clip` | Editing | Remove a clip from a track | `project_name_or_id`, `track_index`, `clip_index` |
| `capcut_set_clip_transform` | Transform | Adjust position `(x, y)`, scale, and rotation | `project_name_or_id`, `track_index`, `clip_index`, `x`, `y`, `scale`, `rotation` |
| `capcut_set_clip_speed` | Transform | Modify speed multiplier (0.1x to 100x) | `project_name_or_id`, `track_index`, `clip_index`, `speed`, `change_pitch` |
| `capcut_add_keyframe` | Animation | Animate scale, position, or opacity | `project_name_or_id`, `track_index`, `clip_index`, `property`, `time_offset`, `value` |
| `capcut_add_transition` | Transitions | Insert video transitions (dissolve, push, zoom) | `project_name_or_id`, `track_index`, `clip_index`, `transition_type`, `duration` |
| `capcut_add_text` | Text | Add static text or lower thirds | `project_name_or_id`, `text`, `start_time`, `duration`, `font_size`, `color` |
| `capcut_add_subtitles` | Text | Parse and import full SRT subtitle file | `project_name_or_id`, `srt_content`, `font_size`, `color` |
| `capcut_add_viral_caption` | Text | Add dynamic animated caption with styles | `project_name_or_id`, `text`, `style_preset`, `highlight_word` |
| `capcut_add_sticker` | Graphics | Place sticker or graphic overlay | `project_name_or_id`, `sticker_id`, `start_time`, `duration` |
| `capcut_create_video_bridge` | Sequencing | Generate cross-scene sequence with audio ducking | `project_name_or_id`, `primary_clip`, `secondary_clip`, `bridge_transition` |
| `capcut_get_media_info` | Utilities | Probe media duration, dimensions, codecs | `file_path` |
| `capcut_generate_preview` | Utilities | Render headless proxy MP4 preview | `project_name_or_id`, `output_path`, `resolution` |

---

## 🧠 Using with AI Agents (Skill Integration)

This repository includes an Agent Skill located at `skills/capcut/SKILL.md`.

To equip your AI assistant with the editing playbook:
1. **Antigravity / Gemini CLI**: Copy the `skills/capcut` directory into your project's `.agents/skills/` directory.
2. **Claude Desktop / Cursor**: Reference `skills/capcut/SKILL.md` in your project prompt or `.cursorrules`.

The skill provides guidelines on:
- Walter Murch's Rule of Six editing principles.
- Microsecond timeline arithmetic and track collision prevention.
- High-retention short-form typography (Styles 6 and 7).
- Quad Easing curves for kinetic punch-in zooms.

---

## 📐 Architecture

```
User Prompt -> AI Agent (Claude/Cursor/Antigravity)
                     │
                     ▼ (Model Context Protocol JSON-RPC)
             capcut-mcp-server
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
Paths Resolver   Media Probe   Draft Manager
(CapCut/JianYing) (FFprobe)          │
                                     ▼
                               Draft Builder
                               (Direct AST)
                                     │
                                     ▼
                      CapCut Desktop Draft Storage
                      (%LOCALAPPDATA%/CapCut/...)
                                     │
                                     ▼
                           Native CapCut Project
```

1. **Deterministic AST Generation**: Instead of automating the GUI, the server reads and writes CapCut's internal `draft_content.json` structure.
2. **Safe Atomic Writes**: Modifications create valid draft trees with all required material references, tracks, and segment IDs.
3. **Cross-Platform**: Dynamically resolves default project directories on Windows and macOS for both international CapCut and Chinese JianYing Pro.

---

## 🧪 Testing

The repository features an automated test suite verifying timeline generation, track collisions, transformations, speed scaling, and SRT subtitle ingestion:

```bash
npm test
```

All 21 tests execute against synthetic audio/video clips generated on-the-fly in an isolated temporary directory.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for details.
