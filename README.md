# Wave Race 64: Recompiled — Linux release

This repo is the **Linux release** of Wave Race 64 Recompiled.
Upstream (Windows/macOS) lives at
[elliotttate/wave-race-64-recomp](https://github.com/elliotttate/wave-race-64-recomp).

## Install

Download `waverace64-recomp_0.4.0_amd64.deb` from
[Releases](https://github.com/davkdavk/wave-race-64-recomp/releases/latest),
then:

```bash
sudo apt install ./waverace64-recomp_0.4.0_amd64.deb
waverace64-recomp
```

Requires a Vulkan driver (`mesa-vulkan-drivers` on AMD/Intel).
Tested on Debian 13 trixie x86_64 with an RX 7800 XT (RADV).

## ROM

You need **Wave Race 64 (USA) (Rev A / v1.1)** — 8 MiB `.z64`,
sha1 `508dfc2d4caa42b6f6de5263d0aed5e44ac7966a`.
Pick it in the launcher. No game data is included.

Verify a dump:

```bash
waverace64-recomp --identify your.z64
```

## What's bundled

HD textures (1828 mappings), 9 replacement music tracks, modern/Aqua water.
Settings and saves live in `~/.local/share/WaveRace64Recomp/`.

## Build from source

See [docs/BUILDING_LINUX.md](docs/BUILDING_LINUX.md).

## Licensing

Port code MIT. The binary links GPL-3.0 N64ModernRuntime, so the built
package is GPL-3.0 as a whole. Bundled music/artwork belong to their owners.
No affiliation with Nintendo. Supply your own dump.
