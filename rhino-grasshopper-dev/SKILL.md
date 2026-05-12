---
name: rhino-grasshopper-dev
description: Create, review, build, deploy, and test Rhino 8 Grasshopper components, C# GHA plugins, RhinoCommon components, Rhino 8 Python 3 Grasshopper scripts, ScriptEditor-published plugins, Yak packages, and RhinoMCP-driven Rhino or Grasshopper automation. Use when working on custom Grasshopper components, .gha projects, RhinoCommon code, Rhino 8 Python 3 script components, Grasshopper definition review, plugin packaging, deployment, or automated smoke testing.
---

# Rhino Grasshopper Dev

## Overview

Use this skill for Rhino 8 and Grasshopper development work that needs repo-first inspection, source-of-truth McNeel guidance, and practical validation. Keep edits small, preserve released component GUIDs, and separate stable engineering logic from Grasshopper UI wrappers where possible. When creating a plugin or a set of connected components, design the workflow data flow first: define the upstream inputs, intermediate data contracts, downstream outputs, component linkages, data-tree topology, and user-facing parameter names before implementing individual components.

## Mode Selection

- **C# GHA component or RhinoCommon plugin**: read `references/csharp-gha.md`. Use `scripts/scaffold_csharp_gha.py` only when starting a new small project or test fixture.
- **Rhino 8 Python 3 Grasshopper script or ScriptEditor plugin**: read `references/python3-script-plugins.md`.
- **Review, test, deploy, CI, Yak, package restore**: read `references/testing-and-deployment.md`.
- **Live Rhino or Grasshopper automation through MCP**: read `references/rhino-mcp.md`; prefer direct MCP tools when available and `run_python` for non-trivial RhinoCommon or Grasshopper API work.
- **Need source authority or further reading**: read `references/official-sources.md`.

## Standard Workflow

1. Inspect the project before editing: `.sln`, `.csproj`, package references, build scripts, deploy scripts, `manifest.yml`, component classes, GUIDs, tests, and local instructions.
2. Identify the artifact type: script component, ScriptEditor project, compiled `.gha`, Rhino `.rhp`, Yak package, or live Rhino/Grasshopper canvas.
3. For plugins or connected component sets, map the whole workflow before coding: input sources, component boundaries, intermediate geometry/data types, tree branch semantics, optional versus required parameters, output consumers, and expected linkages on the Grasshopper canvas.
4. Preserve public surface: component names, nicknames, categories, parameter order, serialization data, file formats, GUIDs, and numerical behaviour unless the user explicitly asks to change them.
5. Validate inputs at numerical and geometry entry points: nulls, empty lists, tree structure, units, tolerances, coordinate system, invalid curves/Breps/meshes, and missing Rhino documents.
6. Report Grasshopper-facing failures with `AddRuntimeMessage` for C# components or clear output/error messages for scripts. Do not fail silently.
7. Run the most relevant checks: static inspection, `dotnet build`, unit tests, Yak build, Rhino/Grasshopper load test, RhinoMCP smoke test, or viewport/selection inspection.

## Utility Scripts

- `scripts/check_rhino_mcp.py`: verify a RhinoMCP HTTP endpoint and list exposed tools.
- `scripts/inspect_gha_project.py`: static inspection for common C# GHA project risks such as missing Grasshopper references, duplicate `ComponentGuid` values, and missing runtime messages.
- `scripts/scaffold_csharp_gha.py`: create a minimal C# Grasshopper component project for a first test or throwaway scaffold.

Run scripts with `python3` and read their `--help` output before use. They are intentionally conservative and do not modify existing projects unless an explicit output path is supplied.

## Review Checklist

- Does the project target the correct runtime for the user: Rhino 8 .NET Core on macOS, optional .NET Framework mode on Windows, or Rhino 7 compatibility?
- Are RhinoCommon and Grasshopper references sourced from NuGet or project templates rather than brittle machine-local paths?
- Are Rhino/Grasshopper assemblies excluded from output copying?
- Is every component GUID unique and stable?
- Are parameter names, nicknames, descriptions, access modes, and type hints explicit?
- For connected components, does each component have a clear role in the full workflow, with minimal duplicated inputs and outputs shaped for the next downstream component?
- Are linkages between components obvious from parameter names, access modes, and output data structures?
- Are data-tree operations intentional rather than accidental flatten/graft/simplify side effects?
- Are geometry tolerances and document units explicit where they affect interpretation?
- Is deployment through Yak or a documented local development folder, with Rhino restart requirements stated?
