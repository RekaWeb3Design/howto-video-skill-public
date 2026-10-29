---
name: howto-video
description: Makes a narrated step-by-step how-to / tutorial video (MP4) for any brand, web app or tool after a short Q&A about brand, purpose, audience, tone and voice. Rebuilds the UI with fictional data, voices it with ElevenLabs (or captions only) and renders it with Playwright + ffmpeg.
license: CC-BY-NC-SA-4.0
metadata:
  author: Víg Réka (Réka Víg)
  studio: The WOW Studio
  contact: hello@rekavig.com
  github: RekaWeb3Design
  version: 1.0.0
---

<!--
  How-to Video Skill
  Created by Víg Réka (Réka Víg) — The WOW Studio
  Copyright (c) 2026 Víg Réka / The WOW Studio
  Licensed under CC BY-NC-SA 4.0 — https://creativecommons.org/licenses/by-nc-sa/4.0/
  Non-commercial use only. Do not sell this skill or bundle it into paid products,
  courses or services, and do not charge anyone for videos made with it,
  without written permission from the author. Free videos for clients are fine.
  Keep this notice and the attribution when sharing or modifying.
  Commercial licensing: hello@rekavig.com
-->

# How-to video maker

*Created by Víg Réka — The WOW Studio. Free for non-commercial use under CC BY-NC-SA 4.0.*

Short, clear tutorial videos for any brand, client or team. Brand-agnostic by default; brand-specific setups live in **Profiles** at the end. Talk to the user in their language.

## Principles

- **Context first, then few questions.** Use what the current project/chat already tells you; ask only what is missing. Never ask what you can find out yourself (repo labels, brand files, recipients in an existing email thread).
- **Gates, in order:** (1) brief, (2) script, (3) finished video, (4) distribution (upload / embed / email, only what the brief asks for). Never skip a gate; one gate per message.
- **No credits before the script is approved.** Say up front that voiceover/generation uses credits.
- **Never send audio alone for review.** Always a finished video with sound.
- **Fictional data only.** No real names, amounts, order numbers or IDs. Use obviously fake ones (Jane Sample, Test Company Ltd., round amounts, `DEMO-2026-001` style IDs; in Hungarian e.g. Minta Anna, Példa Kft.).
- **Tone comes from the brief.** Default is calm and matter-of-fact; no hype or marketing tone unless the brief explicitly asks for it.

## Step 0 — Capability check (silent)

Check: Bash, `node`, `ffmpeg`, Playwright Chromium (install if missing: `npm i playwright && npx playwright install chromium`), an ElevenLabs connector (speech generation), a browser tool for uploads, an email tool for drafts. Offer only what works; say once what is missing. Without a voice tool the video is captions only (scene duration = max(2.5 s, characters ÷ 15) + 0.5 s). Click/whoosh SFX available on request.

## Step 1 — Context (silent)

Look through the current project/chat and memory for: brand name, colours, fonts, logo, design system, repo, earlier videos, recipients, a matching Profile, the user's preferred voice. Note what you found; show it as assumptions in the brief, don't ask it again.

## Step 2 — Questions (one round)

Ask only what Step 1 did not answer. Max 6 questions, multiple choice where possible (use a question tool if available, max 4 per call; otherwise plain text):

