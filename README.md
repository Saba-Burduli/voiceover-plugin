<div align="center">

<img src=".claude-plugin/icon.png" alt="Voiceover Studio icon" width="112" height="112">

# Voiceover Studio

**Put your own voice in the demo videos Claude builds.**

Claude writes the script, a recorder shows you each line to read,<br>
and every scene of the video is timed to your takes.

[![Claude Code plugin](https://img.shields.io/badge/Claude_Code-plugin-D97757?logo=claude&logoColor=white)](https://docs.claude.com/en/docs/claude-code/plugins)
[![Release](https://img.shields.io/github/v/release/Saba-Burduli/voiceover-plugin?color=E0336E)](https://github.com/Saba-Burduli/voiceover-plugin/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
![macOS](https://img.shields.io/badge/macOS-supported-black?logo=apple)
![Runs locally](https://img.shields.io/badge/data-stays_on_your_Mac-2EA44F)

[Install](#install) · [How it works](#how-it-works) · [Recorder keys](#recorder-keys) · [FAQ](#faq) · [Watch the full demo](https://github.com/Saba-Burduli/voiceover-plugin/releases/download/v0.3.3/voiceover-studio-demo.mp4)

<br>

<img src="https://github.com/Saba-Burduli/voiceover-plugin/releases/download/v0.3.3/demo.gif" alt="A real Claude Code session: install the plugin, ask for a demo, record each line, get a video timed to your voice" width="820">

<sub>A real Claude Code session, sped up: install → ask for a demo → record → finished video.</sub>

</div>

---

## Why

Claude Code can build a demo video for your project, but the narration is usually a synthetic voice, or you record yourself and line up clips by hand. A demo in the maker's own voice feels different: viewers hear you, and the product sounds like yours.

Voiceover Studio closes that gap in one sentence:

> Make a demo video of this project. I want to voice it over.

You never write a script, run a command, or manage audio files.

## Install

Inside Claude Code:

```
/plugin install voiceover-studio --marketplace Saba-Burduli/voiceover-plugin
```

<details>
<summary>On Claude Code older than 2.1.275, install it in two steps</summary>

```
/plugin marketplace add Saba-Burduli/voiceover-plugin
/plugin install voiceover-studio@voiceover-plugin
```

</details>

> [!NOTE]
> Voiceover Studio is in review for Anthropic's official plugin directory. Until it's listed there, install it from GitHub as shown above.

**Requirements:** macOS · Claude Code (terminal, IDE extension or the desktop app's Code tab) · Node.js 20+ · [SoX](https://sox.sourceforge.net) for recording. If SoX is missing, Claude notices and offers to install it with `brew install sox`.

## How it works

<table>
<tr>
<td width="33%" valign="top">

### 1 · Install & ask

One command adds the plugin. Ask for a demo you want to narrate, and Claude writes one short, easy-to-say line per scene.

<img src="https://github.com/Saba-Burduli/voiceover-plugin/releases/download/v0.3.3/step-install.gif" alt="Installing the plugin from its marketplace in Claude Code">

</td>
<td width="33%" valign="top">

### 2 · Talk

A recorder opens with the line to say, what's on screen, and the next line. Record, hear it back, keep it or redo it.

<img src="https://github.com/Saba-Burduli/voiceover-plugin/releases/download/v0.3.3/step-record.gif" alt="The recorder showing a line to read while recording">

</td>
<td width="33%" valign="top">

### 3 · Done

Say **done** in Claude. It reads every take and builds the video so each scene lasts exactly as long as you spoke.

<img src="https://github.com/Saba-Burduli/voiceover-plugin/releases/download/v0.3.3/step-video.gif" alt="Claude builds the video and it plays back">

</td>
</tr>
</table>

You can also start it with the slash command:

```
/voiceover-studio:voiceover <what the demo should show>
```

## The recorder

A Terminal window opens on your first line:

```
  Onboarding demo  line 1 of 5
  ────────────────────────────────────────

  Say:

    Here's how a new team gets set up in under a minute.

    On screen: landing page, cursor on Sign up

  ────────────────────────────────────────

  Read the line above when you're ready.

  Enter start recording  ·  s skip  ·  q quit

  Next: First, invite your teammates by email.
```

### Recorder keys

| Key | What it does |
| --- | --- |
| <kbd>Enter</kbd> | Start recording, then stop. After playback: keep the take |
| <kbd>R</kbd> | Redo the take |
| <kbd>P</kbd> | Play the take again |
| <kbd>S</kbd> | Skip this line for now |
| <kbd>Q</kbd> | Quit. Progress is saved, and the recorder picks up where you left off |

The keys also work on Georgian and Russian keyboard layouts. If macOS asks whether Terminal can use the microphone, click **Allow**.

## Features

- **Lines written for speaking.** Short, plain sentences, each with a cue for what's on screen.
- **Instant playback.** Every take plays back right away, so you redo only what you don't like.
- **Scenes timed to your voice.** Each scene lasts as long as its take, plus a short pause. No splitting, no in/out marks.
- **Change one line, record one line.** Reword a line later and only that line goes back to the recorder.
- **Resumable.** Progress is saved after every take.
- **Works with Remotion.** Claude uses [Remotion](https://www.remotion.dev) when your project has it, and ffmpeg otherwise.
- **Private by design.** No network, no account, no API keys, no telemetry.

## FAQ

<details>
<summary><b>How is each scene timed to my voice?</b></summary>

Every line is its own take, so there's nothing to split or mark by hand. Claude reads each take's length and makes that scene last the same time plus 0.3 to 0.6 seconds of breathing room. Each line's audio sits inside its own scene.

</details>

<details>
<summary><b>What if I change a line later?</b></summary>

Ask Claude to reword it. Only the changed line goes back to the recorder; every other take stays as it is. If the new take is longer, only that scene gets longer, and the scenes after it start a little later with their audio still in sync.

</details>

<details>
<summary><b>What does Claude use to build the video?</b></summary>

[Remotion](https://www.remotion.dev) if it's available in your project, with one audio clip per scene. Otherwise it renders the scenes and adds the audio with ffmpeg.

</details>

<details>
<summary><b>Does anything leave my machine?</b></summary>

No. Recordings, scripts and progress stay in a `.voiceover/` folder in your project. The plugin makes no network calls. See the [privacy policy](PRIVACY.md).

</details>

<details>
<summary><b>Does it work on Windows or Linux?</b></summary>

It's built and tested on macOS. On Linux, the recorder doesn't open by itself, but Claude gives you the command to run it with SoX installed. Windows isn't supported yet.

</details>

## Under the hood

| Part | What it does |
| --- | --- |
| **MCP server** | `start_voiceover` saves the lines and opens the recorder window. `get_voiceover_status` returns each kept take's WAV path and duration. |
| **Skill** `voiceover-demo` | Teaches Claude the workflow: plan scenes, write speakable lines, open the recorder, time each scene to its take. |
| **Command** `/voiceover-studio:voiceover` | Runs the same workflow on demand. |

Files are saved in `.voiceover/` in your project:

```
.voiceover/
├── <line-id>.wav      one file per line
├── voiceover.wav      all lines merged into one track
├── manifest.json      progress and durations
└── takes/             every take, including redos
```

### What it does on your machine

- **Microphone:** records only between your two Enter presses, using SoX's `rec`.
- **Terminal:** `start_voiceover` opens one Terminal window with `osascript` to run the recorder, and reuses it if one is already open.
- **Files:** reads and writes only the `.voiceover/` folder in your project. Takes play back with `afplay`.
- **Network:** none. No audio, text or usage data is sent anywhere, and nothing is downloaded.

<details>
<summary><b>Standalone CLI</b></summary>

The plugin runs `dist/voiceover.mjs`, which also works on its own:

```bash
node dist/voiceover.mjs record [--dir .voiceover] [--gap 0.4] [--redo <lineId>]
```
```bash
node dist/voiceover.mjs status
```
```bash
node dist/voiceover.mjs doctor
```

</details>

<details>
<summary><b>Development</b></summary>

```bash
npm install
```
```bash
npm run typecheck && npm run build
```

`dist/voiceover.mjs` is committed, because plugin installs don't run `npm install`. Rebuild and commit it with every source change.

</details>

## Feedback

Questions, bugs and ideas are welcome in [GitHub Issues](https://github.com/Saba-Burduli/voiceover-plugin/issues). If Voiceover Studio helped you ship a demo, a ⭐ helps others find it.

<div align="center">

Made by [Saba Burduli](https://github.com/Saba-Burduli) · [MIT License](LICENSE) · [Privacy](PRIVACY.md)

<sub>Claude and Claude Code are trademarks of Anthropic. This is an independent, community-built plugin.</sub>

</div>
