# How-to Video Skill for Claude

A Claude skill that turns a short Q&A into a narrated, step-by-step tutorial video (MP4) for any brand, web app or tool.

**Created by [Víg Réka](https://github.com/RekaWeb3Design) — The WOW Studio.**
Free for non-commercial use under [CC BY-NC-SA 4.0](LICENSE).

## What it does

1. On first run, asks which voice to use (your own cloned ElevenLabs voice, a stock voice, or captions only) — it never uses someone else's voice ID.
2. Asks a few questions and shows a brief for approval: if it finds branding in your project (colours, fonts, logo), it asks whether to use it or something else; it also asks whether to show a logo or a name credit, and where (corner, watermark, or title/end card only).
3. Gets the visuals: for web platforms it can open them in your Chrome via Claude in Chrome and take the screenshots itself (navigation only — it never saves, submits or signs in); otherwise it uses your screenshots or rebuilds the UI from code.
4. Writes a scene-by-scene script and waits for approval — no credits are spent before this.
5. Generates the voiceover (ElevenLabs) or falls back to captions only.
6. Uses **fictional data only** (real data is covered), animates highlights, cursor and captions, and renders the video with Playwright + ffmpeg.
7. Checks key frames before delivery, then optionally uploads it as an unlisted YouTube video, writes an embed prompt, or drafts an email.

## Requirements

- Claude with skills and code execution (Claude app or Claude Code)
- `node`, `ffmpeg`, Playwright Chromium (the skill installs Playwright if missing)
- Optional: ElevenLabs connector (voiceover — on first run the skill asks which voice to use), Claude in Chrome (captures screenshots of web platforms by itself and uploads to YouTube), an email connector (drafts)

## Install

**Claude app:** zip the `howto-video` folder and upload it in the Skills section of Settings.
**Claude Code:** copy the `howto-video` folder into `~/.claude/skills/` (or `.claude/skills/` in a project).

Then ask: *"Make a how-to video about …"*

Add your own brand/client setups in the **Profiles** section of `SKILL.md` — keep confidential details in your private copy only.

## Licence

© 2026 Víg Réka / The WOW Studio — [CC BY-NC-SA 4.0](LICENSE). See [NOTICE](NOTICE).

- ✅ Use it, share it, adapt it — with credit to *Víg Réka / The WOW Studio*
- ✅ Share modified versions under the same licence
- ✅ Make videos for yourself, your team, or your clients — free of charge
- ❌ No selling, reselling, or bundling into paid products, courses or skill packs
- ❌ No charging clients or customers for videos made with this skill

Commercial licensing: hello@rekavig.com

---

### Magyarul röviden

Claude skill, amely néhány kérdés után narrált, lépésről lépésre haladó útmutató videót készít bármilyen márkához, webapphoz vagy eszközhöz. Első futáskor megkérdezi, milyen hangot használjon, webes platformoknál pedig a Claude in Chrome segítségével maga is tud képernyőképeket készíteni. Szabadon használható és továbbadható nem kereskedelmi célra, a szerző (Víg Réka / The WOW Studio) feltüntetésével. Ügyfeleknek ingyen készíthetsz vele videót, de a vele készült videókért pénzt kérni, illetve a skillt eladni vagy fizetős termékbe, kurzusba csomagolni engedély nélkül nem szabad. Kereskedelmi licenc: hello@rekavig.com
