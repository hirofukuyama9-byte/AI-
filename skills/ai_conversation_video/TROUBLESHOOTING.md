# AI Conversation Video Troubleshooting

## Character is visible but feels lifeless

Possible causes:

- only the mouth is moving
- no idle movement
- no blinking
- no listener reaction
- camera remains fixed too long

Fixes:

- add subtle idle or breathing motion
- add irregular blinking
- insert nods or small head movement
- cut to the listening character after important lines
- shorten long static shots

## Character disappears or video shows only audio

Possible causes:

- source video failed to render correctly
- wrong codec or alpha handling
- character layer disabled in the editor
- export uses an unsupported format
- generated file is corrupted or incomplete

Fixes:

1. Open the generated animation file by itself before editing.
2. Confirm picture and audio are both present.
3. Re-encode the video to a standard editing format if necessary.
4. Confirm the character layer is visible and above the background.
5. Export a short test section before rendering the full video.

## Video cannot be played or imported

Possible causes:

- unsupported codec
- incomplete file
- variable or unusual encoding
- browser preview limitation

Fixes:

- test playback in another player
- transcode to a broadly supported H.264 MP4 for delivery/testing
- use an editing-friendly codec during production when appropriate
- verify the file duration and size are not zero or abnormally small

## Lip sync feels late or early

Possible causes:

- audio offset
- animation processing delay
- mouth thresholds are poorly calibrated
- edited audio differs from the audio used to generate motion

Fixes:

- compare the raw animation with the original audio
- shift audio/video by a few frames in the editor
- recalibrate MotionPNGTuber when using that pipeline
- regenerate animation if the audio was changed substantially after generation

## Mouth movement is too exaggerated

Possible causes:

- mouth shape assets differ too much in size or position
- calibration is too sensitive
- every phoneme produces a large visual jump

Fixes:

- align mouth PNGs to the same canvas and anchor position
- reduce visual differences between neighboring mouth shapes
- recalibrate thresholds
- review at normal playback speed rather than frame-by-frame only

## Mouth position jumps between shapes

Likely cause:

The mouth PNG assets are not aligned to the same reference point.

Fix:

Use identical canvas dimensions and ensure the center/anchor of the lips occupies the same location in every shape asset.

## Body motion looks repetitive

Possible causes:

- loop is too short
- motion has an obvious beginning/end gesture
- same loop is used for every emotional state

Fixes:

- use a longer seamless idle loop
- choose subtle motion without a strong identifiable event
- cut away before repetition becomes obvious
- prepare multiple idle/performance loops where practical

## Two characters do not feel like they are in the same scene

Possible causes:

- mismatched eye lines
- inconsistent scale
- different lighting/color temperature
- incompatible camera angles
- no shared reaction timing

Fixes:

- adjust framing so each character appears to face the other
- normalize approximate head/eye height
- color-match in the editor
- use a shared background or visual frame
- insert response pauses and reaction shots

## Dialogue feels robotic even though voices sound good

Possible causes:

- every line starts immediately
- lines are too long and complete
- no acknowledgement or interruption
- every pause has identical length

Fixes:

- apply `SCRIPT_RULES.md`
- add varied short pauses
- split long lines into conversational turns
- add occasional short reactions or interjections
- vary emotional delivery

## Scene feels slow

Fix in this order:

1. shorten unnecessary silence
2. shorten long lines
3. add a reaction cut or visual change
4. remove repeated information
5. increase music/SE activity only if appropriate

Do not use constant camera movement to hide weak dialogue.

## Scene feels too busy

Possible causes:

- both characters move strongly at the same time
- subtitles are oversized or constantly animated
- too many sound effects
- excessive cuts

Fixes:

- make the listener's motion smaller
- reserve strong subtitle emphasis for key words
- remove sound effects that do not add meaning
- let important reactions hold for a moment

## Final export check

If something goes wrong in the final video, test the pipeline in stages:

1. source voice audio
2. generated character animation
3. editor timeline playback
4. short test export
5. full export

Find the first stage where the problem appears. Fix that stage rather than repeatedly exporting the whole project.
