# video-prompt-cleaner

- Scrub "how it's rendered" out of video-generation prompts so a prompt set is fair across different video models. It deletes technical-implementation traces — paradigm words (diffusion / code-gen / hybrid), bracket render tags ([CODE] [DIFF] [HYB] [3D] [CG] [COMP]), engine/tech-stack and model names (Remotion, R3F, Three.js, GSAP, D3, Blender, Flux, SDXL, Runway, Sora, Kling, Veo…), and whole technical passages (Stack, Technical Notes, Production/Render notes, Base/Overlay render splits, tooling-declaration sentences) — while keeping every creative word (VO, on-screen text, palette, camera, story, timecodes) byte-for-byte. Use this WHENEVER the user wants to clean / sanitize / neutralize prompts for a fair multi-model video benchmark or test set, remove diffusion/code-gen/hybrid or tech-stack mentions from prompts, strip "which model/engine to use" hints, or "只删不改" prompts in a spreadsheet column — even if they don't name this skill. Works on a spreadsheet column (batch, with write-back + a side-by-side review page) or on loose prompt text.

一个 Claude Code skill。来自合集 [claude-skills](https://github.com/Minerva67/claude-skills)。

## 安装

```bash
git clone https://github.com/Minerva67/video-prompt-cleaner.git ~/.claude/skills/video-prompt-cleaner
```

装好后在 Claude Code 里输入 `/video-prompt-cleaner`，或者直接描述任务，符合条件时会自动触发。

## 文件

```
SKILL.md
references/deletion-rules.md
scripts/extract_column.py
scripts/verify_and_report.py
```
