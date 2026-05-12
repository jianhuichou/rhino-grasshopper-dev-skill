# Rhino Grasshopper Dev Skill

Codex skill for creating, reviewing, building, deploying, and testing Rhino 8 Grasshopper components, C# GHA plugins, RhinoCommon code, Rhino 8 Python 3 scripts, ScriptEditor plugins, Yak packages, and RhinoMCP-driven Rhino or Grasshopper automation.

The skill is stored in `rhino-grasshopper-dev/`. The repository root contains only sharing documentation and repository metadata.

## Install

Install from GitHub with the Codex skill installer:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo YOUR_GITHUB_USERNAME/rhino-grasshopper-dev-skill \
  --path rhino-grasshopper-dev
```

Replace `YOUR_GITHUB_USERNAME` with the account or organization that owns the repository.

## Validate

After installing or editing the skill, validate it with:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  ~/.codex/skills/rhino-grasshopper-dev
```

## What It Covers

- C# Grasshopper `.gha` component scaffolding and review.
- RhinoCommon component and plugin conventions for Rhino 8.
- Rhino 8 Python 3 Grasshopper script and ScriptEditor plugin guidance.
- Workflow-level data-flow design for connected component sets.
- Static project inspection helpers.
- RhinoMCP endpoint smoke testing.
- Build, deployment, Yak packaging, and Grasshopper load-test guidance.

## Notes

This skill uses McNeel documentation and McNeel Discourse as source-of-truth references. Blogs and social posts should remain supplemental workflow examples only.
