# pet-asset-pipeline

An Agent Skill for the **dispatch → return → adjudicate → install** loop of game and character art assets.

It exists because of one expensive observation: **bad batches almost always come from a bad dispatch, not from a bad artist.** One dispatch told the executor to use a video frame as the first frame of an image-to-video run. That frame had already been through h264, so sharpness fell from 503 (native PNG) to 41. The entire batch was unusable for that single reason.

## What is inside

- **7-point pre-dispatch checklist** — first-frame sharpness, path verification, negation wording, numeric specs, acceptance-line ownership, naming, and normalization of pixel-count criteria.
- **Return review** — four fixed checks. "The executor says it passed" is not evidence.
- **Adjudication discipline** — never re-run the measurements just to confirm. Adjudication is a judgement, not a re-execution.
- **Install pipeline and baselines** — frame extraction, uniform scaling, anchor alignment, byte-exact write verification, and the sharpness red line measured inside character pixels rather than across the whole frame.
- **Caliber rules** — area and height criteria must declare their method. Largest-connected-component versus whole-bbox differed by 0.6 head-heights on the very same asset.

## The sharpness table that started all of this

| First frame source | Sharpness |
|---|---|
| Video screenshot | 41 |
| Native anchor PNG | 503 |

Input at 8% of the reference sharpness produced output at 31 against 413 in the previous batch.

## Install

```bash
npx skills add CatsMansion/pet-asset-pipeline
```

## Who it is for

Anyone running an outsource-style pipeline where another agent or another person produces art and you have to decide whether it ships. The numbers here come from a real sprite pack of 1372 frames across 24 actions.

MIT.
