# VWorld configuration & developer examples

**Set up the world, keep the original.** These concise examples are based on the documented **VWorld 1.1.0-preview.3** behavior for **Paper 26.2**, **Java 25** and **WorldEdit 7.4.6** where schematics are involved.

| Reference | What you'll find |
| --- | --- |
| [Configuration example](config.example.yml) | Recognized `config.yml` keys, protected worlds, defaults and bounded template limits |
| [Template walkthrough](template-workflow.md) | Real `/vworld worlds` commands to import, preview, mark positions and release |
| [Developer/API example](consumer-integration.md) | Small illustrative `WorldProvider` service excerpt, ownership rules and private-source access |

## Important boundaries

- The YAML is a **reference**, not a universal drop-in replacement for an existing `plugins/VWorld/config.yml`. Back up your setup before changing anything.
- `worlds.yml`, `templates.yml` and `languages.yml` contain plugin-managed state. Do not paste these examples over saved files or edit generated ownership markers.
- `CastleArena` is a sample template ID. The `castle_arena.schem` file is **not included**. Upload your own valid file through the host's file manager before importing.
- `max-lease-seconds` is a cleanup safeguard, not a game timer. A minigame must separately manage its own match lifecycle and player restoration.
- VWorld's implementation **source, JAR builds and complete integration documentation are private**. The developer excerpt illustrates a public-facing contract without publishing implementation code.
- These examples do **not** add a web uploader, new admin commands, production performance guarantees or unverified Folia/FAWE support.

For a project overview and verified preview limits, return to the [VWorld README](../README.md).

Copyright © 2026 VACK STUDIO. All rights reserved.
