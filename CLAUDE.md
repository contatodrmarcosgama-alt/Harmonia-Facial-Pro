@shared/CLAUDE.md

# Harmonia Facial Pro — repo guide

This repo holds two things:

1. **The product landing page** — `index.html`, a single self-contained pt-BR sales page
   (inline CSS + JS, no build step). Open it directly in a browser to preview.
2. **The Arcads ad-creative pack** — skills for generating the Meta ad creative that drives
   traffic to that page. Vendored from
   [`krusemediallc/arcads-claude-code`](https://github.com/krusemediallc/arcads-claude-code)
   (MIT — see `docs/arcads/LICENSE`).

**The offer, brand voice, and audience live in `MASTER_CONTEXT.md`. Read it before writing
any ad copy or creative prompt.** Creative briefs derived from the landing page are in
`ads/briefs/`.

## Landing page rules

- `index.html` is the deliverable — edit it in place, keep it self-contained (no build,
  no external JS deps beyond the Google Fonts link).
- All customer-facing copy is **Brazilian Portuguese**. Match the existing register:
  direct, second-person, plain words, short sentences.
- Price and offer values (R$197 → R$47, the three bonuses, the 7-day guarantee) appear in
  several places. Change them everywhere or nowhere, and mirror any change into
  `MASTER_CONTEXT.md`.

## Arcads-specific session rules

- **API:** Arcads external API (`https://external-api.arcads.ai`).
- **Auth:** HTTP Basic via `ARCADS_BASIC_AUTH` or `ARCADS_API_KEY` in `.env`.
  Setup check: `./scripts/check-arcads-env.sh`.
- **Skill:** `.claude/skills/arcads-external-api/SKILL.md` for API calls, prompts, and polling.
- **Image-ad ecosystem (Meta image creatives):** read
  `shared/skills/image-ad-prompting/OVERVIEW.md` FIRST. Three skills (`chatgpt-image-ad`,
  `nano-banana-image-ad`, `image-ad-clone`) + a shared 37-template prompt library. The
  `image-ad-clone` skill asks which backend to validate against at Phase 1, so generic
  "clone this ad" prompts route correctly. Output is image files; Meta upload is the
  separate `meta-ad-builder` skill.
- **Cost disclosure:** Always present credit totals as **estimates** — Arcads has no billing
  endpoint. Tell the user to confirm exact pricing in the Arcads platform.
- **Logging:** Log every generation call to `logs/arcads-api.jsonl`.
- **First-time setup:** If `.env` is missing, run `./scripts/setup.sh`.

## Advertising compliance (non-negotiable)

This is a health/appearance offer aimed at a young male audience, running on Meta. Creative
that ignores this gets accounts restricted, so treat these as hard constraints:

- **No before/after face comparisons.** Meta prohibits them for health and appearance
  products, and the product itself explicitly makes no promise of physical change.
- **No implied personal attributes.** Never write ad copy that asserts something about the
  viewer ("você é feio", "seu rosto é assimétrico"). Speak to the situation and the desire,
  not to a claimed defect in the reader.
- **No medical or guaranteed-outcome claims.** The app produces a descriptive report and an
  action plan. It does not diagnose, treat, or guarantee a result.
- **No scores or ratings.** "Sem scores, sem julgamentos" is a core product promise — creative
  that shows a rating out of 10 contradicts the product.
- **Faces in creative must be AI-generated or licensed.** Never use a real patient photo
  without written release, and never use Dr Marcos Gama's clinical photography in ads.
