# Changelog — CardputerZero DX Zero

All notable changes to **CardputerZero DX Zero** (`dx-zero`) are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

*No unreleased changes yet.*

---

## [0.1.0] — 2026-11-20

**Package:** [`releases/v0.1.0/dx-zero_0.1.0-m5stack1_arm64.deb`](releases/v0.1.0/dx-zero_0.1.0-m5stack1_arm64.deb)
**Checksums:** [`releases/v0.1.0/SHA256SUMS.txt`](releases/v0.1.0/SHA256SUMS.txt)
**Target:** M5Stack CardputerZero (`arm64`, `APPLaunch`, LVGL 9.5, `320×170`)

### Added
- **6-Operator DX7-Compatible FM Synthesizer**:
  - Full 16-voice polyphony with quietest-voice stealing and anti-click crossfading.
  - All 32 classic Yamaha DX7 routing algorithms with 2-sample averaged self-feedback.
  - 32 built-in factory presets (`E.PIANO 1`, `SOLID BASS`, `BRASS 1`, `STRINGS 1`, `TUB BELLS`, `MARIMBA`, `JAZZ ORGAN`, `LATELY BSS`, `KOTO`, `VIBES`, `SPACE BELL`, etc.).
  - Standard 4104-byte Yamaha DX7 / Dexed `.syx` cartridge importer, inline QWERTY patch renamer, and on-device 32-voice custom `.syx` bank builder.
  - Built-in 8-voice FM drum synthesizer (`KICK`, `SNARE`, `CLAP`, `CHat`, `OHat`, `TOM-L`, `TOM-H`, `PERC`).
- **Dedicated Expression Tab (`EXP`)**:
  - Global ADSR (`Attack`, `Decay`, `Sustain`, `Release`), Velocity Sensitivity & Curve (`LIN / SFT / HRD / FIX`), Channel/Poly Aftertouch Depth & Destination, Sustain Pedal (`CC 64`), Pitch Bend Range (`±1..12` semitones), and multi-mode Expressive Mod Wheel LFO (`VIB / TREM / WAH / FILT / V+T / ALL`, 6 waveforms, `0.2–18.0 Hz`).
- **4-Track ORBIT + SLOOP Groovebox Sequencer (`SEQ`)**:
  - 4 multitimbral tracks (`FM1`, `FM2`, `FM3` with independent DX7 patches + `DRM` 8-part FM percussion) across 4 patterns (`A–D`) and up to 64 steps.
  - 4 dedicated views (`V` to cycle):
    - **`PLY`**: 4-track color-coded live performance view with real-time playheads, active sounding note/drum readouts, on-screen transport bar (`PLAY / REC / FILL / PAT / BPM`), and standalone CardputerZero playable mini-keyboard (`Q 2 W 3 E R 5 T 6 Y 7 U I` + `[` / `]` octave shift).
    - **`GRD`**: 16-step × 4-page visual step grid with live chord/drum overdubbing.
    - **`STP`**: Per-step SLOOP sheet supporting 4-note chords, Force (`GHOST / SOFT / NORM / HARD`), Gate/Tie (`1–16`), Ratchets (`1x–4x`), Microtiming Nudge (`-30..+30%`), Slide portamento, Fill conditions (`ALL / FILL / !FIL / 1:2 / 2:2 / 4:4`), Probability, and Parameter Locks.
    - **`CLP`**: ORBIT Lift/Drop clip editing (`1 / 4 / 8 / 16` steps), 8-level Undo/Redo, Section Chaining (`SINGLE / A>B / AA>BB / A>B>C>D`), per-track Vol/Mute/Len/Div, and 8 savable multi-track loop slots (`Loop 01–08`).
- **Master FX & Punch-In Effects (`FX`)**:
  - Cytomic TPT State-Variable Filter (`OFF / LP / HP / BP`), quadrature Stereo Chorus, Tempo-Synced Ping-Pong Delay, 4 OP-style Punch-In FX (`Stutter`, `Tape Stop`, `Bitcrush`, `HP Sweep`), and a C1-continuous soft-knee stereo bus limiter.
- **UI & Standalone Ergonomics**:
  - 7-tab sliding ribbon (`PLY | FM | EXP | SEQ | FX | AUD | MID`) with `<` / `>` scroll indicators and clean full-height layout.
  - Full CardputerZero keyboard navigation using `F` (Up), `X` (Down), `Z` (Left), `C` (Right) (with or without `Shift`) alongside standard arrow keys and `Tab` / `Shift+Tab`.
  - Custom DX Zero `APPLaunch` launcher icon (`100×100` RGBA).
- **Audio & Independent Mixer (`AUD`)**:
  - PipeWire sink discovery & live switching (`wpctl`) + raw ALSA `plughw:` bypass for both built-in CardputerZero audio (`ES8389-Audio`) and external class-compliant USB audio interfaces.
  - Independent **Sequencer Master Volume (`Seq Mix`)** and **Live Keyboard Master Volume (`Key Mix`)** (`0–140%`), hardware system volume (`0–100%`) with audible startup unmute, selectable sample rate (`44.1 / 48 kHz`) and buffer size (`128–1024` frames), dual Stereo `L`/`R` VU meters, and live `DSP:%` / XRun telemetry.
- **Universal USB MIDI & MIDI Learn (`MID`)**:
  - Hot-plug ALSA Sequencer MIDI input for any class-compliant USB MIDI controller.
  - Universal `L`-key MIDI Learn and 41 learnable targets (including `UI Nav Mode`, `NAV K1: Tab`, `NAV K2: Row`, `NAV K3: Val`, `NAV K4: Preset`, `Seq Mix Vol`, `Key Mix Vol`, and `Seq Fill`).
  - Selectable Drum Pad mode (`8x FM DRUMS`, `PAT + PUNCH`, `FM CHORDS`) and channel filter (`Ch10 Only`, `Any(36-43)`, `Off`).

### Performance & DSP Engineering
- Compiled natively for ARM64 Cortex-A53 with `-O3 -ffast-math -fno-math-errno -funroll-loops -mcpu=cortex-a53`.
- Branchless 32-bit unsigned integer phase accumulators + 4096-entry linearly interpolated sine LUT, 8-sample control-rate EG/LFO, and Padé `fast_tanh` in the master FX bus for crackle-free 16-voice sustained chords.

---

## Release Versioning Convention

Each release is published under `releases/vX.Y.Z/` containing:
- `dx-zero_X.Y.Z-m5stack1_arm64.deb` — Prebuilt ARM64 Debian package for M5Stack CardputerZero.
- `SHA256SUMS.txt` — Verified SHA-256 package checksum.
