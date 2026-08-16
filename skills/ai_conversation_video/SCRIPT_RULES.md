# Script Rules for AI Conversation Videos

## Goal

Write dialogue that is easy to animate, easy to edit, and enjoyable to watch on YouTube.

## Start with character roles

Before writing dialogue, define each character's function.

Examples:
- explainer / learner
- straight man / comic
- skeptic / enthusiast
- expert / beginner

Each character should have a different speaking rhythm and point of view.

## Keep lines animatable

Prefer relatively short lines over long paragraphs. Shorter units are easier to:

- generate as voice clips
- retime in editing
- animate separately
- insert reactions between
- replace if one line sounds unnatural

Long explanations should be broken into multiple turns when possible.

## Conversation should not sound like alternating essays

Avoid:

Character A: long complete explanation.
Character B: long complete explanation.
Character A: another long explanation.

Instead, use questions, reactions, interruptions and short acknowledgements to create exchange.

## Natural dialogue devices

Use selectively:

- 「え、それどういうこと？」
- 「たしかに。」
- 「いや、でも…」
- 「ちょっと待って。」
- 「つまり？」
- 「それは知らなかった。」

Do not overuse fillers. Give each character their own habits.

## YouTube Shorts structure

A useful starting structure for roughly 30–60 second videos:

1. **0–3 sec: Hook** — surprising statement, question, conflict or visual premise.
2. **3–15 sec: Setup** — establish what the characters are discussing.
3. **15–40 sec: Development** — exchange information, disagreement or comedy.
4. **40–55 sec: Payoff** — strongest discovery, joke, reversal or result.
5. **End: Button** — short final reaction, punchline or reason to watch another video.

Treat these as guidelines, not fixed timing rules.

## Longer YouTube videos

For longer videos, build in small resets so the conversation does not become visually flat:

- new question
- new example
- experiment or demonstration
- disagreement
- visual insert
- stronger reaction
- summary before moving to the next topic

## Voice direction in the script

When useful, attach simple performance notes to a line:

- calm
- excited
- confused
- whispering
- skeptical
- laughing lightly
- surprised

Avoid overly complex acting instructions that the TTS or animation tool cannot reliably reproduce.

## Plan reactions explicitly

Important lines should often have a listener reaction immediately afterward.

Example structure:

- A says reveal
- 0.3 sec pause
- B reaction close-up
- B short response
- A continues

This is often more convincing than letting the next long sentence begin immediately.

## Avoid uniformity

A script becomes synthetic when:

- every line has similar length
- every exchange follows question → complete answer
- all characters use the same vocabulary
- nobody changes emotion
- nobody interrupts or reacts

Vary line length and intent.

## Script delivery format

For production, organize dialogue into separate entries so audio can be generated individually.

Recommended fields:

- scene number
- speaker
- line
- emotion / delivery
- expected reaction
- optional shot suggestion

Example:

`S01 | A | え、それ本当にAIなの？ | surprised | B smiles | A close-up`

## Final script check

Before voice generation, read the dialogue aloud. If it feels awkward to say naturally, rewrite it before animation.
