# CardputerZero DX Zero — Complete Operating Manual

**Version:** `0.2.0` | **Platform:** M5Stack CardputerZero (`320×170` LVGL 9.5) | **Author:** Adriano Dias Moraes

> **[IMAGE PLACEHOLDER: `docs/images/manual-cover.jpg`]**
> *Replace with a close-up photo of CardputerZero running DX Zero on the `PLY` dashboard.*

---

## Table of Contents

1. [Getting Started & Hardware Connections](#1-getting-started--hardware-connections)
2. [Understanding the Screen & CardputerZero Keyboard Controls](#2-understanding-the-screen--cardputerzero-keyboard-controls)
3. [Tab 1: `PLY` — Live Performance Dashboard](#3-tab-1-ply--live-performance-dashboard)
4. [Tab 2: `FM` — 6-Operator DX7 Sound Design](#4-tab-2-fm--6-operator-dx7-sound-design)
5. [Tab 3: `EXP` — ADSR, Velocity, Aftertouch, Mod Wheel & Pitch Bend](#5-tab-3-exp--adsr-velocity-aftertouch-mod-wheel--pitch-bend)
6. [Tab 4: `SEQ` — Multi-Track ORBIT + SLOOP Groovebox Sequencer](#6-tab-4-seq--5-view-orbit--sloop-groovebox--hybrid-drum-sampler)
7. [Tab 5: `FX` — Filter, Chorus, Delay & Punch-In Effects](#7-tab-5-fx--filter-chorus-delay--punch-in-effects)
8. [Tab 6: `AUD` — Sound Cards, Seq/Key Mix, Volume & Stereo Diagnostics](#8-tab-6-aud--sound-cards-seqkey-mix-volume--stereo-diagnostics)
9. [Tab 7: `MID` — Presets, `.syx` Bank Builder, MIDI Setup & Learn](#9-tab-7-mid--presets-syx-bank-builder-midi-setup--learn)
10. [USB MIDI Controller & Rotary Control Guide](#10-usb-midi-controller--rotary-control-guide)
11. [Universal MIDI Learn (`L` Key) Walkthrough](#11-universal-midi-learn-l-key-walkthrough)
12. [Creating, Renaming & Organizing Custom 32-Voice DX7 Banks](#12-creating-renaming--organizing-custom-32-voice-dx7-banks)
13. [Built-In 32-Voice Factory Preset Directory](#13-built-in-32-voice-factory-preset-directory)
14. [Configuration Files & Backup Paths](#14-configuration-files--backup-paths)
15. [Troubleshooting](#15-troubleshooting)

---

## 1. Getting Started & Hardware Connections

DX Zero works in **three setups** — no external hardware is required to start making music:
1. **Standalone Pocket Mode**: Just your **M5Stack CardputerZero** using the built-in speaker or 3.5 mm headphone jack and the built-in 56-key mini-keyboard (`Q..I`).
2. **With Any USB MIDI Controller** *(optional)*: Plug any class-compliant USB MIDI keyboard, pad controller, or knob box into USB. DX Zero auto-scans ALSA Sequencer ports every ~2 seconds and connects automatically. Standard Sustain Pedals (`CC 64`), Pitch Bend, Mod Wheel (`CC 1`), and Aftertouch work immediately.
3. **With Any USB Audio Interface** *(optional)*: Plug any class-compliant USB DAC or audio interface (e.g., M-Audio M-Track Duo, Focusrite, Behringer, USB-C headphone dongle) into USB — use a powered USB hub if connecting both a USB audio interface and a bus-powered MIDI keyboard at once.
   - *Tip for USB audio interfaces with a Direct Monitor switch (e.g., M-Track Duo)*: set Direct Monitor to **`USB`**, turn up the headphone/output knob, and use a stereo **TRS** adapter rather than a mono TS plug.
4. **Launching DX Zero**:
   - Select **DX Zero** from the CardputerZero `APPLaunch` launcher.
   - On startup, DX Zero automatically verifies the hardware mixer and unmutes/raises system volume to `80%` if it was muted or below `15%`.

> **[IMAGE PLACEHOLDER: `docs/images/wiring-diagram.jpg`]**
> *Replace with a photo showing standalone CardputerZero usage or an optional USB hub with MIDI controller and USB audio interface.*

---

## 2. Understanding the Screen & CardputerZero Keyboard Controls

### Sliding 7-Tab Ribbon Header
```text
< [FM] [EXP] [SEQ] [FX] [AUD] >   >120   V4   (o)
```
- **7 Tabs on a 5-Tab Sliding Ribbon**: `PLY` → `FM` → `EXP` → `SEQ` → `FX` → `AUD` → `MID`.
  - Moving across the centered tab slides the ribbon left or right (`<` / `>` indicators appear when tabs are off-screen) until reaching the first (`PLY`) or last (`MID`) tab, after which the highlight moves directly to the edge tab.
- **Transport / Mode Badge**:
  - `[]120` (stopped at 120 BPM), `>120` (playing), `>120R` (live recording armed, red).
  - **`NAV`** (bright orange): Indicates **Alesis V61 Button 1 UI Navigation Mode** is toggled ON.
- **Voice Counter (`V0`..`V16`)**: Live count of active polyphonic FM voices (up to 16).
- **MIDI Activity LED**: Flashes cyan whenever MIDI data arrives.

### CardputerZero Matrix Keyboard Controls

DX Zero is designed to be operated comfortably right on the CardputerZero's 56-key matrix using the **`F / X / Z / C`** directional diamond (with or without `Shift`) as well as standard arrow keys:

| Key | Action |
|---|---|
| **`Tab`** / **`Shift + Tab`** | Slide forward / backward through all 7 tabs (`PLY..MID`) |
| **`F`** or **`↑`** *(with/without Shift)* | Move **Up** to the previous option/row |
| **`X`** or **`↓`** *(with/without Shift)* | Move **Down** to the next option/row |
| **`Z`** or **`←`** *(with/without Shift)* | **Left** / Decrease value (`Shift + Z` = fast coarse step on `FM`) |
| **`C`** or **`→`** *(with/without Shift)* | **Right** / Increase value (`Shift + C` = fast coarse step on `FM`) |
| **`Enter`** | Toggle step / Trigger action / Start inline text typing / Arm MIDI Learn |
| **`L`** | **Universal MIDI Learn** for whichever option is currently highlighted |
| **`Space`** | Play / Stop Sequencer (on `FM` tab: audition middle C note) |
| **`R`** | Toggle Live Polyphonic Chord & Drum Overdub Recording (`PLY` / `SEQ`) |
| **`V`** (`SEQ` tab) | Cycle all 5 Sequencer Sub-Views: **`PLY`** (Live) → **`GRD`** (Grid) → **`STP`** (Step Sheet) → **`CLP`** (Clips & Loops) → **`SMP`** (FM Drums & WAV Sampler) |
| **`Q 2 W 3 E R 5 T 6 Y 7 U I`** | **Playable CardputerZero Mini-Keyboard** (`PLY` tab & `SEQ → PLY` / `SMP`): chromatic octave `C..C+12` on `FM1–FM3`, or **8 Drum Pads** (`Q..I`) on `DRM`! |
| **`[` / `]`** | Shift CardputerZero Mini-Keyboard octave Down / Up (`C2..C6`) |
| **`T`** / **`P`** / **`G`** (`SEQ` tab) | Cycle Track (`FM1–FM3/DRM`) / Cycle Pattern (`A–D`) / Toggle **`FILL`** |
| **`1`–`4`** (`PLY`) / **`1`–`6`** (`FM`) / **`1`–`8`** (`SEQ → SMP`) | Quick-select Track (`FM1–DRM`), Operator (`OP1–OP6`), or Drum Pad (`P1–P8`) |
| **`F1` – `F4`** | Toggle OP-style Punch-In FX (`Stutter`, `Tape Stop`, `Bitcrush`, `HP Sweep`) |
| **`Esc` (tap)** | **MIDI Panic (`All Notes Off`)** — immediately silences any stuck notes (or cancels active MIDI Learn / text input) |
| **`Esc` (hold > 600 ms)** | Save configuration and exit cleanly back to `APPLaunch` |

*(When typing a patch or bank name in `Rename Pat` / `New Bank`, `Z / C / F / X` type letters normally until you press `Enter` or `Esc`.)*

---

## 3. Tab 1: `PLY` — Live Performance Dashboard

> **[IMAGE PLACEHOLDER: `docs/images/manual-ply.png`]**
> *Replace with a screenshot of the `PLY` tab showing a selected patch, active knob bars, and waveform scope.*

The **`PLY`** tab is your main performance view. Every row on the left panel can be navigated with `Up` / `Down`, edited with `Left` / `Right`, and MIDI-Learned with `L`:

- **Row 0 — Track Strip (`FM1`, `FM2`, `FM3`, `DRM`)**: Press `1`–`4` or `Left`/`Right` to select which track your keyboard plays. Each FM track holds its own independent DX7 preset!
- **Row 1 — Active Preset (`01 E.PIANO 1` .. `32 SPACE BELL`)**: Highlighted by default — press `Left`/`Right` to browse all 32 voices in the current bank.
- **Row 2 — Bank & Algorithm**: Press `Left`/`Right` (or `[` / `]`) to switch between `DXZ FACTORY` and your custom `.syx` banks.
- **Rows 3–6 — Live Macro Meters**:
  - `BRT`: FM Brightness (scales all modulator operator levels in real time).
  - `REL`: Global Envelope Release tail.
  - `CUT`: Master State-Variable Filter cutoff.
  - `FX`: Master Chorus + Delay wet mix.
- **Right Panel**: Live 24-bar **Oscilloscope**, **Peak VU Meter**, Octave/Arp readout (`A` cycles Arpeggiator modes), and **`2×2` Punch-In FX status pills** (`STUT`, `TAPE`, `CRSH`, `HP`).
- **Built-in QWERTY Mini-Keyboard**: On `PLY`, keys `Z S X D C V G B H N J M ,` play a chromatic octave right from the CardputerZero keyboard! Use `-` / `=` to adjust BPM.

---

## 4. Tab 2: `FM` — 6-Operator DX7 Sound Design

> **[IMAGE PLACEHOLDER: `docs/images/manual-fm.png`]**
> *Replace with a screenshot of the `FM` tab showing the 6 operator badges, DX7 parameters, and 4-bar operator EG graph.*

The **`FM`** tab is dedicated cleanly to authentic 6-operator Yamaha DX7 programming.

### Top Bar: Operator Selector (`1`–`6`)
- Press keys **`1`–`6`** to select **OP1–OP6**.
- Each badge shows **`C`** (teal = Carrier, outputs audio) or **`M`** (amber = Modulator, shapes timbre) according to the active DX7 algorithm.
- Press **`M`** to mute/unmute the selected operator while auditioning (`Space` plays C4).

### Deep DX7 6-Operator Parameters
- **`Algor`** (`1–32`): Selects any of the 32 classic Yamaha DX7 operator routing topologies.
- **`Feedbk`** (`0–7`): Self-modulation feedback intensity (great for saw/brass/grit).
- **`OP Lvl`** (`0–99`): Selected operator output level (volume for carriers, harmonic brightness for modulators).
- **`Coarse`** (`0–31`, `0 = 0.5×`), **`Fine`** (`0–99`), **`Detune`** (`-7..+7`, `0.06 Hz`/step).
- **`EG R1–R4`** (`0–99`) & **`EG L1–L3`** (`0–99`): Authentic DX7 per-operator 4-stage envelope rates & levels.
- **`OP Vel`** (`0–7`): Per-operator velocity sensitivity.
- **`LFO Sp`** (`0–99`): Patch LFO speed.

*Tip: Hold **`Shift + Z / C`** (or `Shift + ← / →`) on `FM` for fast coarse jumps! While on **`FM`** (with `NAV` OFF), Alesis V61 Knobs `K1–K4` control **`OP Lvl`, `Coarse`, `EG R1`, `EG R4`** directly.*

---

## 5. Tab 3: `EXP` — ADSR, Velocity, Aftertouch, Mod Wheel & Pitch Bend

> **[IMAGE PLACEHOLDER: `docs/images/manual-exp.png`]**
> *Replace with a screenshot of the `EXP` tab showing the global ADSR bars, Velocity/Aftertouch/Mod Wheel rows, and live expression telemetry.*

All real-time performance expression controls live on their own dedicated **`EXP`** tab and are **recorded per instrument (per patch)** — switching between instruments preserves each sound's own ADSR, Velocity, Aftertouch, Mod Wheel, and Pitch Bend settings (saved automatically in `~/.config/cardputerzero-dxzero/expr/`):

| Row | Parameter | Range / Options | Description |
|---|---|---|---|
| 0 | **`Attack`** | `0–100%` (default `50%`) | Per-instrument envelope attack speed |
| 1 | **`Decay`** | `0–100%` (default `65%`) | Per-instrument envelope decay speed (`R2`/`R3`) |
| 2 | **`Sustain`** | `0–100%` (default `75%`) | Per-instrument sustain level (`L3`) |
| 3 | **`Release`** | `0–100%` (default `50%`) | Per-instrument release tail (`R4`) |
| 4 | **`VelSens`** | `0–100%` | Global keyboard velocity dynamics (default `85%`, up to `-28 dB` amplitude + FM brightness range) |
| 5 | **`VelCurv`** | `LIN / SFT / HRD / FIX` | Velocity response curve |
| 6 | **`AT Dep`** | `0–100%` | Channel / Poly Aftertouch modulation depth |
| 7 | **`AT Dst`** | `V+B / VIB / BRT / CUT` | Aftertouch destination (Vibrato+Brightness, Vibrato, Brightness, or Filter Cutoff) |
| 8 | **`ModType`** | `VIB / TREM / WAH / FILT / V+T / ALL` | **Expressive Mod Wheel destination**: Pitch Vibrato, Amplitude Tremolo, FM Timbre Wah, Master Filter Wobble, Vibrato+Tremolo, or Full Expressive |
| 9 | **`ModWave`** | `SIN / TRI / SAW- / SAW+ / SQR / S&H` | Mod Wheel LFO waveform |
| 10 | **`ModSpd`** | `0.2–18.0 Hz` | Mod Wheel LFO speed |
| 11 | **`ModAmp`** | `0–100%` | Mod Wheel amplitude/depth (zero effect when wheel is at `0`) |
| 12 | **`BendRng`** | `±1 .. ±12` | Pitch Bend wheel range in semitones (default `±2`) |

*Tip: While on **`EXP`** (with `NAV` OFF), Alesis V61 Knobs `K1–K4` control **`Attack`, `Decay`, `Sustain`, `Release`** directly! The right panel shows a live 4-bar ADSR visualizer plus Mod Wheel, Aftertouch, and Sustain Pedal (`PED:ON/off`) indicators.*

---

## 6. Tab 4: `SEQ` — 5-View ORBIT + SLOOP Groovebox & Hybrid Drum Sampler

> **[IMAGE PLACEHOLDER: `docs/images/manual-seq.png`]**
> *Replace with a screenshot of the `SEQ` tab showing the 4-track color `PLY` view, live playheads, and on-screen transport controls.*

Press **`V`** on the **`SEQ`** tab to cycle through five dedicated groovebox sub-views: **`PLY`** → **`GRD`** → **`STP`** → **`CLP`** → **`SMP`**.

### Sub-View 1: `PLY` (4-Track Live Color Performance & Per-Track Mixer)
Designed so you can perform, mix, and live-record multi-track grooves **using only the CardputerZero keyboard** (or alongside any USB MIDI controller):
- **4 Color-Coded Live Track Lanes**:
  - **`FM1`** (**DX Teal**), **`FM2`** (**OP Cyan**), **`FM3`** (**Neon Magenta**), **`DRM`** (**OP Orange**).
  - Each lane shows its 16-step live playhead strip (auto-following pages on 32/64-step tracks) plus a **live readout on the right** showing the active sounding note/chord or drum hits (`C4+2`, `K+H`, `SNR`), per-track volume (`V:85%`), or `MUTE`.
- **Per-Track Mix & Mute**:
  - Use **`F` / `X`** to highlight any track (`FM1–DRM`): **`Z` / `C`** adjusts that track's independent volume (`0–150%`), and **`Enter`** toggles **Mute**.
- **Playing & Live-Recording Standalone**:
  - Highlight any track (`FM1–DRM`) and play **`Q 2 W 3 E R 5 T 6 Y 7 U I`** (`[` / `]` shifts octave `C2..C6`) — on **`DRM`**, **`Q W E R T Y U I`** plays all **8 Drum Pads** (`Kick..Perc`)!
  - Move **`X`** down to Row 4 (the **On-Screen Transport Bar**: `> PLAY` | `o REC` | `FILL` | `PAT:A` | `120BPM`), pick a control with **`Z` / `C`**, and press **`Enter`** (or press **`Space`** anytime for Play/Stop and **`-`/`=`** for BPM). Turn **`o REC`** ON and play while the loop runs to overdub straight into the active track!

### Sub-View 2: `GRD` (64-Step Visual Grid)
- **4 Tracks (`T`)**: `FM1`, `FM2`, `FM3` (each with its own independent DX7 patch & expression profile!) + `DRM` (8-part hybrid FM/Sample percussion).
- **4 Patterns (`P`)**: `A`–`D` (64 steps across 4 pages of 16 steps).
- Use **`Z` / `C`** to move the step cursor, **`Enter`** to toggle steps ON/OFF, **`F` / `X`** to shift note pitch (or select drum pad `1–8` on `DRM`), **`G`** to toggle live **`FILL`**, **`R`** to arm live overdub, and **`Backspace`** to clear the current track.

### Sub-View 3: `STP` (SLOOP Per-Step Sheet)
Edit every expressive detail of the selected step (`F`/`X` to pick row, `Z`/`C` to adjust, `Enter` to toggle):
- **`Step On`** / **`Root Note`** (or 8-Drum hit toggles on `DRM`)
- **`Chord`**: Cycles `Mono`, `Major`, `Minor`, `Maj7`, `Min7` (or keeps custom 4-note live-recorded chords!)
- **`Force / Vel`**: 4 SLOOP dynamic levels (`GHOST` 36, `SOFT` 68, `NORM` 100, `HARD` 127)
- **`Gate / Tie`**: `1..16` steps for staccato hits or legato ties
- **`Ratchet`**: `1x..4x` rapid sub-step retriggers
- **`Nudge`**: `-30%..+30%` microtiming groove shift
- **`Slide / Gld`**: Portamento pitch glide into the step
- **`Fill Cond`**: `ALL`, `FILL` (only when Fill active), `!FIL`, `1:2`, `2:2`, `4:4`
- **`Prob`**: `10%..100%` trig probability
- **`PLock Brt`** / **`PLock Cut`**: Per-step Parameter Locks!

### Sub-View 4: `CLP` (ORBIT Lift/Drop Clips, Mix, Chain & Savable Loops)
- **`ORBIT Lift`**: Choose clip length (`1 / 4 / 8 / 16` steps), press **`Enter`** to copy (or **`Shift+Enter`** to cut) — chords, ties, force, ratchets, nudge, slide, fill conditions, and P-locks all travel with the clip!
- **`ORBIT Drop`**: Press **`Enter`** to drop the lifted clip at the current cursor step on ANY track or pattern.
- **`Undo / Redo`**: **`Enter`** undoes the last edit; **`Shift+Enter`** redoes (8-level history).
- **`Seq Chain`**: `SINGLE`, `A>B`, `AA>BB`, or `A>B>C>D` automatic section chaining.
- **`Track Vol` / `Track Mute` / `Track Len (4–64)` / `Step Div (1/8..1/16T)`**.
- **`Loop Slot (01–08)` → `Save Loop` / `Load Loop`**: Saves & recalls your entire 4-track multitimbral loop (including per-track patches & Seq/Key mix) under `~/.config/cardputerzero-dxzero/loops/`!

### Sub-View 5: `SMP` (Hybrid FM Drum Editor & On-Device WAV Sampler)

> **[IMAGE PLACEHOLDER: `docs/images/manual-smp.png`]**
> *Replace with a screenshot of `SEQ → SMP` showing the 48-bar live waveform graph, Start/End trim markers, and FM/WAV parameters.*

Each of the **8 Drum Pads (`P1 KICK .. P8 PERC`)** can run as either an **editable FM Drum Synth** or a **16-bit PCM WAV Sampler** — press **`1–8`** or **`Q W E R T Y U I`** (or **`Space`**) anytime inside `SMP` to audition pads while sculpting!

#### Mode A: `FM SYNTH` (Editable 8-Voice FM Drum Synthesis)
Select **`Source` → `FM SYNTH`** to shape the built-in percussion synthesizer for the selected pad (the top graph previews the envelope & FM modulation shape live):
- **`FM Tune`** (`-12 .. +12` semi): Pitch-tune kicks, snares, hats, toms, and metallic perc.
- **`FM Decay`** (`25% .. 250%`): Shorten for tight 808 clicks or lengthen for booming sub kicks & open cymbals.
- **`FM Mod`** (`0% .. 100%`): Dial FM modulator index for punch, metallic clang, or gritty percussion.
- **`FM Noise`** (`0% .. 100%`): Blend crisp high-passed noise snap/sizzle.
- **`Pad Gain`** (`0% .. 150%`) & **`Choke Grp`** (`ON/OFF` — e.g. Closed Hat cuts Open Hat).

#### Mode B: `WAV SAMPLE` (Import, Graph-Trim, Resample Synth & Record Mic)
1. **Load External `.wav` Samples**:
   - Copy any 16-bit PCM mono or stereo `.wav` files (up to 3 seconds each) to `~/.config/cardputerzero-dxzero/samples/` via `scp`.
   - Select **`Source` → `WAV SAMPLE`**, highlight **`WAV File`**, and use **`Z` / `C`** to browse & audition your samples immediately!
2. **Record Directly From DX Zero's FM Synth (`Rec Synth`)**:
   - Highlight **`Rec Synth`** and press **`Enter`** — the header turns red (`REC SYNTH...`).
   - Play any DX7 note, chord, or FX sound on your MIDI keyboard (or CardputerZero). Press **`Enter`** again to stop early (or let it auto-finish at 2.5 s).
   - DX Zero automatically trims leading/trailing silence, normalizes cleanly, assigns the sample to the pad, and saves it as `~/.config/cardputerzero-dxzero/samples/synth_padX.wav`!
3. **Record From Microphone / USB Audio Input (`Rec Mic`)**:
   - Highlight **`Rec Mic`** and press **`Enter`** — the waveform header displays the live input level (`REC MIC xx%`) from CardputerZero's built-in mic (`ES8389-Audio`) or your connected USB audio interface.
   - Beatbox, tap, or sample an external instrument, then press **`Enter`** to stop — auto-trimmed, normalized, loaded onto the pad, and saved as `mic_padX.wav`!
4. **Visual Waveform Cutting & Cropping**:
   - Adjust **`Start Cut`** (teal vertical cursor) and **`End Cut`** (magenta vertical cursor) with **`Z` / `C`** while watching the 48-bar waveform graph highlight the active region in bright orange.
   - Highlight **`Crop/Save`** and press **`Enter`** to destructively crop the sample to `[Start..End]` (with automatic anti-click edge fades) and save the updated `.wav` file!
   - Shape **`Pitch`** (`-12..+12` semi) and **`Pad Gain`** (`0..150%`), then press **`S`** on `MID` (or exit cleanly) to save your entire 8-pad hybrid kit to `drum_kit.cfg`.

### Independent Sequencer vs Live Keyboard Volume Mix (`AUD` Tab)
To jam live on top of a running 4-track loop (including **both FM tracks and `DRM`**), open **`AUD`** (or turn **`K3`/`K4`** while on **`SEQ`**) to independently balance:
- **`Seq Mix` (`0–140%`)**: Master volume for all sequenced `FM1–FM3` and `DRM` tracks (`0%` = silent).
- **`Key Mix` (`0–140%`)**: Master volume for live keyboard and live drum pad playing.

---

## 7. Tab 5: `FX` — Filter, Chorus, Delay & Punch-In Effects

> **[IMAGE PLACEHOLDER: `docs/images/manual-fx.png`]**
> *Replace with a screenshot of the `FX` tab showing filter sliders and Punch-In FX rows.*

- **Master State-Variable Filter**: `Filter Mode` (`OFF / LP / HP / BP`), `Cutoff`, `Resonance`.
- **Stereo Chorus**: `Chorus Mix`, `Chorus Dep` (quadrature stereo modulation).
- **Tempo-Synced Ping-Pong Delay**: `Delay Mix`, `Delay Fdbk`, `Delay Div` (`1/16`, `1/8`, `3/16` dotted-8th, `1/4`).
- **Master Bus**: `FX Wet Mix` (global wet macro), `Master Vol` (`0–120%` into the smooth C1 stereo bus limiter).
- **OP-Style Punch-In FX** (`Enter` or `F1`–`F4` from any tab):
  - **`PNCH Stut`**: Tempo-synced 1/16th beat-repeat stutter loop.
  - **`PNCH Tape`**: Vinyl/tape slowdown pitch drop to zero.
  - **`PNCH Crush`**: Lo-fi sample-rate & bit-depth decimation.
  - **`PNCH HP`**: Rising resonant DJ high-pass sweep.

---

## 8. Tab 6: `AUD` — Sound Cards, Seq/Key Mix, Volume & Stereo Diagnostics

> **[IMAGE PLACEHOLDER: `docs/images/manual-aud.png`]**
> *Replace with a screenshot of the `AUD` tab showing PipeWire USB selection, Seq/Key Mix bars, dual `L`/`R` VU meters, and `DSP:%` readout.*

| Row | Option | Function |
|---|---|---|
| 0 | **`Sys Volume`** | Real Linux PipeWire + ALSA hardware playback volume (`0–100%`) |
| 1 | **`Synth Gain`** | Internal FM/FX master output level (`0–120%`) |
| 2 | **`Seq Mix`** | Independent **Sequencer Master Volume** (`0–140%`) for all 4 sequenced tracks |
| 3 | **`Key Mix`** | Independent **Live Keyboard Master Volume** (`0–140%`) for jamming over a loop |
| 4 | **`Audio Mute`** | Quick hardware mute / unmute (`Enter` or `M`) |
| 5 | **`Sound Card`** | Switch live between `[DEF] Auto (PipeWire)`, `[USB] PCM2900C Audio CODEC` (M-Track Duo), `[INT] Built-in Audio Stereo` (ES8389), or raw ALSA `[RAW]` bypass |
| 6 | **`Driver`** | Read-only display of the active backend/sink driver (e.g., `PipeWire Sink #63 (USB-Audio)`) |
| 7 | **`Sample Rate`** | Toggle `44100 Hz` / `48000 Hz` |
| 8 | **`Buffer Size`** | Select `128`, `256`, `512` (recommended default), or `1024` frames |
| 9 | **`Test Chime`** | Press `Enter` to play a test FM chord immediately |
| 10 | **`Scan Audio`** | Press `Enter` to detect newly connected USB audio interfaces |

- **Bottom Telemetry Bar**: Displays independent **`L`** (teal) and **`R`** (cyan) stereo peak meters plus live **`DSP:xx%`** audio-thread CPU load and **`X:0`** XRun counter.

---

## 9. Tab 7: `MID` — Presets, `.syx` Bank Builder, MIDI Setup & Learn

> **[IMAGE PLACEHOLDER: `docs/images/manual-mid.png`]**
> *Replace with a screenshot of the `MID` tab showing Preset/Bank management, Rename/Save/New Bank, and MIDI monitor.*

| Row | Option | Function |
|---|---|---|
| 0 | **`DX7 Preset`** | Browse all 32 presets in the active bank (`Z`/`C` or `←`/`→`) |
| 1 | **`DX7 Bank`** | Switch between `DXZ FACTORY` and any `.syx` banks found on disk |
| 2 | **`Rename Pat`** | Press `Enter` to type a new 10-character DX7 name for the active patch |
| 3 | **`Save Patch`** | Choose destination `Slot 01–32` (`Z`/`C`), press `Enter` to save to `.syx` |
| 4 | **`New Bank`** | Press `Enter` to name & create a brand-new 32-voice `.syx` bank |
| 5 | **`MIDI In`** | Choose `ALL` (plug & play) or lock to a specific ALSA MIDI port |
| 6 | **`Pad Mode`** | `8x FM DRUMS`, `PAT + PUNCH` (Pads 1–4 launch Patterns A–D; Pads 5–8 trigger Punch FX), or `FM CHORDS` (8 jazz/pop chords) |
| 7 | **`Pad Ch`** | Explicit Drum Pad MIDI Channel: **`Ch 10`** (default — keeps Ch 1 keys clean!), **`Ch 1..Ch 16`**, **`Any Ch`**, or **`Off (Keys)`** |
| 8 | **`Pad Base`** | Base MIDI note for the 8 pads (`0..120`, default `36` = C2) — move outside your keyboard range if your pads share Ch 1! |
| 9 | **`MIDI Learn`** | Select any of 41 MIDI targets (`Z`/`C`, including **`NAV K1: Tab`**, **`NAV K2: Row`**, **`NAV K3: Val`**, **`NAV K4: Preset`**), press `Enter` to arm learn |
| 10 | **`Reset MIDI`** | Press `Enter` to restore default MIDI CC mappings |
| 11 | **`Save All`** | Press `Enter` (or `S`) to save Audio, MIDI Learn, Drum Kit, Expressions, and Sequencer patterns |

---

## 10. USB MIDI Controller & Rotary Control Guide

> **[IMAGE PLACEHOLDER: `docs/images/midi-controller-map.jpg`]**
> *Replace with an annotated photo of a USB MIDI controller showing rotary knobs, buttons, pads, and pitch/mod wheels.*

Any class-compliant USB MIDI controller works out-of-the-box. DX Zero ships with sensible defaults (tested on 4-knob / 4-button / 8-pad controllers such as the Alesis V61), and **every knob, button, and rotary nav control can be remapped in seconds** via **`MID` → `MIDI Learn`** or by pressing **`L`** on any parameter.

### Default MIDI Map
| Controller Input | MIDI Message | Default Function |
|---|---|---|
| **Keyboard Keys** | Ch 1 Notes | Play active FM track with full velocity dynamics |
| **Pitch Bend Wheel** | Pitch Bend | Smooth `±2` semitones (configurable `±1..12` in `EXP`) |
| **Modulation Wheel** | `CC 1` | Expressive Mod Wheel LFO (`ModType / ModWave / ModSpd / ModAmp` in `EXP`) |
| **Sustain Pedal** | `CC 64` | Full 16-voice damper hold & release |
| **Drum Pads (1–8)** | Ch 10 Notes `36–43` | 8 FM Drums (`Kick..Perc`) / Pattern Launch / Chords |
| **Button 1** | `CC 48` (Toggle) | **Toggle `UI NAV` Mode** (ON = `NAV`, OFF = Play) |
| **Button 2** | `CC 49` | Sequencer **Play / Stop** |
| **Button 3** | `CC 50` | Sequencer **Live Record Arm** |
| **Button 4** | `CC 51` | **Punch-In FX: Stutter** |

### Rotary Knobs `K1–K4` (`CC 20–23` Default — Fully Learnable in `MID`)

| Mode / Visible Tab | `K1` (`CC 20`) | `K2` (`CC 21`) | `K3` (`CC 22`) | `K4` (`CC 23`) |
|---|---|---|---|---|
| **UI `NAV` Mode ON** | **Slide Tabs (`PLY..MID`)** | **Select Row / Option** | **Full-Range Value Edit** | **Scroll Presets (`01–32`)** |
| `NAV` OFF on `PLY`/`AUD`/`MID` | Brightness (FM) | Env Release | Filter Cutoff | FX Wet Mix |
| `NAV` OFF on `FM` | Selected OP Level | OP Coarse Ratio | OP EG Rate 1 | OP EG Rate 4 |
| `NAV` OFF on `EXP` | Global Attack | Global Decay | Global Sustain | Global Release |
| `NAV` OFF on `SEQ` | BPM (`40–240`) | Swing (`0–75%`) | **Seq Mix Volume** | **Key Mix Volume** |
| `NAV` OFF on `FX` | Filter Cutoff | Filter Resonance | Chorus Mix | Delay Feedback |

*Using a different controller? Open **`MID` → `MIDI Learn`** and bind **`NAV K1: Tab`**, **`NAV K2: Row`**, **`NAV K3: Val`**, **`NAV K4: Preset`**, or **`UI Nav Mode`** to any knob or button on your controller, then press **`S`** to save!*

---

## 11. Universal MIDI Learn (`L` Key) Walkthrough

Want to assign ANY parameter (such as `Mod Speed`, `Seq Mix`, `Key Mix`, `Seq Fill`, `System Volume`, `OP2 Level`, `Algorithm`, or `UI Nav Mode` if your controller buttons use different CCs)?
1. Navigate to the option you want using `F`/`X` (or `↑`/`↓`) on **any tab** (or select any of the 37 targets on **`MIDI Learn`** in the **`MID`** tab).
2. Press **`L`** (or `Enter` on the `MIDI Learn` row). The footer turns amber: `LEARN [<Target>]: Move knob/btn...`
3. Turn a knob or press a button/pad on your MIDI controller. The footer confirms `LEARNED CC xx -> <Target>`.
4. Press **`S`** on the **`MID`** tab (or exit cleanly by holding `Esc`) to save your custom mapping permanently.

---

## 12. Creating, Renaming & Organizing Custom 32-Voice DX7 Banks

### Scenario A: Editing & Saving a Modified Factory Sound
1. Pick a starting sound on `PLY` (e.g., `01 E.PIANO 1`).
2. Sculpt it in `FM` (adjust `Attack`, `Release`, `Algorithm`, `Feedback`, `OP1–OP6` levels/ratios, `ModType`, etc.).
3. Switch to `MID` → highlight **`Rename Pat`** → press **`Enter`** → type `MY RHODES` → press **`Enter`**.
4. Highlight **`Save Patch`** → choose `Slot 01` (or any slot `01–32`) → press **`Enter`**.
   - Because `DXZ FACTORY` is read-only, DX Zero automatically clones it into `~/.config/cardputerzero-dxzero/banks/USER_01.syx` and writes your new sound into `Slot 01`.

### Scenario B: Building a Brand-New 32-Instrument Bank From Scratch
1. Open **`MID`** → highlight **`New Bank`** → press **`Enter`**.
2. Type a name like `GIG_SET` → press **`Enter`**.
3. DX Zero creates `~/.config/cardputerzero-dxzero/banks/GIG_SET.syx` (32 clean `INIT 01..32` slots) and activates it.
4. Sculpt sounds, rename them, and save them into slots `01–32`. Because the output is a standard **4104-byte Yamaha DX7 `.syx`** file, you can copy it off the CardputerZero and load it directly in **Dexed** or a hardware **Yamaha DX7**!

### Scenario C: Importing External Dexed / Yamaha DX7 `.syx` Banks
Copy any `.syx` files onto your CardputerZero:
```bash
scp *.syx adrianomoraes@<cardputer-ip>:~/.config/cardputerzero-dxzero/banks/
```
Restart DX Zero — every `.syx` file appears under **`DX7 Bank`**!

---

## 13. Built-In 32-Voice Factory Preset Directory

| # | Name | Alg | Character | # | Name | Alg | Character |
|---|---|---|---|---|---|---|---|
| 01 | `E.PIANO 1` | 5 | Classic DX7 Rhodes tines | 17 | `E.PIANO 2` | 5 | Bright bell-tine electric piano |
| 02 | `SOLID BASS` | 16 | Punchy 80s FM bass | 18 | `DX PIANO 1` | 5 | Percussive FM acoustic grand |
| 03 | `BRASS 1` | 22 | Warm analog-style FM brass | 19 | `SYNTHBRASS` | 22 | Snappy 80s poly synth brass |
| 04 | `STRINGS 1` | 5 | Detuned lush string ensemble | 20 | `LATELY BSS` | 16 | Rubbery house / TX81Z bass |
| 05 | `TUB BELLS` | 5 | Inharmonic tubular bells | 21 | `VIBES` | 5 | Metallic vibraphone with tremolo |
| 06 | `MARIMBA` | 5 | Woody mallet percussion | 22 | `KALIMBA` | 5 | Warm thumb piano pluck |
| 07 | `JAZZ ORGAN` | 32 | 6-drawbar additive organ | 23 | `STEEL DRUM` | 5 | Caribbean FM steel pan |
| 08 | `SYN LEAD` | 1 | Cutting solo FM lead | 24 | `CHURCH ORG` | 32 | Full additive pipe organ |
| 09 | `WARM PAD` | 5 | Slow glass ambient pad | 25 | `KOTO` | 7 | Sharp plucked Japanese string |
| 10 | `SLAP BASS` | 16 | Funky percussive slap bass | 26 | `GLASS BELL` | 5 | Shimmering crystal bell |
| 11 | `CLAVINET` | 7 | Funky bright clavinet | 27 | `ACID FM` | 1 | Squelchy resonant FM bass |
| 12 | `FM FLUTE` | 29 | Breathy chiff + pure flute | 28 | `CHOIR PAD` | 5 | Ethereal vocal formant pad |
| 13 | `HARPSICH` | 5 | Bright baroque harpsichord | 29 | `RETRO CHIP` | 5 | 8-bit chiptune square lead |
| 14 | `PLUCK FM` | 5 | Modern synthwave FM pluck | 30 | `ACCORDION` | 5 | Reedy detuned folk accordion |
| 15 | `SUB BASS` | 5 | Deep fundamental sub bass | 31 | `FM GUITAR` | 5 | Clean chorus-ready FM guitar |
| 16 | `SCI-FI FX` | 1 | Evolving S&H metallic FX | 32 | `SPACE BELL` | 5 | Deep cinematic shimmer bell |

---

## 14. Configuration Files & Backup Paths

All user data is stored cleanly under `~/.config/cardputerzero-dxzero/`:
- `~/.config/cardputerzero-dxzero/banks/*.syx` — Your custom & imported 32-voice DX7 `.syx` banks.
- `~/.config/cardputerzero-dxzero/expr/*.dxzexp` — Per-instrument Expression profiles (`ADSR`, `Vel`, `AT`, `ModWheel`, `BendRng`) recorded per bank.
- `~/.config/cardputerzero-dxzero/samples/*.wav` — Imported, synth-resampled (`synth_padX.wav`), and mic-recorded (`mic_padX.wav`) 16-bit PCM drum samples.
- `~/.config/cardputerzero-dxzero/drum_kit.cfg` — Saved 8-pad hybrid FM Drum & WAV Sampler kit configuration.
- `~/.config/cardputerzero-dxzero/loops/loop_01..08.dxzloop` & `.meta` — Saved programmable multi-track ORBIT+SLOOP loops.
- `~/.config/cardputerzero-dxzero/midi_map.cfg` — Saved MIDI Learn & Drum Pad Channel/Base bindings (`DXZMIDI3` format).
- `~/.config/cardputerzero-dxzero/patterns.cfg` — Saved 4-pattern × 4-track × 64-step sequencer data (`DXZSEQ2` format).
- `~/.config/cardputerzero-dxzero/engine.cfg` — Last audio output device, sample rate, buffer size, and track patch slots.

---

## 15. Troubleshooting

- **No sound at startup or after plugging in a USB interface**:
  - Open **`AUD`** → press **`Enter`** on **`Scan Audio`** → select your `[USB]` or `[INT]` PipeWire sink on **`Sound Card`** → raise **`Sys Volume`** (`80–100%`) → press **`Enter`** on **`Test Chime`**.
  - On the **M-Audio M-Track Duo**, confirm **Direct Monitor** is set to **`USB`** and the **Headphone/Output** knob is turned up.
- **Audio only heard in Left headphone ear**:
  - Check the dual **`L`** and **`R`** meters at the bottom of **`AUD`**. If both bars move equally, check your 3.5 mm-to-1/4" headphone adapter (ensure it is a stereo **TRS** adapter and not a mono TS plug or misaligned 4-ring TRRS mic headset).
- **Bottom 8 keys trigger drums instead of notes**:
  - Open **`MID`** and verify **`Pad Ch`** is set to **`Ch10 Only`** (default).
- **Toggle buttons on MIDI controller don't respond**:
  - Open **`MID`**, press your controller button, and read the `MIDI: Ch1 CC xx = 127` monitor line at the bottom. Highlight **`MIDI Learn`**, select `UI Nav Mode` / `Seq Play/Stop` / `Seq Live Rec` / `Punch: Stutter`, press **`Enter`**, press your button, and press **`S`** to save.
