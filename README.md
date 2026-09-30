# Listing to 3D

A reusable Codex skill that turns an individual real-estate listing link into a plan-based, furnished, walkable 3D reconstruction of the actual property.

Paste a listing URL into a new Codex chat, or invoke the skill explicitly:

```text
$listing-to-3d https://example.com/property-listing
```

Automatic invocation is enabled. An explicit request such as “summarize this listing” takes precedence and does not start a reconstruction.

## Install

Clone this repository into your personal Codex skills directory:

```sh
git clone https://github.com/aek15/listing-to-3d.git ~/.codex/skills/listing-to-3d
```

If that folder already contains an installation, preserve any local edits before replacing or updating it. Start a new Codex chat after installation to make the skill available.

## What it does

1. Collects and inspects available photographs, floor plans, dimensions, panoramas and video.
2. Creates a photo-to-room map, shared metric geometry, camera estimates and uncertainty record **before implementing the scene**.
3. Builds real 3D geometry with the photographed layout and furnishings, walking controls, collision and an inspection camera.
4. Compares rendered viewpoints against every property photograph and checks the furnished circulation routes.
5. Delivers the runnable project, source records, saved renders and a validation report.

If the listing, a listed photograph, or a usable floor plan remains inaccessible, the skill stops before scene implementation and identifies the files the user needs to supply. Video and panoramas are optional when the listing does not provide them.

## Requirements

Use in Codex with filesystem access, code execution and supported browser access. Scene dependencies are resolved for each project; Three.js is the suggested default, not a hard requirement. The optional contact-sheet helper requires Python 3 and Pillow. The skill does not itself include a standalone reconstruction engine or host generated scenes.

## Files

- [SKILL.md](SKILL.md): entrypoint, automatic trigger and workflow.
- [agents/openai.yaml](agents/openai.yaml): skill metadata and invocation policy.
- [references/source-analysis.md](references/source-analysis.md): source collection, geometry interpretation and photo matching.
- [references/scene-and-validation.md](references/scene-and-validation.md): scene construction, navigation and verification.
- [scripts/contact_sheet.py](scripts/contact_sheet.py): labeled source inventories and reference/render comparison sheets.

For helper usage:

```sh
python scripts/contact_sheet.py --help
python scripts/contact_sheet.py inventory --help
python scripts/contact_sheet.py compare --help
```

## Accuracy and scope

Floor plans constrain structure; photographs provide appearance and spatial evidence. Measured dimensions, inferred dimensions and unresolved discrepancies must be distinguished. The result is a visual reconstruction, not a survey-grade or photogrammetric digital twin. Multi-floor properties require actual stair and level connectivity.

This repository contains the reusable skill only. Property photographs, generated scenes and the apartment used to develop the workflow are not bundled. Rights to downloaded listing material remain with their respective owners. External publication of generated projects or source assets requires separate authorization.
