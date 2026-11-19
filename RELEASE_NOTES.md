> **Historical archive:** These notes describe the earlier Vack Worlds 1.0.0 project, not the currently presented VWorld 1.1.0-preview.3. The public repository does **not** contain or distribute the JAR mentioned in the historical notes. See [README](README.md) for the current public project overview.

# Vack Worlds v1.0.0 | Vack Studio

First release: world creation and import, per-world properties, on-demand loading, asynchronous template forks, protected deletion, spawn and teleport, a minigame Java service, and English/Arabic UUID-persisted command feedback.

Requirements: VackMini 0.1.0 / Minecraft 26.2, Java 25. Built against Paper API `26.2.build.130-stable`.

Installation: Copy `VackWorlds-1.0.0.jar` into `plugins/` and restart the server.

Validation: Gradle `clean build` passed on Java 25. The provided server began startup but network socket binding was blocked by the isolated test environment before plugin enable. Live server and two-player tests remain pending.

Download: `VackWorlds-1.0.0.jar`. Checksum: see `SHA256SUMS.txt`.

Copyright (c) Vack Studio. All rights reserved.
