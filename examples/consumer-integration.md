# VWorld developer reference & source access

**VWorld 1.1.0-preview.3** keeps its implementation source, runtime JARs and full integration documentation **private**. This public page provides a small, newly written API usage illustration—not the VWorld implementation, not a full integration, and not a public SDK download.

## Integrating a minigame

VWorld exposes the `studio.vack.worlds.WorldProvider` service to consumers on **Paper 26.2 / Java 25**, with verified **WorldEdit 7.4.6** for schematic support. The existing `WorldsApi` is for traditional whole-world management; it is not the temporary-world provider.

A consuming plugin should compile against its authorized VWorld JAR using `compileOnly` or `provided`. If the integration is required, declare `depend: [VWorld]` in its own `plugin.yml`. Do not shade VWorld or WorldEdit.

The following **illustrative excerpt** shows the service and request names. It is intentionally **not a drop-in Java class**: the integrating game must implement the callback and match-lifecycle logic described below.

```java
// Illustrative only. Run on the Paper primary thread.
// gamePlugin is the integrating plugin's own Plugin instance.
WorldProvider provider =
    Bukkit.getServicesManager().load(WorldProvider.class);

if (provider == null) {
    throw new IllegalStateException("VWorld schematic provider is unavailable");
}

WorldProvider.Request request =
    provider.request(gamePlugin, "CastleArena", Duration.ofSeconds(120));

// Retain this Request for the current match. Never block the server tick thread.
request.ready().whenComplete((lease, failure) -> {
    // The real minigame must validate its match generation here.
    // On failure or stale callbacks: cancel/release that exact request.
    // On success: validate lease.point("spawn") and any other required points.
    // Teleport with the game's existing player-restoration handling.
    // Mark the lease in use only when the match becomes active.
    // On every finish/abort/disable path: release the lease or cancel the request.
});
```

**Explicit cleanup calls:** use `request.cancel()` when setup is abandoned or a request is still pending; once a lease is available, use `lease.release()` on match finish, abort or disable. Both are idempotent. The example deliberately leaves game-specific restoration and generation checks to the consumer.

The API above is the documented **Request → Lease** flow. A request timeout (1–600 seconds) covers preparation, **not** game length. `max-lease-seconds` is an emergency cleanup age, **not** a countdown or renewal mechanism.

## Ownership contract

| VWorld manages | The game integration manages |
| --- | --- |
| Schematic registration, validation and integrity | Queue selection, timers, roles and gameplay |
| One owned temporary world per successful lease | Player entry, safe teleports and player-state restoration |
| Lease states, evacuation, unload and owned cleanup | Required spawn/spectator points and bounds enforcement |
| Retained failed sessions for administrator review | Releasing/cancelling the right request on every terminal path |

Keep the Request/Lease **per match**, use a generation token to ignore stale callbacks, and never block the Paper primary thread with `.join()` or `.get()`. Missing WorldEdit, unsupported reader versions, missing points, capacity failures or invalid templates must fail setup clearly. Do not silently fall back to a shared mutable arena.

VWorld never authorizes a consumer to delete schematic sources or temporary dimension folders. Even when a release fails, retain the failure and retry through the provider rather than bypassing ownership checks.

## Source availability

The actual VWorld Java implementation, complete integration contract and runtime artifacts are not distributed in this public presentation repository. Authorized developers should request access through **VACK STUDIO** using the official contact links in the [main README](../README.md). Public examples are instructional excerpts, not full configuration files, production-ready adapters, source releases or evidence of tested compatibility for other platforms.

Copyright © 2026 VACK STUDIO. All rights reserved.
