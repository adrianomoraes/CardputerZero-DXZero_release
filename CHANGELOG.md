# Changelog — CardputerZero DX Zero

All notable changes to **CardputerZero DX Zero** (`dx-zero`) are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

*No unreleased changes yet.*

---

## [0.2.0] — 2026-11-21

**Package:** [`releases/v0.2.0/dx-zero_0.2.0-m5stack1_arm64.deb`](releases/v0.2.0/dx-zero_0.2.0-m5stack1_arm64.deb)
**Checksums:** [`releases/v0.2.0/SHA256SUMS.txt`](releases/v0.2.0/SHA256SUMS.txt)
**Target:** M5Stack CardputerZero (`arm64`, `APPLaunch`, LVGL 9.5, `320×170`)

### Added
- **5th Sequencer Sub-View: `SEQ → SMP` (Hybrid FM Drum Editor & On-Device WAV Sampler)**:
  - Each of the 8 `DRM` pads (`P1 KICK .. P8 PERC`) can now switch between **`FM SYNTH`** (editable FM drum synthesis) and **`WAV SAMPLE`** (16-bit PCM mono/stereo `.wav` sampler).
  - **Editable FM Drum Synthesis**: Per-pad **`FM Tune` (`-12..+12` semi)**, **`FM Decay` (`25%..250%`)**, **`FM Mod` (`0%..100%`)**, **`FM Noise` (`0%..100%`)**, **`Pad Gain` (`0%..150%`)**, and **`Choke Grp`** (e.g., Closed Hat cuts Open Hat).
  - **WAV Sample Loader & Waveform Editor**: Load external 16-bit `.wav` samples from `~/.config/cardputerzero-dxzero/samples/`, view a live **48-bar waveform graph**, dial in **`Start Cut`** (teal cursor) and **`End Cut`** (magenta cursor), and destructively **`Crop/Save`** with anti-click edge fades.
  - **On-Device Recording**:
    - **`Rec Synth`**: Resample up to 2.5 s directly from DX Zero's live FM + FX output into any drum pad (auto-trimmed, normalized, and saved as `synth_padX.wav`).
    - **`Rec Mic`**: Record up to 2.5 s from CardputerZero's built-in microphone (`ES8389-Audio`) or connected USB audio interface via ALSA capture with a live input level readout (saved as `mic_padX.wav`).
  - Full 8-pad hybrid kit persistence in `~/.config/cardputerzero-dxzero/drum_kit.cfg`.
- **Instant MIDI Panic (`Esc` Tap + `CC 120` / `CC 123`)**:
  - Tapping **`Esc`** immediately triggers **MIDI Panic (`All Notes Off`)** (while holding `Esc` > 600 ms still saves & exits cleanly to `APPLaunch`).
  - Added standard MIDI `CC 120` (*All Sound Off*) and `CC 123` (*All Notes Off*) support.
- **Explicit Drum Pad MIDI Channel & Base Note (`MID` Tab)**:
  - Added selectable **`Pad Ch`** (`Ch 10` default, `Ch 1..Ch 16`, `Any Ch`, or `Off (Keys)`) and **`Pad Base`** (`0..120`, default `36`) so drum pads stay completely isolated from keyboard notes on any controller (`DXZMIDI3` config).
- **Per-Track Volume Readout & Live Mixing in `SEQ → PLY`**:
  - Each of the 4 track lanes (`FM1`, `FM2`, `FM3`, `DRM`) now displays its independent volume (`V:xx%`), adjustable directly via `Z` / `C` while jamming.

### Fixed
- **Hanging / Stuck MIDI Notes**: Live keyboard `note_off` now releases matching live voices across all 3 FM tracks so switching tracks while holding keys never leaves a note hanging.
- **Top-Velocity FM Tone Artifact**: Capped modulator velocity gain at `1.0×` at velocity `127` with a soft FM modulation index ceiling (`1.85`) to eliminate Bessel sideband foldover/aliasing on hard key strikes, plus added a `10%` Aftertouch strike deadzone (default `aftertouch_depth` lowered to `35%`).
- **`Seq Mix` Volume on `DRM` Track**: Each drum voice now tracks `from_seq` and scales its live output directly by `(from_seq ? seq_mix : kbd_mix) * track_volume[3]` so `Seq Mix = 0%` cleanly silences sequenced drums while live pad/keyboard hits follow `Key Mix`.

---

## [0.1.1] — 2026-11-20

**Package:** [`releases/v0.1.1/dx-zero_0.1.1-m5stack1_arm64.deb`](releases/v0.1.1/dx-zero_0.1.1-m5stack1_arm64.deb)
**Checksums:** [`releases/v0.1.1/SHA256SUMS.txt`](releases/v0.1.1/SHA256SUMS.txt)
**Target:** M5Stack CardputerZero (`arm64`, `APPLaunch`, LVGL 9.5, `320×170`)

### Changed
- **Per-Instrument Expression Recording (`EXP` Tab)**:
  - Expression parameters (**Attack**, **Decay**, **Sustain**, **Release**, **Velocity Sensitivity & Curve**, **Aftertouch Depth & Destination**, **Mod Wheel Type / Wave / Speed / Amplitude**, and **Pitch Bend Range**) are now **recorded and recalled independently per instrument (per patch)** instead of being shared globally across all instruments.
  - Multi-track sequences (`FM1`, `FM2`, `FM3`) now render each track simultaneously with its own instrument's expression profile.
  - Per-bank expression profiles are automatically persisted alongside `.syx` banks under `~/.config/cardputerzero-dxzero/expr/*.dxzexp` while keeping `.syx` cartridges 100% standard 4104-byte Yamaha DX7 / Dexed compatible.
  - The `EXP` tab header badge now displays the active instrument's name so it is always clear which patch's expression is being edited.
- **Updated Default ADSR Envelope**:
  - Changed default ADSR values across all patches to **Attack `50%`**, **Decay `65%`**, **Sustain `75%`**, and **Release `50%`**.

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