1. **Brand** — which brand is it for? Brand look (colours/fonts/logo from a file, site or design system) or neutral?
2. **Topic + scope** — which tool/feature, and exactly which task from start to finish? Full flow (default) or one short task (~40 s)?
3. **Audience + goal** — internal team / one named person / client / public; what should they be able to do afterwards?
4. **Tone + address** — calm-matter-of-fact (default) / friendly / formal; informal or formal address (e.g. tegező / magázó in Hungarian); one person or a group?
5. **Voice + language** — which voice (the user's own cloned voice, a stock voice, or captions only); which narration language?
6. **Format + destination** — 16:9 internal guide (default) / 9:16 social / embedded on a site or in an app; target length? If an email goes out: to whom, in which thread (if unclear, search the mailbox for the relevant thread and propose it)?

If relevant, also: **visual mode** (rebuilt UI with fictional data / screenshots / footage the user supplies) and **closing line** (who to contact with questions).

## Step 3 — Brief (gate 1)

Show one brief table, defaults filled in, and wait for approval:

| Setting | Default |
|---|---|
| Brand look | From project context; else neutral (white cards, system sans, one accent colour) |
| Voice | The voice from the brief or a Profile. Never assume a voice ID: list the available voices and say which one you use and with which model |
| Narration | Language from the brief; calm, matter-of-fact; address per brief |
| Captions | On, top of the frame (never over the highlighted UI) |
| Music / SFX | None (music only generated or user-supplied, ~−22 dB under speech) |
| Format | 16:9, 1280×720, 25 fps (9:16 = 720×1280, 1:1 = 1080×1080 on request) |
| Length | 60–100 s, full flow, about 6 steps |
| Visual mode | Rebuilt UI with fictional data for apps whose code is available; screenshot mode for third-party tools (e.g. Google Analytics, Shopify admin) |
| Delivery | MP4 (+ optional `.srt`); upload/embed/email only if the brief says so |

If a Profile matches, apply its overrides and say so.

## Step 4 — Source material

**Rebuilt UI (code available):** read the real page in the repo to copy exact labels, button texts, field order, toasts and states, e.g. `grep -nE "CardTitle|Label|label=|placeholder=|Button|toast\." src/pages/<Page>.tsx`. If the repo is not in the session, attach and clone it read-only. Never copy real data from a DB or files; delete real sample files from the workspace once you have the labels.

**Screenshot mode:** one screenshot per step, same width (1280–1440 px). Cover personal data before zooming. Do not submit forms or change settings to get a nicer screen.

**Brand look:** take colours/fonts/logo from the brand source the brief names. Only fonts loadable locally or from Google Fonts; if the brand font isn't available, pick the closest and say so.

## Step 5 — Script (gate 2)

Table: `# | on screen (shown / highlighted) | narration`.
- Shape: greeting + what we do → where to find it (menu path) → one step per scene → what the result means (statuses, totals) → what to download / what happens next → privacy line if relevant (e.g. "Your files never leave your computer") → closing line from the brief.
- Exact UI labels in quotes, in the UI's language.
- Pace ≈ 1.8 words/s in Hungarian, ≈ 2.4 words/s in English (estimate other languages similarly); check the total against the target length.
- Short spoken sentences; one action per scene; tone and address exactly as briefed.

Show the script, wait for approval; on edits show only the changed rows.

## Step 6 — Voiceover

- Generate the **whole approved narration in one call**, tone prefix matching the brief (default `[calm, friendly, matter-of-fact]`), with the tool's default number of takes. One call only; never re-call to retry.
- Download the takes as `voice_A.mp3` and `voice_B.mp3`. Use take A first. Don't send audio for review; mention that take B exists and that switching means re-timing (a few minutes).
- Timing: `ffmpeg -i voice_A.mp3 -af silencedetect=noise=-35dB:d=0.35 -f null -` to find paragraph boundaries; map each scene to its sentence. Only if ambiguous, transcribe with timestamps (costs credits; say so).

## Step 7 — Scene (`scene.html`)

One self-contained page at the briefed size. All motion is a **pure function of time**: `window.setT(t)` sets everything for second `t`. No CSS animations, transitions or timers.

House style:
- **Title card:** "<Tool/Module> – <what>" in the brand look; small "New" tag for a new feature.
- **UI** rebuilt in the app's own look (fonts, colours, card style), or the step's screenshot with zoom/pan.
- **Highlight** (outline + dimmed backdrop) on the active element, fading in ~0.3 s into the scene; brand accent colour, orange if none.
- **Files "dropping in"** to upload fields, **cursor** moving to buttons with a click ripple, values changing (e.g. a dropdown from May → June).
- **Captions** at the top (below the highlight only if it is at the top); max 2 lines.
- **Explainer mini-diagram** when a concept needs it.
- **Result screen**: statuses highlighted row by row as the voice mentions them (green / yellow / red).
- **End card:** privacy line if relevant + closing line + brand logo if available.
- Nothing overlaps unintentionally; all on-screen text must be correct and make sense in its language.

## Step 8 — Render

```js
// render.js — node render.js <duration_seconds> [width] [height]
// Part of the How-to Video Skill by Víg Réka / The WOW Studio (CC BY-NC-SA 4.0)
const {chromium} = require('playwright');
const fs = require('fs');
(async () => {
  const [fps, dur] = [25, Number(process.argv[2])];
  const [w, h] = [Number(process.argv[3] || 1280), Number(process.argv[4] || 720)];
  const b = await chromium.launch();
  const p = await b.newPage({viewport: {width: w, height: h}});
  await p.goto('file://' + __dirname + '/scene.html');
  await p.evaluate(() => document.fonts.ready);
  fs.mkdirSync(__dirname + '/frames', {recursive: true});
  for (let i = 0; i < Math.ceil(fps * dur); i++) {
    await p.evaluate((t) => window.setT(t), i / fps);
    await p.screenshot({path: `${__dirname}/frames/f${String(i).padStart(5, '0')}.jpg`, type: 'jpeg', quality: 92});
  }
  await b.close();
})();
```
Run with a long timeout (up to 10 min). Before the full render, use a `shots.js` variant that renders only a handful of keyframe times, to check layout cheaply.

```bash
ffmpeg -hide_banner -loglevel error -y -framerate 25 -i frames/f%05d.jpg -i voice_A.mp3 \
  -c:v libx264 -pix_fmt yuv420p -crf 20 -preset veryfast \
  -c:a aac -b:a 160k -af apad -shortest -movflags +faststart <Brand>_<Feature>_howto.mp4
```
File name: `<Brand>_<Feature>_howto.mp4` (no accents, underscores).

## Step 9 — Check (before showing)

Grab 6–9 frames at key moments into one contact sheet (`ffmpeg -ss T -frames:v 1`, then `hstack`/`vstack`) and **look at it**: captions not covering titles or highlights, highlights on the right element, no real data, readable and correct text, brand look applied, highlight timed to its sentence. Fix before delivering. Never report a check you did not do.

## Step 10 — Deliver (gate 3)

Send the MP4 so it renders inline. Short list: what each part shows, "all data is fictional", any known small issue (offer to fix), take B exists. Ask for feedback; on revisions change only what was asked, re-render, re-check.

## Step 11 — Distribution (gate 4, only what the brief asked for)

**Unlisted YouTube:** ask whether Claude should upload it via a browser tool, or give the user a ready prompt to run themselves. Settings:
- Title `<Brand/Tool> – <Feature>: how-to` (in the narration language); description: one sentence on what it shows + "Only fictional names and amounts appear in this video."
- Audience: not made for kids; no age restriction; no playlist; no paid promotion.
- Show more: automatic chapters and key moments OFF; language per brief; category Education; standard YouTube licence; **embedding ON**; publish to subscriptions feed OFF; comments OFF; show like count OFF.
- Video elements: none. Wait for the copyright check; stop and report if it flags anything.
- Visibility **Unlisted** — double-check that Public and Private are not selected. Never Public or Scheduled.
- Don't change channel/account settings or accept new terms; stop and ask if prompted.
- Return: link (`youtu.be/…`), the 11-character video ID, and the confirmed settings.

**In-app / site embed:** write a coding-agent prompt (e.g. for Claude Code) that:
- inspects and reuses any existing help-video pattern instead of building a new one;
- adds the button/dialog with `https://www.youtube-nocookie.com/embed/<ID>?rel=0`, rendering the iframe **only when the dialog is open** (nothing loads from YouTube before the click);
- follows the repo's existing code style and conventions;
- runs typecheck + build; stages only the changed files explicitly; commits and pushes with a clear message;
- ends with **DO NOT start a dev server.**
After it reports back, verify live if a browser is available.

**Email:** an email **draft** (never send without the user's go-ahead), in the existing thread with the agreed recipients: what it shows in 2–3 lines, the video link, what to try and when, the user's usual greeting and sign-off. Return the draft link.

## Profiles

Add one block per brand or client to override the defaults. Keep client-confidential details (repo names, people, internal workflows) only in your private copy, never in a shared one.

### Example profile
- Repo `<owner>/<repo>` (branch); visual mode: rebuilt UI (card style, the app's fonts and colours), highlight colour; ID format like `DEMO-2026-001`.
- Voice: `<voice name>` (look up the ID in the voice tool; don't hard-code it in shared copies).
- Narration: language, address form, greeting; closing line and end card text.
- Delivery: MP4 → unlisted YouTube on `<channel>` → embed via `<existing help-video component>` → email draft in `<thread>`.
- File name `<Brand>_<Feature>_howto.mp4`.

## Rules

- No copyrighted music, characters or footage; third-party UIs only as screenshots of the product being explained, never presented as official.
- No real personal data in the video.
- Never upload as Public; never send an email without explicit go-ahead.
- Ask before spending credits beyond what was approved.
- Keep the attribution header of this skill intact when sharing or modifying it (CC BY-NC-SA 4.0).

---
*How-to Video Skill © 2026 Víg Réka / The WOW Studio · CC BY-NC-SA 4.0 · Commercial licensing: hello@rekavig.com*
