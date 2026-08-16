# AI Conversation Video Production Workflow

## Goal

Produce a repeatable AI-character conversation video from idea to YouTube-ready export.

## 1. Define the format

Decide before production:

- YouTube Shorts or standard YouTube
- approximate final duration
- number of characters
- horizontal or vertical frame
- whether the scene is dialogue-only or includes demonstrations / cutaways

Recommended delivery targets:

- Shorts: 1080 x 1920, 9:16
- Standard YouTube: 1920 x 1080, 16:9

## 2. Define characters

For each character, record:

- role in the conversation
- personality
- speaking style
- voice
- common reactions
- visual identity
- whether they are mainly speaker, learner, straight man, comic, expert, etc.

Keep these traits consistent across episodes.

## 3. Write the script

Use `SCRIPT_RULES.md`.

Break the script into short, editable dialogue units. Add emotion and reaction notes only where they help production.

Before moving on, read the script aloud and remove lines that sound like written prose rather than spoken conversation.

## 4. Generate voice audio

Generate audio by character and preferably by dialogue line or small group of lines.

Benefits:

- easier timing adjustments
- easier regeneration of one bad line
- easier insertion of reaction pauses
- easier sync with animation

Keep filenames systematic, for example:

- `S01_A_001.wav`
- `S01_B_002.wav`

If using generated voices, keep voice settings consistent for the same character unless an emotional change is intentional.

## 5. Prepare animation assets

Choose the animation method based on the shot.

### MotionPNGTuber

Use for efficient talking-character shots with repeatable base motion and mouth shapes.

Prepare according to `../motionpngtuber/SKILL.md`, including the looping base video and required mouth assets.

### Hedra or similar tools

Use for shots requiring more generated body or facial performance from an image + audio input.

Do not force every shot through the same animation tool. Choose based on what the scene needs.

## 6. Generate character performances

For each speaking section:

- create the speaking animation
- create or preserve a usable listening / idle state
- check lip sync
- check expression
- check whether body motion is too repetitive

If the tool produces stronger motion than necessary, prefer shorter shots and hide artifacts through editing rather than using a long continuous take.

## 7. Build the dialogue edit

In the video editor:

1. Place voice clips in conversational order.
2. Adjust pauses manually.
3. Add speaking character shots.
4. Add listener reactions.
5. Add two-shots where useful.
6. Remove dead time that does not feel intentional.

Do not use identical pause lengths throughout.

## 8. Add shot variation

Use camera changes to support meaning.

Possible pattern:

- opening two-shot
- speaker close-up
- listener reaction
- return to speaker
- two-shot for shared moment
- tighter shot for punchline

The camera should react to the conversation, not change randomly.

## 9. Add subtitles

Subtitles should improve comprehension and rhythm.

Recommendations:

- keep text short enough to read quickly
- emphasize only important words
- avoid filling the entire screen with text
- time subtitle changes to spoken rhythm rather than arbitrary intervals

For entertainment-focused videos, visual emphasis can be added to the key word or punchline.

## 10. Add sound effects and BGM

Use sound design to support moments, not cover weak timing.

Good uses:

- reveal
- surprise
- awkward pause
- punchline
- transition

Keep dialogue intelligible above BGM.

## 11. Naturalness review

Use `NATURAL_CONVERSATION.md`.

Check:

- does the listener move or react?
- are eye lines believable?
- are there varied pauses?
- are loops obvious?
- is one character frozen while the other speaks?
- do emotions change when the meaning changes?

## 12. Watch the full video without editing

Do one uninterrupted playback before export.

Mark only moments where you instinctively feel:

- slow
- unnatural
- too busy
- confusing
- repetitive

Fix those first. Do not endlessly polish parts the viewer will not notice.

## 13. Export

Use a high-quality master appropriate for YouTube.

After export, confirm:

- video opens correctly
- audio is present
- no black or missing-character sections
- aspect ratio is correct
- subtitles remain within safe viewing area
- first few seconds work without explanation

## Recommended principle

Build the pipeline so individual steps can be replaced. For example, MotionPNGTuber can handle efficient dialogue shots while another animation tool handles expressive moments. The workflow should survive changes in individual AI tools.
