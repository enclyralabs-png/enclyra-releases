# Enclyra for macOS — 0.9.0 beta

**An AI that runs on your Mac, not in the cloud.** It talks with you, remembers you, and does real work on your
computer — files, PDFs, videos, pictures, reminders, the web — on a small local model that fits in 8 GB of RAM.
Your files and chats never leave your Mac.

**[⬇ Download Enclyra.dmg](https://github.com/enclyralabs-png/enclyra-releases/releases/latest/download/Enclyra.dmg)**

---

## How reliable is it? (honest numbers)

| Task | Result in our tests |
|---|---|
| **3–4 step tasks** ("find my PDFs from this week, merge them, zip the result") | **85–90% done right** |
| Long chains (6–7 steps) | most steps work, but the whole chain is fully right less often — **check the result** |
| More than ~10 actions in one request | refused on purpose: "too many actions at once" — split it up |

**How we tested:** an 8 GB Mac, lab conditions — our own test sets of hundreds of requests, run on test files and
folders. Real use is messier (your file names, your folders, your wording), so expect it to be lower at first.
Everything it does to files can be undone (see below).

---

## What it can do

Type normally to **chat**. Start a message with **`ACT>`** to make it **do** something:

```
ACT> find all screenshots on my desktop and move them to a folder called Shots
ACT> compress report.pdf and add page numbers
ACT> make clip.mp4 louder and turn it into a gif
ACT> remind me to call mom at 7 pm
```

- **Files & folders** — create, find, move, copy, rename, delete (to the Trash), zip / unzip, organize, find what fills your disk
- **Undo** — one button puts back what the last task did: moves, copies, renames, deletes, created files and folders
- **PDF** — merge, split, rotate, compress, page numbers, password, redact words, remove pages
- **Video & audio** — trim, speed, volume, fade, cut silence, even loudness, remove background noise, square / vertical, extract audio, video → gif, record the screen
- **Pictures** — resize, compress to a size, remove the background, convert formats, read text from a picture (OCR)
- **Convert** — between common file formats (mp4 → mp3, png → jpg, md → pdf…)
- **Web** — search, and download what it found
- **Your Mac** — calendar, reminders, notes, music, read mail, Wi-Fi, Bluetooth, volume, timers, keep awake, screenshots, Shortcuts
- **Writing** — drafts, summaries, translations, saved to a file if you ask
- **Memory** — it learns the people, places and things you talk about, on your Mac, and uses them in later chats

---

## What it can't do (yet)

- **No cloud, no big models.** It runs small models (3–4B) on your Mac. Chat answers are good, not GPT-level.
- **It never sends for you.** Email, messages and files are opened ready to send — you press send.
- **It doesn't click around websites** or fill in forms for you.
- **Big coding jobs** — writing a whole new project or large code changes are weak on 8 GB. Small edits work.
- **Memory can be wrong.** It picks facts out of your chats automatically; a new name or place is only kept once
  you've mentioned it twice. It treats what it remembers as "might be true".
- **Apple Silicon Macs only** (M1 and later). Tested on macOS 26. No Intel, no Windows build yet.
- **English works best.**

---

## Requirements

- Apple Silicon Mac, **8 GB RAM** or more
- **Ollama** (free, runs the models) — Enclyra helps you install it on first launch
- About **5 GB** of disk for the models, plus about **2–3 GB** for the optional speed-up cache

## Install

1. Download `Enclyra.dmg`, open it, drag **Enclyra** into **Applications**.
2. **First open — getting past macOS Gatekeeper.** Enclyra is not signed with a paid Apple developer certificate
   yet (that costs $99/year — it will come), so macOS blocks it the first time. You only do this once:

   **Way 1 — System Settings (macOS 15 Sequoia and later, also works on older):**
   1. Double-click Enclyra in Applications. macOS says it can't be opened → click **Done** (not "Move to Trash").
   2. Open **System Settings → Privacy & Security**, scroll down to **Security**.
   3. Next to *"Enclyra" was blocked to protect your Mac*, click **Open Anyway**, enter your Mac password.
   4. Click **Open** in the last box. From now on it opens normally.

   **Way 2 — if macOS says "Enclyra is damaged and can't be opened":** it isn't damaged — that is the download
   mark macOS puts on unsigned apps. Open **Terminal** and paste:
   ```
   xattr -dr com.apple.quarantine /Applications/Enclyra.app
   ```
   Then open Enclyra normally.

   On macOS 14 and older, **right-click Enclyra → Open → Open** also works.

   *Why trust it?* It only removes the block for this one app, nothing else on your Mac. If you'd rather not, wait
   for the signed version.
3. First launch downloads Ollama and the models (about 5.5 GB — see below). Keep the Mac online until it's done.
4. Enclyra may ask to build a **speed-up cache** (actions answer about 2× faster). It runs in the background for a
   few minutes; say No if your Mac is busy — you can build it later from the **!** at the top.

---

## First launch — the only time it needs the internet

Setup downloads everything Enclyra needs **once**. After that, it works with the Wi-Fi off.

| Step | What is downloaded | Size | From |
|---|---|---|---|
| 1. Ollama | the free app that runs AI models on your Mac (Enclyra opens the installer, you click through it) | ~200 MB | ollama.com |
| 2. The models | depends on your Mac's RAM — Enclyra picks the package for you (table below) | ~5 GB on 8 GB | ollama.com |
| 3. Meaning model | `all-mpnet-base-v2` — how it understands what you mean, for search and memory | ~420 MB | huggingface.co |

**The models — one package per RAM size:**

| Your Mac | Models it downloads |
|---|---|
| **8 GB** | `granite3.1-moe:3b` + `granite4:micro` (plan and do the actions), `gemma3:1b` (chat) — ~5 GB |
| **16 GB** | `granite3.1-moe:3b` + `granite4:tiny-h` (actions), `gemma3:1b` (chat) — bigger, smarter planner |
| **32 GB** | `granite3.1-moe:3b` + `granite4:small-h` (actions), `gemma3:1b` (chat) — the biggest planner |

You can switch packages or add models later in Settings; if one is missing, Enclyra falls back to one you have.

Only these files are downloaded — nothing about you is uploaded. If the internet drops during setup, just open
Enclyra again and it carries on.

**What "offline" means here:** the AI model runs on **your Mac's own chip**. Your chats, files, memory and
everything you ask it are worked out on your Mac and stay there. Nothing is sent to us — or anyone — unless you
allow it. The one thing Enclyra does on its own is **check for updates** when it starts (below), and you can turn
that off too.

---

## Privacy — exactly what goes online

Nothing you say or do is sent anywhere. The only times Enclyra uses the internet:

| When | What is sent | Turn it off |
|---|---|---|
| App launch | update check, with a **random install number** (not your name, email or IP) so we can count how many people use Enclyra | Settings → uncheck automatic update checks |
| You ask for a web search or download | the search words | don't ask for one |
| First launch, only if you choose it | your public IP to ip-api.com, to guess your city | choose "offline" or "skip" |
| You press **Report issue** | the report you see and approve before it's sent | don't press it |

We run no server that receives your chats, files or memory. We can't see what you do in the app.

---

## Feedback

Something went wrong, or something you want? Use **Report issue** in the app — it shows you exactly what will be
sent. This is a beta made by one person; every report gets read.

**Made by [Enclyra Labs](https://www.enclyralabs.com).**
