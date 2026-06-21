# Lavalink Server — Local Custom Filters Plugin 🎧

Your Lavalink server is pre-configured with a private, high-fidelity **Custom Filters Plugin** featuring **130 presets and advanced digital signal processing (DSP) controls**.

The compiled plugin `.jar` has been placed directly in your `plugins/` directory:
📂 `plugins/lavalink-custom-filters-plugin-1.0.0.jar`

Since the `.jar` is located in the local `plugins/` folder, **no remote configuration is needed** in `application.yml`. Lavalink loads it automatically on startup.

---

## 🚀 Bot Developer Integration Guide

Bot developers can control these filters dynamically using Lavalink player updates under the custom filter name `"custom-filters"`.

### 1. Preset Mode (1–130)
To apply a preset, send the `"preset"` field. 
Example JSON payload:
```json
{
  "filters": {
    "custom-filters": {
      "preset": "8d-audio"
    }
  }
}
```

### 2. Manual Custom DSP Controls
To manually configure advanced filters, omit `preset` and configure the following parameters:

```json
{
  "filters": {
    "custom-filters": {
      // 3-Band Parametric EQ
      "peqEnabled": true,
      "peqLowFreq": 150.0,
      "peqLowGainDb": 6.0,
      "peqMidFreq": 1000.0,
      "peqMidQ": 0.5,
      "peqMidGainDb": -3.0,
      "peqHighFreq": 8000.0,
      "peqHighGainDb": 4.0,

      // Dynamics Compressor & Noise Gate
      "compressorEnabled": true,
      "compressorThresholdDb": -16.0,
      "compressorRatio": 4.0,
      "compressorAttackMs": 15.0,
      "compressorReleaseMs": 80.0,
      "compressorMakeupGainDb": 3.0,
      "gateEnabled": true,
      "gateThresholdDb": -45.0,

      // Reverb
      "reverbEnabled": true,
      "reverbRoomSize": 0.75,
      "reverbDamp": 0.25,
      "reverbWetMix": 0.35,

      // 3D Binaural Auto-Rotator (8D Audio with ITD shadow delays)
      "spatialMode": "THREE_D_ROTATOR",
      "spatialRotationRateHz": 0.25
    }
  }
}
```

---

## 📊 Complete Presets Reference (1–130)

