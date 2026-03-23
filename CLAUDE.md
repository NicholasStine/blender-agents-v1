# Blender Production Pipeline

This project uses a multi-agent skill pipeline to produce 3D scenes in Blender via the Blender MCP server.

## Agents

| Skill | Role |
|---|---|
| `/script-reader` | Translates a script or scene idea into tone, lighting direction, and a concrete prop list |
| `/set-designer` | Lays out the scene — places hero, supporting, and background objects |
| `/sculptor` | Creates or modifies geometry; builds multipart assemblies |
| `/painter` | Applies materials, textures, and surface detail |
| `/cameraman` | Decides framing, shot type, and composition |
| `/camera-operator` | Configures the physical camera — lens, DOF, exposure, constraints |

## Primary Pipeline

```
script-reader
     │
     ▼
set-designer
     │
     ├──► sculptor   (repeat per object that needs modeling)
     │
     ├──► painter    (repeat per object that needs materials)
     │
     ▼
cameraman
     │
     ▼
camera-operator
```

## Iteration Paths

Agents loop back when output is unsatisfactory. Re-invoke the agent at the point where the issue originates — not earlier.

```
camera-operator ──► cameraman          if composition feels wrong after technical setup
cameraman       ──► camera-operator    if shot choice requires a different lens or DOF
painter         ──► sculptor           if surface detail reveals a geometry problem
sculptor        ──► painter            if new geometry needs materials applied
set-designer    ──► sculptor           if a required object doesn't exist yet
set-designer    ──► painter            if placed objects need materials before layout reads correctly
set-designer    ──► cameraman          if layout changes invalidate the chosen shot
any agent       ──► script-reader      if intent is ambiguous and the brief needs re-reading
```

## Rules

- Always start with `/script-reader` when working from a script or scene idea.
- Each agent operates only within its domain — do not cross responsibilities.
- Pass the script-reader output forward explicitly; downstream agents depend on it.
- Use mm units and real-world scale throughout.
- Re-check the viewport after every significant change.
