# Cursor camera · omnigami

Your real screen, a cursor and a camera that follows it.

An eight-second proof: your product’s real screen, a big cursor glides to one control and clicks it, the camera zooms in on the click, the screen changes to the real result, and the camera pulls back out.

Watch it play live, and change its words, at [omnigami.ai/skills/cursor-camera](https://omnigami.ai/skills/cursor-camera).

## Install

In Claude Code:

```
/plugin marketplace add omnigami-ai/skills
/plugin install omnigami-cursor-camera@omnigami
```

With the skills CLI, for Claude Code and other agents that read SKILL.md:

```bash
npx skills add omnigami-ai/cursor-camera
```

Or copy `skills/cursor-camera/` into your agent's skills folder (for Claude Code, `~/.claude/skills/cursor-camera/`). Then ask:

```
Make a cursor-camera shot of the main feature on https://your-product.com
```

## What it runs

The skill works on your computer. It runs the Node scripts in `skills/cursor-camera/scripts/`: they open your product's pages in a local headless browser to capture its real screens, then render the film with that browser and ffmpeg, writing MP4s and an editable HTML film to your project. It sends nothing to omnigami or anyone else, and uses no network beyond loading your own product's pages and the fonts and assets in this folder.

## You need

- Claude Code with Opus 5.5
- Node 20 or later
- ffmpeg
- Chrome, Chromium, Edge or Brave

None beyond your Claude plan’s usage. Node, ffmpeg and the browser are free.

## Licence

Free to use. Use the films and anything else the skill makes for anything, commercial work included. Don't redistribute the skill. See [LICENSE.md](LICENSE.md). The bundled fonts keep their own licence (SIL Open Font License, beside them in `reference/assets/fonts/`).

## Credits

Style inspired by the grammar of Figma’s “Figma Motion” (https://x.com/figma/status/2069827742800253230), ElevenLabs’ “Reception” (https://x.com/ElevenLabs/status/2100262886916358361), @LexnLin’s “Tessel” (https://x.com/LexnLin/status/2104148233106723099): an independent style study; none of them made or endorsed this skill. Its example shows Lamplit, a fictional company made for omnigami’s examples, with sample data.

omnigami is not affiliated with Anthropic. More skills at [omnigami.ai](https://omnigami.ai).