| Index / Name | Category | Description |
|---|---|---|
| 1 / `bass-boost` | Equalization | Raises low frequencies (shelving filter, gain boost below 120Hz) |
| 2 / `treble-boost` | Equalization | Raises high frequencies (shelving filter, gain boost above 5kHz) |
| 3 / `mid-boost` | Equalization | Raises midrange (peaking/bell filter at 1.5kHz) |
| 4 / `vocal-boost` | Equalization | Emphasizes vocal presence range (bell filter at 2.2kHz) |
| 5 / `bass-cut` | Equalization | Removes low-end rumble (high-pass at 80Hz) |
| 6 / `treble-cut` | Equalization | Softens harsh highs (low-pass at 8kHz) |
| 7 / `loudness-contour` | Equalization | Fletcher-Munson curve emulation (shelving boost) |
| 8 / `smile-eq` | Equalization | Boosted bass/treble + scooped mids (3-band parametric EQ) |
| 9 / `v-shape-eq` | Equalization | Exaggerated scooped mids (steep 3-band parametric EQ) |
| 10 / `telephone` | Equalization | Narrow bandpass filter (300Hz–3.4kHz) |
| 11 / `radio` | Equalization | AM-radio style bandpass + tube saturation |
| 12 / `warm-tone` | Equalization | Bass shelf boost + tape saturation warmth |
| 13 / `bright-tone` | Equalization | High-mid/treble emphasis (high shelf boost) |
| 14 / `scoop-eq` | Equalization | Mid-range cut peaking filter at 800Hz |
| 15 / `presence-boost` | Equalization | 6.5kHz lift for voice clarity |
| 16 / `air-boost` | Equalization | 12kHz+ high shelf shimmer lift |
| 17 / `sub-boost` | Equalization | Deep sub-bass low shelf boost at 50Hz |
| 18 / `de-esser` | Equalization | Dynamic notch compressor targeting sibilance (6.5kHz) |
| 19 / `compressor` | Dynamics | Dynamic range compression (threshold/ratio/attack/release) |
| 20 / `limiter` | Dynamics | Prevents clipping with high ratio ceiling |
| 21 / `expander` | Dynamics | Dynamic range expansion (ratio < 1.0) |
| 22 / `noise-gate` | Dynamics | Silences noise floor below -45dB |
| 23 / `multiband-compressor` | Dynamics | Compresses bands with focus peaking at 1kHz |
| 24 / `loudness-normalizer` | Dynamics | Dynamics levelling with +6dB makeup gain |
| 25 / `auto-gain` | Dynamics | Slow automatic gain control (AGC) |
| 26 / `transient-shaper` | Dynamics | Emphasizes note attacks using rapid compression time constants |
| 27 / `soft-clipper` | Dynamics | Hyperbolic tangent soft saturation curve |
| 28 / `brickwall-limiter` | Dynamics | 100:1 ratio hard ceiling limiter |
| 29 / `sidechain-compressor` / `ducking` | Dynamics | Tempo-synced gain ducking simulation |
| 30 / `pumping-compressor` | Dynamics | Fast attack and release pumping dynamics |
| 31 / `chorus` | Modulation | Multiple delayed, LFO pitch-modulated signals |
| 32 / `flanger` | Modulation | Sweeping metallic comb filter effect |
| 33 / `phaser` | Modulation | Sweeping phase cancellation using cascaded Allpass filters |
| 34 / `ring-modulator` | Modulation | Multiplication with high frequency carrier tone |
| 35 / `auto-pan` | Modulation | Panning moving left/right automatically |
| 36 / `auto-wah` | Modulation | Dynamic envelope-follower filter sweep |
| 37 / `tremolo` | Modulation | Low frequency amplitude (volume) modulation |
| 38 / `slow-gear` | Modulation | Attack transient volume fade-in |
| 39 / `frequency-shifter` | Modulation | Ring modulator carrier frequency shifter |
| 40 / `univibe` | Modulation | Rotating-speaker phase sweep + tube warmth |
| 41 / `overdrive` | Distortion | Soft clipping waveshaping distortion |
| 42 / `fuzz` | Distortion | Hard clipping high-gain distortion |
| 43 / `bitcrusher` | Distortion | Bit depth resolution reduction (Lo-fi digital grit) |
| 44 / `sample-rate-reducer` | Distortion | Downsampling without low-pass (aliasing grit) |
| 45 / `tape-saturation` | Distortion | Analog tape-style soft compression curve |
| 46 / `tube-saturation` | Distortion | Asymmetric tube harmonics waveshaping |
| 47 / `wavefolder` | Distortion | Waveform folding waveshaping |
| 48 / `clipper-hard` | Distortion | Abrupt waveform hard limiting clipping |
| 49 / `lo-fi-crush` | Distortion | Combined bitcrush + sample-rate reduction |
| 50 / `vinyl-crackle` | Distortion | Procedural analog record pops and crackles |
| 51 / `tape-hiss` | Distortion | Procedural high-frequency white-noise tape hiss |
| 52 / `am-radio-distortion` | Distortion | Bandpass EQ + hard clipping distortion |
| 53 / `stereo-widener` | Spatial | Exaggerates stereo image (mid-side processing) |
| 54 / `mono-merge` | Spatial | Collapses stereo to mono |
| 55 / `8d-audio` | Spatial | Head-Shadow + ITD 3D space auto-rotation |
| 56 / `binaural-pan` | Spatial | ITD-based rotating binaural pan |
| 57 / `haas-effect` | Spatial | Haas effect sub-millisecond delay widening |
| 58 / `surround-simulator` | Spatial | Multi-tap short delay + room reverb surround feel |
| 59 / `center-channel-extractor` | Spatial | Mono collapse + vocals mid-boost |
| 60 / `stereo-flip` | Spatial | Swaps left and right channels |
| 61 / `depth-reverb-pan` | Spatial | Panning rotator with dynamic reverb blend |
| 62 / `pitch-shift` | Pitch/Time | Alters pitch without changing speed |
| 63 / `formant-shift` | Pitch/Time | Formant-preserving pitch shift emulation |
| 64 / `harmonizer` | Pitch/Time | Major third pitch shifted harmony voice mix |
| 65 / `autotune-style` | Pitch/Time | Micro pitch shift + tube saturation |
| 66 / `chipmunk-voice` | Pitch/Time | Fast high pitch shift (+6 semitones) |
| 67 / `demon-voice` | Pitch/Time | Heavy deep pitch shift (-6 semitones) |
| 68 / `helium-voice` | Pitch/Time | Pitch up + high shelf boost |
| 69 / `robot-voice` | Pitch/Time | Pitch down + Ring Modulator robot tone |
| 70 / `nightcore` | Pitch/Time | High pitch shift (+3 semitones) |
| 71 / `daycore` | Pitch/Time | Deep pitch shift (-3 semitones) |
| 72 / `slowed-reverb` | Pitch/Time | Pitch down (-2 semitones) + wet room reverb |
| 73 / `vaporwave` | Pitch/Time | Pitch down (-3.5 semitones) + delay + cathedral reverb |
| 74 / `time-stretch` | Pitch/Time | Speed change time stretch simulation (+1 semitone) |
| 75 / `reverb-room` | Reverb | Small room simulation |
| 76 / `reverb-hall` | Reverb | Large hall spatial simulation |
| 77 / `reverb-plate` | Reverb | Bright, dense studio plate simulation |
| 78 / `reverb-cathedral` | Reverb | Cathedral space with extremely long decay |
| 79 / `gated-reverb` | Reverb | Long decay reverb abruptly cut off by noise gate |
| 80 / `echo-slap` | Reverb | 80ms slapback echo repeat |
| 81 / `echo-multitap` | Reverb | Rythmic delay repeats |
| 82 / `ping-pong-delay` | Reverb | Cross-channel left/right delay feedback |
| 83 / `tape-echo` | Reverb | Echo with tape saturation in feedback loop |
| 84 / `reverse-reverb` | Reverb | Pre-delay reverb simulation |
| 85 / `shimmer-reverb` | Reverb | Reverb with octave pitch-shift feedback |
| 86 / `notch-filter` | Filters | Notch reject band filter at 1kHz |
| 87 / `comb-filter` | Filters | Comb filtering delay line at 2ms |
| 88 / `all-pass-filter` | Filters | Flat amplitude phase shift filter |
| 89 / `resonant-low-pass` | Filters | Lowpass with high resonance peak at 1.2kHz |
| 90 / `resonant-high-pass` | Filters | Highpass with high resonance peak at 300Hz |
| 91 / `bandpass-sweep` | Filters | LFO-modulated bandpass sweep filter |
| 92 / `talk-box` | Filters | Vocal talk-box formant peak filter |
| 93 / `vocoder` | Filters | Ring modulator carrier bandpass |
| 94 / `underwater-effect` | Lo-Fi | Lowpass muffled filter + slow tremolo wobble |
| 95 / `walkie-talkie` | Lo-Fi | Bandpass filter + compression + bitcrush |
| 96 / `megaphone` | Lo-Fi | Narrow bandpass + high overdrive distortion |
| 97 / `old-record` | Lo-Fi | Bandpass EQ + procedural vinyl crackles |
| 98 / `cassette-tape` | Lo-Fi | Tape saturation + procedural hiss noise + chorus wobble |
| 99 / `8-bit` | Lo-Fi | Heavy bitcrusher (3-bit) + downsampler (GameBoy style) |
| 100 / `am-shortwave-radio` | Lo-Fi | Bandpass + overdrive + ring mod noise |
| 101 / `broken-speaker` | Lo-Fi | Fuzz distortion + random gating dropouts |
| 102 / `police-radio` | Lo-Fi | Bandpass + hard limiting + clipping |
| 103 / `earrape` | Novelty | Extreme distortion + compressor makeup gain boost |
| 104 / `glitch-stutter` | Novelty | Fast 18Hz stutter gating effect |
| 105 / `reverse-audio` | Novelty | Reversing echo loop illusion |
| 106 / `granular-freeze` | Novelty | 95% feedback short delay line freeze |
| 107 / `alien-voice` | Novelty | Pitch down + ring mod vocal modulation |
| 108 / `hellcore` | Novelty | Pitch down + extreme distortion earrape |
| 109 / `cursed-bass-boost` | Novelty | 16dB low shelf bass boost + overdrive distortion |
| 110 / `wormhole` | Novelty | Slow flanger sweep + cathedral reverb + pitch down |
| 111 / `stadium-reverb` | Reverb | Arena-scale long reverb + wide stereo panning |
| 112 / `classroom-reverb` | Reverb | Medium reflective classroom room space |
| 113 / `canyon-echo` | Reverb | Long 800ms echo delay + cathedral reverb |
| 114 / `outer-space` | Novelty | Pitch down + cathedral reverb + space ring modulator |
| 115 / `broken-record` | Novelty | Tremolo gating + pitch down drift |
| 116 / `car-audio` | Equalization | Heavy cabin mid-bass boost (120Hz) + compression |
| 117 / `club-dance` | Spatial | Sub-bass low shelf boost + pumping compression + widening |
| 118 / `sub-woofer` | Equalization | Lowpass filter isolating sub-bass (<80Hz) |
| 119 / `super-nightcore` | Speed/Pitch | Sped up pitch (+3.5 semitones) + vocal mid boost |
| 120 / `lofi-study` | Lo-Fi | Tape saturation + lofi lowpass (2.5kHz) + tape hiss |
| 121 / `dj-filter-sweep` | Filters | Sweeping flanger drop effect |
| 122 / `retro-arcade` | Lo-Fi | Bitcrush + ring mod retro sound |
| 123 / `radioactive` | Distortion | Extreme overdrive + ring modulator noise |
| 124 / `dark-ambient` | Reverb/Pitch | Pitch down (-4 semitones) + dark tremolo + room reverb |
| 125 / `ghostly` | Reverb/Pitch | Octave pitch up (+12 semitones) + auto-pan + cathedral reverb |
| 126 / `ufo` | Modulation | Panning rotator + ring modulator |
| 127 / `screamer` | Distortion | High drive overdrive + vocal mids peak boost |
| 128 / `heaven` | Reverb/Pitch | Octave pitch up (+12 semitones) + high shelf air boost + reverb |
| 129 / `custom-lofi-vibe` | Lo-Fi | Downsampler + lowpass filter |
| 130 / `dj-muffled-drop` | Filters | 400Hz lowpass filter muffling effect |
