# MotionPNGTuber Skill

## Purpose
This skill stores practical knowledge for using MotionPNGTuber, a video-based real-time lip-sync system positioned between a simple PNGTuber and Live2D.

Primary reference:
- https://github.com/rotejin/MotionPNGTuber#-detailed-reference

Use this skill when answering questions about:
- MotionPNGTuber setup and installation
- Creating mouth sprites
- Mouth tracking and calibration
- Generating mouthless loop videos
- Real-time microphone lip sync
- Mouth color correction
- Emotion detection
- Browser output
- Troubleshooting MotionPNGTuber
- Using MotionPNGTuber on macOS, Windows, or Ubuntu

## Core Concept
MotionPNGTuber uses a short looping MP4 as the character base and overlays mouth sprites in real time based on microphone input. This allows continuous motions such as hair sway and clothing movement without requiring a full Live2D rig.

Typical workflow:
1. Prepare a short looping MP4.
2. Prepare or generate mouth PNG sprites.
3. Analyze the video and detect mouth position.
4. Calibrate mouth placement.
5. Check placement with the lightweight visual preview.
6. Generate a mouthless video.
7. Run real-time lip sync.
8. Correct mouth color if necessary.

## Requirements
- Python 3.10
- `uv` package manager

Quick start:
```bash
uv sync
uv run python mouth_track_gui.py
```

Sample assets are under:
```text
assets/asmr_tomari/
```

## Input Assets

### Loop video
Use a short looping `.mp4`, typically a few seconds long.

Recommendations:
- Keep the face visible.
- Avoid the face being covered by hands, hair, objects, or extreme motion.
- A clean frontal or near-frontal face generally makes tracking easier.

### Mouth sprites
Recommended mouth sprite set:

```text
open.png    mouth open
closed.png  mouth closed
half.png    half-open mouth
e.png       custom E-like shape
u.png       custom U-like shape
```

Requirements:
- PNG with transparency
- Around 128 px width is a practical reference size
- `open.png` alone can sometimes work as a fallback, but all five sprites are recommended for stability

## Main GUI Workflow
Launch:
```bash
uv run python mouth_track_gui.py
```

Normal sequence:
1. Create mouth PNG sprites if none exist.
2. Select the loop video.
3. Select the mouth sprite folder.
4. Run `(1) Analyze → Calibrate`.
5. Adjust mouth placement and confirm.
6. Run `Visual check (lightweight)`.
7. Run `(2) Generate mouthless video`.
8. Run `(3) Live run`.
9. If the mouth color does not match the face, use auto color blending or manual sliders.

Default behavior in the 2026-04-10 developer build:
- Shadow blending: ON
- HUD display: OFF

## Calibration Controls

### Mouse
- Left drag: move mouth
- Scroll wheel: zoom
- Right drag: rotate

### Keyboard
- Arrow keys: fine movement
- `W/A/S/D`: alternative fine movement, useful when arrow keys do not work correctly on Mac
- `+/-`: zoom
- `z/x`: rotate
- `Space` or `Enter`: confirm
- `Esc`: cancel

On macOS, `+/-` may be more reliable than the mouse wheel for zooming.

## Mouth Placement Margin Factor
The mouth placement margin factor controls the detected mouth crop/placement size during Analyze → Calibrate.

Default:
```text
2.1
```

Adjustment guide:
- Mouth PNG too small or edges clipped → increase to about `2.3–2.6`
- Mouth too large or includes jaw/cheeks → decrease to about `1.8–2.0`

Recommended workflow:
1. Analyze and calibrate at `2.1`.
2. Use Visual check to compare around `1.9 / 2.1 / 2.3`.
3. Apply the best value.
4. Re-run Analyze → Calibrate.
5. Generate the mouthless video.

Important: changing the margin factor requires Analyze → Calibrate to be run again.

## Lightweight Visual Check
Use this before full mouthless-video export to avoid repeatedly performing heavy processing.

It can reuse:
```text
mouth_track.npz
mouth_track_calibrated.npz
```

If `open.png` exists, the mouth overlay can also be previewed.

Controls:
- `1/2/3`: select margin-factor candidate
- `r/f`: increase/decrease mouth erase range
- `a/d`: previous/next frame
- `[/]`: jump 10 frames
- `Space`: play/pause
- `Enter`: apply selected settings
- `Esc` or `q`: close without applying

## Mouth PNG Color Correction
Mouth sprites may look pasted on if their color differs from the underlying face video.

Adjustable parameters include:
- brightness
- saturation
- warm/cool color temperature
- correction intensity
- edge priority
- edge correction width
- color-difference highlight preview

Recommended process:
1. Start Live run.
2. Optionally increase color-difference highlight.
3. Press Auto color blending.
4. Fine-tune the sliders manually.

The correction is weighted more strongly near the mouth sprite edges so skin boundaries can blend naturally.

Auto color blending:
- compares the base video's mouth area with colored edge areas of the mouth PNG
- ignores transparent areas
- is available during Live run
- automatically saves changes

## Emotion Detection
MotionPNGTuber can estimate voice emotion and switch expressions.

Typical states:
- neutral: default
- happy: higher pitch / brighter tone
- angry: strong voice / high energy
- sad: quieter / lower tone
- excited: very high energy

