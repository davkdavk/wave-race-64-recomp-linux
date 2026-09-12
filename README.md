# Wave Race 64: Recompiled — Linux release

This repo is the **Linux release** of Wave Race 64 Recompiled.
Upstream (Windows/macOS) lives at
[elliotttate/wave-race-64-recomp](https://github.com/elliotttate/wave-race-64-recomp).

## Debian Install

Download `waverace64-recomp_0.4.0_amd64.deb` from
[Releases](https://github.com/davkdavk/wave-race-64-recomp/releases/latest),
then:

```bash
sudo apt install ./waverace64-recomp_0.4.0_amd64.deb
waverace64-recomp
```

Requires a Vulkan driver (`mesa-vulkan-drivers` on AMD/Intel).
Tested on Debian 13 trixie x86_64 with an RX 7800 XT (RADV).

## Steam Deck Install

**Steam Deck package requires testing.** It is provided as a portable Linux
build for SteamOS, but it has not yet been validated on real Steam Deck
hardware.

Download `waverace64-recomp_0.4.0_steamdeck.tar.gz` from
[Releases](https://github.com/davkdavk/wave-race-64-recomp/releases/latest),
then in Desktop Mode:

```bash
mkdir -p ~/Games
tar -xzf waverace64-recomp_0.4.0_steamdeck.tar.gz -C ~/Games
~/Games/waverace64-recomp/run-waverace64.sh
```

To add it to Steam, choose **Games -> Add a Non-Steam Game to My Library -> Browse**
and select `~/Games/waverace64-recomp/run-waverace64.sh`.

Steam Deck notes:

- Put your ROM anywhere readable, such as `~/ROMs/` or an SD card.
- First launch opens the ROM picker; choose your USA Rev A dump.
- The package is portable and does not need `sudo` or pacman.
- If it fails, run `~/Games/waverace64-recomp/WaveRace64Recomp --version` from
  a terminal and report the output.

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
