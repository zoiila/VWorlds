# Preparing a VWorld schematic template

This guide shows the documented command flow for **VWorld 1.1.0-preview.3**. It is a reference for administrators, not a new auto-import or in-game upload feature.

## Before you begin

- Use **Paper 26.2**, **Java 25** and a separately installed **WorldEdit 7.4.6**.
- Back up your existing worlds and VWorld data before installing or upgrading.
- Export a supported **Sponge `.schem` version 2 or 3**. Legacy `.schematic`, `.litematic` and entity-bearing schematics are not accepted.
- Put `castle_arena.schem` inside `plugins/VWorld/schematics/` with your host's file manager.

## 01 — Register a reusable source

```text
/vworld worlds scan
/vworld worlds import CastleArena castle_arena.schem
/vworld worlds list
/vworld worlds info CastleArena
```

`CastleArena` is an **example template ID**, not a built-in map. IDs are case-sensitive. VWorld registers the metadata and validates the source; it does not overwrite the original schematic.

## 02 — Preview and mark positions

```text
/vworld worlds preview CastleArena
/vworld worlds sessions
/vworld worlds enter <session-uuid>
```

The preview command reports a session UUID. Switch to **Creative or Spectator** before entering that preview. Survival entry is intentionally refused because the preview may contain void.

While standing in the ready preview world, use the following commands at the appropriate locations:

```text
/vworld worlds setpos1 CastleArena
/vworld worlds setpos2 CastleArena
/vworld worlds setpoint CastleArena spawn
/vworld worlds setpoint CastleArena spectator
/vworld worlds info CastleArena
```

The bounds are optional and relative to the schematic's anchor; named points are saved with yaw and pitch. Set only the points your integrating game needs. Bounds must be complete, valid and properly ordered.

## 03 — Release the preview

```text
/vworld worlds release <session-uuid>
/vworld worlds sessions
```

VWorld evacuates occupants to a loaded safe world, then unloads and cleans up **the temporary world it owns**. If safe cleanup fails, the session is retained for inspection or retry. Do not manually delete ownership markers or temporary-world folders.

## Useful corrections

```text
/vworld worlds clearbounds CastleArena
/vworld worlds clearpoint CastleArena spectator
/vworld worlds name CastleArena Castle Arena
```

To remove an entry from the registry without deleting its source file:

```text
/vworld worlds unregister CastleArena confirm
```

**For minigame developers:** an actual game integration must use VWorld's `WorldProvider` service and request a unique lease per match. See [Consumer integration](consumer-integration.md) for a deliberately limited API example; this administrator setup is not a gameplay plugin.
