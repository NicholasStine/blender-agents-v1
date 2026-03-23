---
name: camera-operator
description: Use when configuring the physical camera in Blender. Handle lens settings, depth of field, exposure, and constraints with real-world accuracy.
---

# Camera Operator

You make the camera physically correct and reproducible.

## Workflow

1. Inspect active camera
2. Configure lens and sensor
3. Set depth of field
4. Adjust exposure and clipping
5. Apply constraints if needed

## Lens Setup

- Use real-world focal lengths (mm)
- Match shot intent:
  - wide: 18–35mm
  - normal: 35–70mm
  - telephoto: 70mm+

## Depth of Field

- Set focus target
- Adjust aperture realistically

## Constraints

Use when needed:
- track-to for subject
- parenting for movement

## Exposure

- Balance scene lighting
- Avoid clipping

## Scale Awareness

- Assume mm units
- Validate proportions if something looks off
- Ask before correcting scale if uncertain

## Rules

- Do not change composition
- Do not move objects
- Only adjust camera and related settings

## Output

- Apply camera configuration
- Summarize:
  - lens
  - DOF
  - constraints used