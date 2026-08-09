# Creative briefs — Harmonia Facial Pro

Ready-to-run briefs derived from the landing page copy in `index.html`. Nothing here has been
sent to the Arcads API — these are the inputs for when you do.

| File | What it holds |
|---|---|
| `01-angles-and-hooks.md` | The 6 core angles, with pt-BR hooks, primary text, and headlines |
| `02-avatars.md` | Avatar specs for the audience, and the character-sheet prompts to build them |
| `03-image-ads.md` | Template picks from the 37-template library, with variables filled for this offer |
| `04-ugc-video-scripts.md` | Six UGC scripts with shot direction and model routing |

## How to run one

1. Make sure setup is done — `./scripts/setup.sh` (needs your Arcads key), then confirm with
   `./scripts/check-arcads-env.sh`.
2. Read `MASTER_CONTEXT.md` for voice and the compliance constraints. They are not optional
   on this offer.
3. For image ads: read `shared/skills/image-ad-prompting/OVERVIEW.md`, check the aspect-ratio
   table in `shared/skills/image-ad-prompting/prompting/prompt-library.md` against your
   backend, then invoke `chatgpt-image-ad` or `nano-banana-image-ad` with the filled prompt.
4. For video: build the avatar still first (`02-avatars.md`), get it approved, *then* animate.
   Stills are cheap, video is not.
5. Publishing to Meta is the separate `meta-ad-builder` skill. Every ad it creates is PAUSED.

## Testing order

Angles 1 and 2 carry the landing page's own headline and named mechanism, so they are the
cleanest read on whether the page converts cold traffic. Start there, one angle per ad set,
static before video — statics are ~0.03 credits versus ~1 for Veo, so you can buy a lot more
signal for the same spend before committing to a UGC production.

## Three templates you cannot use on this offer

The library contains before/after formats. They are prohibited here — Meta restricts
before/after imagery for health and appearance products, and the product itself promises no
physical change:

- **T13** — Before/After two-panel split
- **T19** — Fake AirDrop dialog (with before/after)
- **T17** — Stacked-bar "with vs without", if framed as a change in the viewer's face

T17 is usable if the comparison is about *clarity of direction* (guessing from YouTube vs
following a personalized plan), not about facial change. See `03-image-ads.md`.
