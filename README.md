# Motion Graphics — Claude Skill

An AI Motion Graphics Director + Producer + Animator. A reusable [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that takes a creative brief — a topic, a message, a brand, a reference, a rough idea — and produces a polished, professional motion-graphics video: deterministic rendering, beat-synced animation, synthesized soundtrack, h264 delivery.

Built from a real production run: a 15-second, 6-scene, 60fps showreel rendered with 900 deterministic canvas frames, headless Chrome capture, a fully synthesized numpy soundtrack, and ffmpeg encode.

## Demo

**[▶ Watch the demo showreel](https://github.com/Hosseinamiri850/motion-graphics-skill/releases/download/v1.0.0/showreel-demo.mp4)** — 15s, 1920x1080, 60fps, six beat-synced scenes (kinetic type, identity build, data-viz motion, inverted type playground, 3D wireframe globe, outro lockup) with a fully synthesized soundtrack. Produced end-to-end by this skill's pipeline.

## What it makes

| Use case | Example brief |
|---|---|
| Résumé / showreel | "Make a 15s motion showreel that shows what an incredible motion designer I am" |
| Logo animation / ident | "Animate our logo — luxury, minimal, 5 seconds" |
| Kinetic typography | "Lyric-style kinetic type for this quote, 10s, square for Instagram" |
| Title sequence | "Opening titles for our conference talk, cyberpunk mood" |
| Data-viz motion | "30s animated growth story from these numbers" |
| Product / UI showcase | "Product reveal from these screenshots, dark and cinematic" |
| Social clip | "15s vertical clip announcing our launch" |
| Concept sequence | "Abstract music-driven piece, 20s, ambient mood" |

## Install

### Claude Code (local)

```bash
git clone https://github.com/Hosseinamiri850/motion-graphics-skill.git
mkdir -p ~/.claude/skills
cp -r motion-graphics-skill/motion-graphics ~/.claude/skills/
```

Restart Claude Code. The skill auto-activates on motion-graphics requests, or invoke explicitly with `/motion-graphics`.

### Claude Desktop / other harnesses

Copy the `motion-graphics/` folder into your harness's skills directory (or import `SKILL.md` into any agent harness that reads skill folders). The skill is self-contained: an agent that has never seen this conversation can read it and produce professional motion graphics from a new brief.

## How it works

```
Brief → Analysis → Concept → Visual Direction → Storyboard → Shot Design
      → Animation → Preview → Iterate → Render → Encode → Quality Check
```

1. **Brief analysis** — extract message, duration, platform/ratio, tone, audio, references. Write a one-sentence creative idea before coding; every scene must serve it.
2. **Concept + storyboard** — scenes get a job (hook / identity / proof / energy / depth / resolution), one dominant element each, staggered entrance timing, and a cut/crossfade behavior. Visual climax at ~70–80%.
3. **Visual direction** — one palette (1 bg / 1 ink / 1 accent), one shape family, one type system, post-grade (grain, vignette, letterbox). Accent scarcity and post-grade are what make scenes feel like one film.
4. **Implementation** — inspects the environment (headless Chrome + ffmpeg preferred; Remotion/Blender/AE guidance included) and picks the best path. **Determinism rule**: every animated value is a pure function of frame index — seeded PRNG only.
5. **Animation craft** — easing library with assignment rules (nothing linear), arc-length draw-on, 40–80ms stagger, beat sync, camera settle/push transitions, fibonacci-sphere 3D wireframes, per-letter typography.
6. **Soundtrack** — fully synthesized, deterministic numpy soundtrack: kick/hats/clap/bass/arp/risers/impacts, sidechain duck, dotted-8th delay, scene boundaries on bar lines.
7. **Capture + encode** — preview stills first (inspect visually, fix, repeat), then full frame capture, `ffmpeg` h264 `yuv420p` + `faststart`, verified with `ffprobe`.
8. **Quality control** — mandatory visual inspection checklist (dark-on-dark bugs, focal clarity, accent scarcity, motion sanity, determinism), plus failure-mode table with fixes.

## What's inside

```
motion-graphics/
├── SKILL.md                          # main workflow + methodology
├── references/
│   ├── animation-principles.md       # easing, timing, draw-on, typography,
│   │                                 #   camera, particles, 3D, grain, determinism
│   ├── reference-analysis.md         # 13-dimension grammar extraction,
│   │                                 #   analyze-don't-imitate process
│   └── qc-checklist.md               # pre-delivery checklist
└── scripts/
    ├── scene_template.js             # deterministic canvas renderer skeleton
    ├── capture_template.mjs          # headless Chrome frame capture harness
    └── audio_template.py             # synthesized soundtrack generator
```

## Requirements

- Node.js 18+ and a headless-capable Chromium (Chrome or Edge — paths in `capture_template.mjs`)
- Python 3 with numpy (for the soundtrack)
- ffmpeg (encode)
- Claude Code, Claude Desktop, or any agent harness that loads skill folders

No motion-graphics software required — no After Effects, no Blender, no paid tools. Everything renders in a browser canvas and encodes with ffmpeg.

## Design principles baked in

- **Analyze, don't imitate** — references are mined for visual grammar (composition, color relationships, motion language, pacing), then rebuilt in the subject's own language. Never copied.
- **Every element earns its place** — if an effect can't be justified ("draw-on = being made", "beat pulse = energy", "slam = emphasis"), it gets deleted.
- **Determinism** — seeded PRNG everywhere; re-renders are frame-identical, partial re-capture works, parallel batches work.
- **Accent scarcity** — one highlighted element per scene. Scarce accents read as designed; abundant accents read as template.
- **Strong opening, clean ending** — hook in the first 2 seconds, lockup + fade at the end. Never abrupt.

## Example prompt

> "Make a 10-second square motion graphic announcing our API launch. Dark, technical, cyan accent. Beat-synced. Use the motion-graphics skill."

## License

MIT