Presets:
- Stable: slower expression changes; good for streaming
- Standard: balanced
- Responsive: faster reaction; suitable for gaming or high-energy content

## Browser Output
After generating the mouthless video, MotionPNGTuber can export:

```text
mouth_track.json
*_mouthless_h264.mp4
```

`mouth_track.json` is the main browser-facing mouth-track data.

The H.264 file is generated when `ffmpeg` is available and is recommended for browser/player use.

For AudioWorklet-based browser players, opening directly with `file://` may block microphone or worklet access. Serve the directory locally instead:

```bash
python -m http.server 8000
```

Then open:
```text
http://localhost:8000
```

## Command-Line Workflow

Face tracking:
```bash
uv run python auto_mouth_track_v2.py --video loop.mp4 --out mouth_track.npz
```

Calibration:
```bash
uv run python calibrate_mouth_track.py --video loop.mp4 --track mouth_track.npz --sprite open.png
```

Generate mouthless video:
```bash
uv run python auto_erase_mouth.py --video loop.mp4 --track mouth_track_calibrated.npz --out loop_mouthless.mp4
```

Real-time lip sync:
```bash
uv run python loop_lipsync_runtime_patched_emotion_auto.py \
  --loop-video loop_mouthless.mp4 \
  --mouth-dir mouth_dir/Char \
  --track mouth_track_calibrated.npz
```

Mouth sprite extraction:
```bash
uv run python mouth_sprite_extractor.py --video loop.mp4 --out mouth/
```

## macOS Setup
MotionPNGTuber's macOS support is experimental and intended for Apple Silicon.

Typical setup:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
cp pyproject.toml pyproject.win.toml
cp pyproject.macos.toml pyproject.toml
uv venv .venv && uv sync
uv pip install pip setuptools wheel torch==2.0.1 torchvision==0.15.2
```

Then build `xtcocotools` from source and build `mmcv-full` from source, followed by:

```bash
uv pip install --no-build-isolation anime-face-detector
uv pip install mmdet==2.28.0 mmpose==0.29.0
```

Launch:
```bash
.venv/bin/python mouth_track_gui.py
```

Important:
- Do not delete the `deps/` directory after setup.
- Calibration zoom may work better with `+/-` than the mouse wheel.

## Troubleshooting

### Mouth position is wrong
1. Try recalibration first.
2. Use Visual check.
3. Compare margin-factor values.
4. Adjust the margin factor only if necessary.
5. Re-run Analyze → Calibrate after changing the factor.

### Black smudge after mouth erase
Try disabling Shadow blending.

### `uv sync` fails
```bash
uv cache clean
uv sync
```

### CUDA is not detected
```bash
uv run python -c "import torch; print(torch.cuda.is_available())"
```

### Analysis stops on RTX 50-series or newer GPUs
The Torch/CUDA build may not match the GPU architecture.

The GUI uses `--device auto`, which tries CUDA first and can fall back to CPU.

If analysis still fails:
```bash
uv run python auto_mouth_track_v2.py ... --device cpu
```

Check the logs for CUDA compatibility messages.

### Analysis appears frozen
Initial analysis can be slow, especially with long videos or when processing falls back to CPU. Check progress and logs before assuming the application has stopped.

### Mouth PNG creation immediately shows `Analysis error`
A script-path bug affecting the detector was fixed on 2026-04-13. If the error remains after updating, inspect the log and verify that:

```text
face_track_anime_detector.py
```

exists in the project.

## Key Project Files
Useful files when debugging or extending the project:

```text
mouth_track_gui.py
mouth_sprite_extractor_gui.py
mouth_sprite_extractor.py
auto_mouth_track_v2.py
calibrate_mouth_track.py
auto_erase_mouth.py
erase_mouth_offline.py
loop_lipsync_runtime_patched_emotion_auto.py
face_track_anime_detector.py
convert_npz_to_json.py
```

Shared package:
```text
motionpngtuber/
```

Important modules include:
- `mouth_color_adjust.py`
- `lipsync_core.py`
- `image_io.py`
- `auto_crop_estimator.py`
- `mouth_auto_classifier.py`
- `mouth_feature_analyzer.py`
- `realtime_emotion_audio.py`
- `workflow_validation.py`

## Practical Guidance for Future Answers
When helping with MotionPNGTuber:

1. Prefer the GUI workflow for beginners.
2. Use the CLI when debugging, automating, or isolating errors.
3. For mouth alignment problems, recalibrate before changing advanced settings.
4. Use Visual check before regenerating the full mouthless video.
5. Treat margin-factor changes as analysis-stage changes that require re-analysis.
6. For unnatural mouth appearance, test color blending before rebuilding assets.
7. On Mac, account for experimental support and dependency-build complexity.
8. If performance suddenly drops, check whether CUDA fell back to CPU.
9. For browser playback, prefer exported H.264 plus `mouth_track.json` and serve locally rather than using `file://`.
10. When project behavior differs from this document, check the latest upstream MotionPNGTuber README because the project is still a developer preview and APIs/features may change.

## Source Status
This knowledge was compiled from the MotionPNGTuber upstream README / Detailed Reference available in August 2026. The upstream project identifies itself as a developer preview, so future answers should verify the upstream repository when version-specific accuracy matters.
