# Cursor camera · omnigami

Your real screens, a cursor and a camera that follows it.

An 18-second demo of one real task on your product’s real screens. A big cursor glides between targets, lights what it hovers, clicks, scrolls and drags a selection, and the camera it carries pushes in and pulls back with it, ending on the real result.

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
Make a cursor-camera demo of the main task on https://your-product.com
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

Its example shows Lamplit, a fictional company made for omnigami’s examples, with sample data.

omnigami is not affiliated with Anthropic. More skills at [omnigami.ai](https://omnigami.ai).
