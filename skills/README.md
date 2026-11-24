# Skills de diseño/motion (vendorizadas)

Origen: https://github.com/freshtechbro/claudedesignskills (MIT, ver `LICENSE-claudedesignskills`), snapshot 2025-11-19.
Solo las relevantes para webs/landings (fuera: Babylon, PlayCanvas, A-Frame, PixiJS, Blender, Substance).

Instalación (symlinks a user scope):
```
for d in /Users/mikel/Desktop/Dev/MR-AGENTS/skills/*/; do ln -sfn "${d%/}" "$HOME/.claude/skills/$(basename "$d")"; done
```

Las usan los agentes del swarm de diseño leyendo `~/.claude/skills/<skill>/SKILL.md` (+ `references/`) antes de implementar.
